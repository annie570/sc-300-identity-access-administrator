# Lab Walkthrough: Set Up Self-Service Password Reset (SSPR)

---

## Overview

This lab has five tasks:
1. Create a security group (SSPRTesters)
2. Create a test user (Bala Sandhu)
3. Enable and configure SSPR
4. Register an email method as the test user
5. Test the password reset flow

---

## Task 1 — Create a Security Group

### Why create a group first?
Best practice is to roll out SSPR to a **limited group** first — a pilot group.
This lets you test the configuration and catch issues before enabling SSPR
for the entire organisation.

### Steps

1. Go to **entra.microsoft.com**
2. Under **Manage**, select **Groups**
3. Select **+ New Group**
4. Enter the following values:

| Setting | Value |
|---|---|
| Group type | Security |
| Group name | `SSPRTesters` |
| Group description | `Members are testing the rollout of SSPR` |
| Membership type | Assigned |

5. Select **Create**
6. Confirm **SSPRTesters** appears in the Groups list

> 💡 **SC-300 Tip:** Assigned membership = you manually add members.
> Dynamic membership = members added automatically based on user attributes.
> For a controlled pilot, use Assigned so you control exactly who is included.

---

## Task 2 — Create a Test User

### Why a non-admin account?
SSPR behaves differently for administrator accounts. Admin accounts always use
email for resets and cannot use security questions. To test the standard user
SSPR experience, always use a non-admin test account.

### Steps

1. Under **Manage**, select **Users**
2. Select **+ New user → Create new user**
3. Enter the following values:

| Setting | Value |
|---|---|
| User principal name | `balas` |
| Display name | `Bala Sandhu` |
| Password | Copy the auto-generated password and save it in Notepad |

4. Select the **Assignments** tab
5. Select **+ Add group**
6. Check the box for **SSPRTesters**
7. Select the **Select** button
8. Select **Review + create → Create**
9. Confirm **Bala Sandhu** appears in the All users list

---

## Task 3 — Enable and Configure SSPR

### Step 1 — Enable SSPR for the Group

1. Under **Manage**, select **Password reset**
2. On the **Properties** page:
   - Change the setting from **None** to **Selected**
   - Select the link under **Select Group**
   - Check the box for **SSPRTesters**
   - Select the **Select** button
3. Select **Save**

### SSPR Scope Options

| Option | Meaning |
|---|---|
| None | SSPR disabled for all users |
| Selected | SSPR enabled for members of a chosen group only |
| All | SSPR enabled for every user in the tenant |

> 💡 **Best practice:** Always start with **Selected** for a pilot group before
> rolling out to All. This limits the blast radius if there are configuration issues.

---

### Step 2 — Review Authentication Methods

1. Under **Manage**, select **Authentication methods**
2. Review the default settings
3. Ensure **Email** is selected as an available method
4. Note the available authentication methods:

| Method | Notes |
|---|---|
| Email | External email address — used in this lab |
| Mobile app notification | Microsoft Authenticator push |
| Mobile app code | Authenticator TOTP code |
| Mobile phone | SMS or voice call |
| Office phone | Voice call to office number |
| Security questions | Only available for non-admin accounts |

> 💡 **SC-300 Tip:** The number of methods required for reset can be set to 1 or 2.
> Requiring 2 methods is more secure but requires users to register more methods.

---

### Step 3 — Review Registration Settings

1. Under **Manage**, select **Registration**
2. Review the default values:

| Setting | Default | Notes |
|---|---|---|
| Require users to register when signing in | Yes | Users prompted on next sign-in |
| Number of days before re-confirmation | 180 | Users asked to verify methods every 180 days |

---

### Step 4 — Review Notification Settings

1. Under **Manage**, select **Notifications**
2. Review the default values:

| Setting | Default | Notes |
|---|---|---|
| Notify users on password reset | Yes | User receives email when password is reset |
| Notify all admins when admins reset password | Yes | Security alert for admin resets |

