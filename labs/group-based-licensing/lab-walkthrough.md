# Lab Walkthrough: Group-Based Licensing Migration

## Overview

This walkthrough documents the complete migration process from direct (PowerShell-managed) license assignments to group-based licensing in Microsoft Entra ID for an organisation of 1,000 users.

---

## Step 1 — Assign the License to the "All Users" Group

### Where to do it
**Azure Portal → Microsoft Entra ID → Groups → All Users → Licenses**

### Steps
1. Sign in to the **Azure Portal** (portal.azure.com)
2. Navigate to **Microsoft Entra ID**
3. Select **Groups** from the left menu
4. Search for and open the **"All Users"** group
5. Select **Licenses** from the left panel
6. Click **+ Assignments**
7. Select **Office 365 Enterprise E3**
8. Review the license plan options (enable/disable specific service plans if needed)
9. Click **Save**

### What Happens Next
- Microsoft Entra ID begins processing the license assignment for all 1,000 group members
- This is an asynchronous background process — it may take several minutes to hours for large organisations
- Users will receive both their existing **direct** license and the new **group** license simultaneously during migration

> 💡 **SC-300 Tip:** Group-based licensing is processed asynchronously. For large groups, always check processing status before proceeding to the next step.

---

## Step 2 — Confirm License Assignment Has Completed

### Where to check
**Azure Portal → Microsoft Entra ID → Groups → All Users → Licenses**

### What to look for

| Status Message | Meaning |
|---|---|
| ✅ "Latest license changes have been applied to all users" | Processing complete — safe to proceed |
| 🔄 "Processing..." | Still running — wait before continuing |
| ⚠️ "X users have errors" | Some users could not receive the license |

### Common Errors and Resolutions

**Error 1: Insufficient Licenses**
- **Cause:** The tenant does not have enough E3 licenses for all 1,000 users
- **Resolution:** Purchase additional licenses in the Microsoft 365 Admin Center
- **Check:** Microsoft 365 Admin Center → Billing → Licenses

**Error 2: Conflicting License Plans**
- **Cause:** A user already has a license that includes a service plan conflicting with E3
- **Example:** User has Office 365 E1 with Exchange Online Plan 1, and E3 also includes Exchange Online Plan 2 — some plans cannot coexist
- **Resolution:** Disable the conflicting service plan in the group license assignment, or remove the conflicting direct license first

**Error 3: User Account Issues**
- **Cause:** Disabled accounts, accounts pending deletion, or accounts without a usage location set
- **Resolution:** Ensure all user accounts have a **Usage Location** set (required for license assignment)

---

## Step 3 — Verify User License State

### Where to check
**Azure Portal → Microsoft Entra ID → Users → [Select User] → Licenses**

### Expected User State During Migration

During migration, each user should show **two license entries** for Office 365 E3:

| Assignment Type | Source | State |
|---|---|---|
| ✅ Direct | Assigned directly to the user (from old PowerShell script) | Active |
| ✅ Inherited | Assigned via "All Users" group | Active |

Both entries provide identical access — the user only consumes **one license**, not two.

### What to Verify
- Both direct and group licenses show as **Active**
- The service plans enabled are identical in both
- The user has full access to Office 365 services

> 💡 **SC-300 Tip:** Having both direct and group licenses assigned is normal during migration. The user's access is unaffected — this dual state is intentional and temporary.

---

## Step 4 — Remove Direct Licenses (Individual Testing)

### Testing with a Single User First
Before bulk removal, test the removal on **one or two users** to confirm no access disruption occurs.

**Azure Portal → Users → [Select User] → Licenses → [Select E3 Direct] → Remove**

### Expected Result After Removal

| Before Removal | After Removal |
|---|---|
| Direct: Office 365 E3 ✅ | Direct: Office 365 E3 ❌ (removed) |
| Group (All Users): E3 ✅ | Group (All Users): E3 ✅ (remains) |
| User access: Active | User access: Active ✅ (unchanged) |

The license state remains **unchanged** — the user retains full access via group inheritance.

---

## Step 5 — Bulk Remove Direct Licenses via PowerShell

Once individual testing confirms no disruption, run the PowerShell script to remove direct licenses from all 1,000 users in bulk.

### Prerequisites
```powershell
# Install required module
Install-Module Microsoft.Graph -Scope CurrentUser

# Connect to Microsoft Graph
Connect-MgGraph -Scopes "User.ReadWrite.All", "Organization.Read.All"
```

### Script — Remove Direct E3 License from All Users

```powershell
# Define the E3 license SKU ID
# Find your SKU ID: Get-MgSubscribedSku | Select SkuPartNumber, SkuId
$e3SkuId = "YOUR-E3-SKU-ID-HERE"  # Replace with actual SKU ID

# Get all users with a direct E3 license assignment
$users = Get-MgUser -All -Property Id, DisplayName, AssignedLicenses |
    Where-Object {
        $_.AssignedLicenses | Where-Object {
            $_.SkuId -eq $e3SkuId -and
            $_.AssignedByGroup -eq $null  # Direct assignments only
        }
    }

Write-Host "Found $($users.Count) users with direct E3 licenses"

# Remove direct license from each user
foreach ($user in $users) {
    try {
        Set-MgUserLicense -UserId $user.Id `
            -AddLicenses @() `
            -RemoveLicenses @($e3SkuId)

        Write-Host "✅ Removed direct license from: $($user.DisplayName)"
    }
    catch {
        Write-Host "❌ Error for $($user.DisplayName): $($_.Exception.Message)"
    }
}

Write-Host "Migration complete."
```

### Verify Bulk Removal

```powershell
# Confirm no users have direct E3 assignments remaining
$remaining = Get-MgUser -All -Property Id, DisplayName, AssignedLicenses |
    Where-Object {
        $_.AssignedLicenses | Where-Object {
            $_.SkuId -eq $e3SkuId -and
            $_.AssignedByGroup -eq $null
        }
    }

Write-Host "Users still with direct E3 license: $($remaining.Count)"
# Expected result: 0
```

---

## Migration Complete ✅

### Post-Migration State

| Item | State |
|---|---|
| License assignment method | Group-based (All Users group) |
| Direct assignments | 0 — all removed |
| PowerShell script | Decommissioned — no longer needed |
| New user onboarding | Automatic — added to All Users group = gets E3 |
| User offboarding | Automatic — removed from All Users group = loses E3 |

### Benefits Achieved

| Before | After |
|---|---|
| Manual PowerShell script runs required | Fully automatic — Entra ID manages licenses |
| Risk of missed license assignments | New users get license on account creation |
| Risk of orphaned licenses on departures | Removed users lose license automatically |
| IT admin overhead | Near zero — self-managing |
| Audit trail | Full license assignment history in Entra ID |

---

## Key Exam Points — SC-300

- Group-based licensing **does not require** Azure AD Premium P1 for the basic feature, but **does require** P1 for advanced features like dynamic groups
- **Dynamic groups** auto-add users based on attributes (e.g. department = "Sales") — the most powerful combination with group-based licensing
- The **All Users** group in Entra ID is a built-in group that cannot be deleted
- License assignment errors appear in the group's **Licenses** blade with details on affected users
- **Usage Location** must be set on user accounts before licenses can be assigned
- Removing a direct license when a group license exists causes **no service interruption**
