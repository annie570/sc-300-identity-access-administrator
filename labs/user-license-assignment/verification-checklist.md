# Verification Checklist — User License Assignment Lab

Use this checklist to confirm all steps were completed successfully.

---

## Task 1 — User Creation ✅

- [ ] Navigated to **entra.microsoft.com**
- [ ] Selected **Identity → Users** in the left navigation
- [ ] Clicked **+ New user → Create new user**
- [ ] Set **User name** to `DominiqueK`
- [ ] Set **Name** to `Dominique Koch`
- [ ] Set **First name** to `Dominique`
- [ ] Set **Last name** to `Koch`
- [ ] Created a **unique secure password**
- [ ] Set **Usage Location** (required for license assignment)
- [ ] Clicked **Create**
- [ ] Confirmed **Dominique Koch** appears in the **All users** list

---

## Task 2 — License Assignment ✅

- [ ] Navigated to **admin.microsoft.com** (Microsoft 365 admin center)
- [ ] Selected **Billing → Licenses**
- [ ] Selected an **available license** from the list
- [ ] Selected **Licensed users** tab
- [ ] Clicked **+ Assign licenses**
- [ ] Searched for and selected **Dominique Koch**
- [ ] Clicked **Assign**
- [ ] Confirmed Dominique Koch appears in the **Licensed users** list

---

## Task 3 — Verification in Entra Admin Center ✅

- [ ] Returned to **entra.microsoft.com**
- [ ] Navigated to **Identity → Users → Dominique Koch**
- [ ] Selected **Licenses** from the user's left panel
- [ ] Confirmed the assigned license is listed
- [ ] Confirmed license **Status** shows as **Active**
- [ ] Confirmed **Assignment type** shows as **Direct**

---

## Key Questions — Test Your Understanding

**Q1: Why is Usage Location required before assigning a license?**
> Microsoft uses Usage Location to determine which services and features are
> available based on regional data privacy laws and service availability.
> Without it, the system cannot determine which services to provision.

**Q2: Where is individual license assignment managed — Entra admin center or M365 admin center?**
> Individual license assignments are managed in the **Microsoft 365 admin center**
> (admin.microsoft.com) under Billing → Licenses. The Entra admin center is used
> to view license status on a user's profile but not to assign them directly.

**Q3: What is the difference between direct and group-based license assignment?**
> **Direct** — license assigned specifically to one user; must be managed individually.
> **Group-based** — license inherited from group membership; automatically applied
> and removed as users join or leave the group.

**Q4: What role is required to complete this lab?**
> A minimum of **User Administrator** role is required to create users and manage
> licenses. Global Administrator also has these permissions.

**Q5: What happens if you try to assign a license without setting Usage Location?**
> The license assignment will fail with an error indicating that a Usage Location
> must be set before licenses can be assigned to the user.

---

## SC-300 Exam Relevance

This lab directly covers the following SC-300 exam skills:

| Skill | Covered |
|---|---|
| Create users in Microsoft Entra ID | ✅ |
| Configure user properties (Usage Location) | ✅ |
| Assign licenses to users | ✅ |
| Verify license assignment | ✅ |
| Navigate Entra and M365 admin centers | ✅ |
| Understand direct vs group license assignment | ✅ |