---

### Step 5 — Configure Custom Helpdesk

1. Under **Manage**, select **Customization**
2. Set **Customize helpdesk link** to **Yes**
3. In the **Custom helpdesk email or URL** box, enter:
   ```
   admin@<your-organization-domain>.onmicrosoft.com
   ```
   *(Replace with your actual Entra ID domain name)*
4. Select **Save**

> 💡 **What this does:** Replaces the default "Contact your administrator" link
> shown to users when they cannot reset their own password. Points them to
> your IT helpdesk instead.

---

## Task 4 — Register Email for SSPR

Now you will sign in as **Bala Sandhu** and register an email address for SSPR.

### Steps

1. Open a **new private/incognito browser window**

> ⚠️ Use private/incognito mode to avoid conflicts with your admin session.
> If you see "The administrator has not enabled this feature" — make sure
> you are in private/incognito mode.

2. Go to **https://aka.ms/ssprsetup**
3. Sign in with:
   - **Username:** `balas@<your-domain>.onmicrosoft.com`
   - **Password:** the password you saved in Notepad earlier
4. If prompted to update the password, create a new one and save it
5. Select the **Security info** tab
6. Select **+ Add sign-in method**
7. In the **Add a method** box, select **Email**
8. Enter your personal email address
9. Check your email inbox for the verification code
10. Enter the code in the text box
11. Select **Next**
12. Email is now registered as an SSPR method for Bala Sandhu

---

## Task 5 — Test Self-Service Password Reset

Now test the full reset flow as Bala Sandhu.

### Steps

1. Open a **new private/incognito browser window**
2. Go to **https://aka.ms/sspr**
3. For **User ID**, enter:
   ```
   balas@<your-domain>.onmicrosoft.com
   ```
4. Complete the **CAPTCHA**
5. Select **Next**
6. Select the **Email my alternate email** radio button
7. Select **Email**
8. Check your email inbox for the verification code
9. In the **Enter your verification code** box, enter the code
10. Select **Next**
11. Enter a **new password** and confirm it
12. Select **Finish**
13. Save the new password
14. Close the browser window

### Expected Result
✅ Password reset successfully without any administrator involvement
✅ Bala Sandhu can now sign in with the new password
✅ Bala Sandhu receives a notification email confirming the reset

---

## Full SSPR Flow Diagram

```
Admin setup:
SSPRTesters group created → Bala Sandhu added to group
        ↓
SSPR enabled for SSPRTesters group
        ↓
Email set as authentication method
        ↓
Custom helpdesk contact configured

User flow:
Bala Sandhu registers email at https://aka.ms/ssprsetup
        ↓
Bala Sandhu forgets password → goes to https://aka.ms/sspr
        ↓
Enters user ID + completes CAPTCHA
        ↓
Selects email verification
        ↓
Enters code received by email
        ↓
Sets new password
        ↓
✅ Password reset complete — no admin required
```

---

## SSPR Licensing Summary

| Scenario | License Required |
|---|---|
| Cloud-only users — password reset | Free (included in Entra ID Free) |
| SSPR with all authentication methods | Azure AD Premium P1 |
| Password writeback to on-premises AD | Azure AD Premium P1 |
| SSPR with Identity Protection risk policies | Azure AD Premium P2 |

---

## Common Issues and Fixes

| Issue | Cause | Fix |
|---|---|---|
| "Administrator has not enabled this feature" | Not in private/incognito mode | Open a new private/incognito window |
| Cannot find SSPRTesters when enabling SSPR | Group not yet created | Create the group first in Entra ID |
| Verification code email not received | Spam filter or incorrect email | Check spam folder; verify email address entered correctly |
| User cannot reset password | Not registered for SSPR | User must complete registration at https://aka.ms/ssprsetup first |
| Password does not meet requirements | Password policy | Check the tenant password policy for complexity requirements |
