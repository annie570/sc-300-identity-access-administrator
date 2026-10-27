# Lab Walkthrough: Change User License Assignments

## Overview

This walkthrough covers two main tasks:
1. Creating a new user in Microsoft Entra ID
2. Assigning a Microsoft 365 license to that user

---

## Task 1 — Create a New User in Microsoft Entra ID

### Step 1 — Access the Microsoft Entra Admin Center

1. Open your browser and go to **entra.microsoft.com**
2. Sign in with your administrator account
3. In the left navigation, under **Identity**, select **Users**

---

### Step 2 — Create a New User

1. On the **Users** page, select **+ New user** from the top menu
2. Select **Create new user** from the dropdown

---

### Step 3 — Fill in User Details

Enter the following information on the Create new user page:

| Setting | Value |
|---|---|
| User name | `DominiqueK` |
| Name | `Dominique Koch` |
| First name | `Dominique` |
| Last name | `Koch` |
| Password | Create a unique secure password |
| Usage location | Select your preferred location (e.g. Kenya) |

> ⚠️ **Important — Usage Location:**
> The Usage Location field is **mandatory** before any license can be assigned.
> It determines which Microsoft 365 services are available based on regional regulations.
> If left blank, license assignment will fail.

---

### Step 4 — Review and Create

1. Review all the entered details
2. Click **Create** to finalise the account
3. You will be returned to the **All users** list

---

### Step 5 — Verify User Creation

- Confirm **Dominique Koch** appears in the **All users** list
- The account will show:
  - Display name: Dominique Koch
  - User principal name: DominiqueK@[yourtenant].onmicrosoft.com
  - Identity: Cloud-only (not synced from on-premises)

---

## Task 2 — Assign a License to the User

### Step 1 — Open the Microsoft 365 Admin Center

1. Go to **admin.microsoft.com**
2. Sign in with your administrator account

> 💡 **Note:** License assignment for individual users is managed through the
> **Microsoft 365 admin center**, not the Entra admin center.
> This is an important distinction for the SC-300 exam.

---

### Step 2 — Navigate to Licenses

1. In the left navigation, select **Billing**
2. Select **Licenses** from the submenu
3. You will see a list of all licenses available in your tenant

---

### Step 3 — Select a License

1. Select an **available license** from the list
   - Example: Microsoft 365 Business Basic, Microsoft 365 E3, etc.
2. The license details page opens showing:
   - Total licenses purchased
   - Licenses assigned
   - Licenses available

---

### Step 4 — Assign the License to Dominique Koch

1. Select **Licensed users** from the menu near the top of the page
2. Click **+ Assign licenses**
3. In the search box, type **Dominique Koch**
4. Select **Dominique Koch** from the search results
5. Click **Assign** at the bottom of the page

---

### Step 5 — Confirm Assignment

After clicking Assign:
- A confirmation message appears
- Dominique Koch now appears in the Licensed users list
- The license count updates (Available licenses decreases by 1)

---

## Task 3 — Verify License in Microsoft Entra Admin Center

### Step 1 — Return to Entra Admin Center

1. Go back to **entra.microsoft.com**
2. Navigate to **Identity → Users**
3. Search for and select **Dominique Koch**

---

### Step 2 — Check License on User Profile

1. On Dominique Koch's profile page
2. In the left panel, select **Licenses**
3. Verify the assigned license is listed

### Expected Result

| Field | Value |
|---|---|
| License name | [The license you assigned] |
| Assignment type | Direct |
| Status | Active |
| Assigned via | Microsoft 365 admin center |

---

## Summary of Steps Completed

| Step | Action | Location | Result |
|---|---|---|---|
| 1 | Browsed to Entra admin center | entra.microsoft.com | Accessed Identity portal |
| 2 | Created new user | Identity → Users → + New user | Dominique Koch account created |
| 3 | Set Usage Location | During user creation | Location set — license assignment enabled |
| 4 | Opened M365 admin center | admin.microsoft.com | Accessed license management |
| 5 | Navigated to Billing → Licenses | M365 admin center | Viewed available licenses |
| 6 | Assigned license | + Assign licenses → search → Assign | License assigned to Dominique Koch |
| 7 | Verified license | Entra admin center → User → Licenses | License confirmed as Active |

---

## Common Errors and Fixes

| Error | Cause | Fix |
|---|---|---|
| Cannot assign license | Usage Location not set | Go to user profile → Edit → set Usage Location |
| User not found in search | Account not yet created or wrong tenant | Verify user exists in Entra ID All users list |
| No licenses available | All licenses consumed | Purchase more licenses in Billing → Licenses |
| License shows as error | Service plan conflict | Disable conflicting service plan in license assignment |
| License not visible in Entra | Processing delay | Wait a few minutes and refresh the Licenses page |

---

## Admin Centers — Key Differences

| Task | Where to Do It |
|---|---|
| Create / manage users | Microsoft Entra admin center |
| Assign individual licenses | Microsoft 365 admin center |
| Assign group-based licenses | Microsoft Entra admin center |
| View user license status | Microsoft Entra admin center (User → Licenses) |
| Purchase new licenses | Microsoft 365 admin center (Billing) |
| Bulk license management | PowerShell (Microsoft Graph) |
