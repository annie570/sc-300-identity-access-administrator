# PowerShell Reference — Group-Based Licensing

Quick reference for Microsoft Graph PowerShell commands used in license management.

---

## Setup and Connection

```powershell
# Install Microsoft Graph PowerShell module
Install-Module Microsoft.Graph -Scope CurrentUser

# Connect with required permissions
Connect-MgGraph -Scopes "User.ReadWrite.All", "Organization.Read.All", "Directory.Read.All"

# Verify connection
Get-MgContext
```

---

## Finding License SKU IDs

```powershell
# List all available licenses in the tenant
Get-MgSubscribedSku | Select-Object SkuPartNumber, SkuId, ConsumedUnits, @{
    Name="TotalLicenses"
    Expression={$_.PrepaidUnits.Enabled}
}

# Common SKU Part Numbers
# ENTERPRISEPACK      = Office 365 E3
# ENTERPRISEPREMIUM   = Office 365 E5
# SPE_E3              = Microsoft 365 E3
# SPE_E5              = Microsoft 365 E5
# AAD_PREMIUM         = Azure AD Premium P1
# AAD_PREMIUM_P2      = Azure AD Premium P2
```

---

## Viewing User Licenses

```powershell
# Get licenses for a specific user
$user = Get-MgUser -UserId "ann@contoso.com" -Property AssignedLicenses, DisplayName
$user.AssignedLicenses

# Get all users with a specific license
$skuId = "YOUR-SKU-ID"
Get-MgUser -All -Property Id, DisplayName, AssignedLicenses |
    Where-Object { $_.AssignedLicenses.SkuId -contains $skuId }

# Count licensed users
(Get-MgUser -All -Filter "assignedLicenses/`$count ne 0" -ConsistencyLevel eventual -CountVariable count)
Write-Host "Licensed users: $count"
```

---

## Assigning Licenses

```powershell
# Assign a license to a single user
$license = @{
    SkuId = "YOUR-SKU-ID"
    DisabledPlans = @()  # Leave empty to enable all plans
}

Set-MgUserLicense -UserId "user@contoso.com" `
    -AddLicenses @($license) `
    -RemoveLicenses @()

# Assign license with specific service plans disabled
$license = @{
    SkuId = "YOUR-E3-SKU-ID"
    DisabledPlans = @("SERVICE-PLAN-ID-TO-DISABLE")
}

Set-MgUserLicense -UserId "user@contoso.com" `
    -AddLicenses @($license) `
    -RemoveLicenses @()
```

---

## Removing Licenses

```powershell
# Remove a specific license from one user
Set-MgUserLicense -UserId "user@contoso.com" `
    -AddLicenses @() `
    -RemoveLicenses @("YOUR-SKU-ID")

# Remove direct license from ALL users (bulk migration script)
$skuId = "YOUR-E3-SKU-ID"

Get-MgUser -All -Property Id, DisplayName, AssignedLicenses | ForEach-Object {
    $directLicense = $_.AssignedLicenses | Where-Object {
        $_.SkuId -eq $skuId -and $_.AssignedByGroup -eq $null
    }

    if ($directLicense) {
        Set-MgUserLicense -UserId $_.Id `
            -AddLicenses @() `
            -RemoveLicenses @($skuId)
        Write-Host "Removed from: $($_.DisplayName)"
    }
}
```

---

## Group License Management

```powershell
# Get license assignments for a group
Get-MgGroupLicense -GroupId "GROUP-ID"

# Assign license to a group
$license = @{
    SkuId = "YOUR-SKU-ID"
    DisabledPlans = @()
}

Set-MgGroupLicense -GroupId "GROUP-ID" `
    -AddLicenses @($license) `
    -RemoveLicenses @()

# Find the All Users group ID
Get-MgGroup -Filter "displayName eq 'All Users'" | Select-Object Id, DisplayName

# Check group license processing errors
Get-MgGroupMemberWithLicenseError -GroupId "GROUP-ID" |
    Select-Object Id, DisplayName
```

---

## Setting Usage Location (Required Before License Assignment)

```powershell
# Set usage location for a single user (required for license assignment)
Update-MgUser -UserId "user@contoso.com" -UsageLocation "KE"  # KE = Kenya

# Set usage location for all users missing it
Get-MgUser -All -Property Id, DisplayName, UsageLocation |
    Where-Object { -not $_.UsageLocation } |
    ForEach-Object {
        Update-MgUser -UserId $_.Id -UsageLocation "KE"
        Write-Host "Set location for: $($_.DisplayName)"
    }
```

---

## Audit and Reporting

```powershell
# Export all user license states to CSV
Get-MgUser -All -Property Id, DisplayName, UserPrincipalName, AssignedLicenses |
    Select-Object DisplayName, UserPrincipalName,
        @{Name="Licenses"; Expression={($_.AssignedLicenses.SkuId) -join ", "}} |
    Export-Csv -Path "license-report.csv" -NoTypeInformation

# Find users with no license
Get-MgUser -All -Property Id, DisplayName, AssignedLicenses |
    Where-Object { $_.AssignedLicenses.Count -eq 0 } |
    Select-Object DisplayName

# Find users with license errors in a group
$groupId = "ALL-USERS-GROUP-ID"
Get-MgGroupMemberWithLicenseError -GroupId $groupId |
    ForEach-Object {
        $user = Get-MgUser -UserId $_.Id -Property DisplayName, UserPrincipalName
        [PSCustomObject]@{
            Name  = $user.DisplayName
            UPN   = $user.UserPrincipalName
            Error = "License assignment error — check Entra ID portal"
        }
    } | Export-Csv -Path "license-errors.csv" -NoTypeInformation
```

---

## Common Country Codes for Usage Location

| Country | Code |
|---|---|
| Kenya | KE |
| United States | US |
| United Kingdom | GB |
| South Africa | ZA |
| Nigeria | NG |
| Germany | DE |
| Denmark | DK |
