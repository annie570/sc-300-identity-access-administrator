# Verification Checklist — SSPR Lab

---

## Task 1 — Create Security Group ✅

- [ ] Navigated to **Entra admin center → Manage → Groups**
- [ ] Selected **+ New Group**
- [ ] Set Group type to **Security**
- [ ] Set Group name to **SSPRTesters**
- [ ] Set Membership type to **Assigned**
- [ ] Selected **Create**
- [ ] Confirmed SSPRTesters appears in the Groups list

---

## Task 2 — Create Test User ✅

- [ ] Navigated to **Manage → Users → + New user → Create new user**
- [ ] Set User principal name to **balas**
- [ ] Set Display name to **Bala Sandhu**
- [ ] Copied and saved the auto-generated password
- [ ] Selected the **Assignments** tab
- [ ] Added **SSPRTesters** group assignment
- [ ] Selected **Review + create → Create**
- [ ] Confirmed Bala Sandhu appears in All users list

---

## Task 3 — Enable and Configure SSPR ✅

- [ ] Navigated to **Manage → Password reset**
- [ ] Changed scope from None to **Selected**
- [ ] Selected **SSPRTesters** as the target group
- [ ] Selected **Save**
- [ ] Reviewed **Authentication methods** — confirmed Email is enabled
- [ ] Reviewed **Registration** settings
- [ ] Reviewed **Notifications** settings
- [ ] Navigated to **Customization**
- [ ] Set custom helpdesk link to **Yes**
- [ ] Entered admin email/URL in the custom helpdesk box
- [ ] Selected **Save**

---

## Task 4 — Register Email for SSPR ✅

- [ ] Opened a **private/incognito** browser window
- [ ] Navigated to **https://aka.ms/ssprsetup**
- [ ] Signed in as **balas@[domain].onmicrosoft.com**
- [ ] Updated password if prompted (saved new password)
- [ ] Selected **Security info → + Add sign-in method**
- [ ] Selected **Email** as the method
- [ ] Entered personal email address
- [ ] Retrieved and entered verification code from email
- [ ] Email method confirmed as registered

---

## Task 5 — Test SSPR ✅

- [ ] Opened a **new private/incognito** browser window
- [ ] Navigated to **https://aka.ms/sspr**
- [ ] Entered **balas@[domain].onmicrosoft.com** as User ID
- [ ] Completed the CAPTCHA
- [ ] Selected **Email my alternate email**
- [ ] Retrieved and entered verification code from email
- [ ] Entered and confirmed new password
- [ ] Selected **Finish**
- [ ] Confirmed password reset completed successfully

---

## Exam-Style Questions

**Q1: What are the three SSPR scope options and when should each be used?**
> - **None** — SSPR is completely disabled; no users can reset their own password
> - **Selected** — SSPR enabled for members of one specific group; use this for
>   pilots and controlled rollouts before going tenant-wide
> - **All** — SSPR enabled for every user in the tenant; use after successful pilot

**Q2: Why was a non-administrator account used to test SSPR in this lab?**
> Administrator accounts have different SSPR behaviour — they are always required
> to use email for resets and cannot use security questions. To test the standard
> end-user SSPR experience, a non-admin account must be used.

**Q3: What must a user do before they can use SSPR to reset their password?**
> The user must first **register at least one authentication method** at
> `https://aka.ms/ssprsetup`. Without completing registration, SSPR will not
> work even if the feature is enabled for their group.

**Q4: What does the custom helpdesk setting in SSPR do?**
> It replaces the default "Contact your administrator" link shown to users
> when they cannot reset their own password. You can set it to an email address
> or a URL pointing to your IT helpdesk portal or ticketing system.

**Q5: A user at your organisation resets their cloud password via SSPR but their on-premises Active Directory password is unchanged. What feature is needed to fix this?**
> **Password writeback** — this feature syncs cloud password resets back to
> the on-premises Active Directory. It requires Azure AD Connect to be configured
> and an **Azure AD Premium P1** license.

**Q6: What is the URL where users register their SSPR authentication methods?**
> `https://aka.ms/ssprsetup`
> This is the registration portal where users add and manage their
> authentication methods for SSPR.

**Q7: What is the URL where users go to actually reset their forgotten password?**
> `https://aka.ms/sspr`
> This is the self-service password reset portal where users initiate
> the password reset process.

**Q8: A user reports they see "The administrator has not enabled this feature" when trying to register for SSPR. What is the most likely cause?**
> The user is NOT signed in with a private/incognito browser window.
> Their existing browser session may be interfering with the registration flow.
> Opening a fresh private/incognito window and signing in again usually resolves this.

---

## SC-300 Exam Relevance

| Skill Area | Covered |
|---|---|
| Enable and configure SSPR | ✅ Task 3 |
| SSPR scope — None / Selected / All | ✅ Task 3 |
| Configure SSPR authentication methods | ✅ Task 3 |
| Configure SSPR registration settings | ✅ Task 3 |
| Configure SSPR notifications | ✅ Task 3 |
| Custom helpdesk configuration | ✅ Task 3 |
| SSPR registration as end user | ✅ Task 4 |
| Test end-to-end SSPR flow | ✅ Task 5 |
| Understand password writeback | ✅ Exam questions |
| SSPR licensing requirements | ✅ Walkthrough |
