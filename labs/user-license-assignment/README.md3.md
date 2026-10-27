# Lab: Change User License Assignments

**Exam Domain:** 1 — Implement identities in Microsoft Entra ID
**Topic:** User creation and license assignment
**Platform:** Microsoft Entra admin center + Microsoft 365 admin center
**Status:** ✅ Complete

---

## 🎯 Lab Objective

Create a new user in Microsoft Entra ID and assign a Microsoft 365 license to them through the Microsoft 365 admin center. Verify the license appears correctly on the user's profile in the Entra admin center.

---

## 🏢 Scenario

As an Identity Administrator, you are responsible for onboarding new users and ensuring they have the correct licenses assigned. In this lab, you will create a new user account for **Dominique Koch** and assign an available Microsoft 365 license to their account.

---

## 📋 Prerequisites

| Requirement | Detail |
|---|---|
| Tenant | Microsoft Entra tenant (free trial acceptable) |
| Role required | User Administrator (minimum) |
| Admin centers | Microsoft Entra admin center + Microsoft 365 admin center |
| License | At least one available Microsoft 365 license in the tenant |

---

## 📁 Lab Files

| File | Description |
|---|---|
| [lab-walkthrough.md](./lab-walkthrough.md) | Step-by-step lab guide with screenshots descriptions |
| [verification-checklist.md](./verification-checklist.md) | Checklist to confirm all steps completed correctly |

---

## ✅ Key Learning Outcomes

- Create a new user in Microsoft Entra ID using the admin center
- Understand required user fields including Usage Location
- Navigate the Microsoft 365 admin center for license management
- Assign a license to a specific user
- Verify license assignment in the Entra admin center
- Understand the relationship between Entra ID and Microsoft 365 admin center

---

## 🔑 Key Concepts for SC-300 Exam

| Concept | What to Know |
|---|---|
| Usage Location | Must be set before a license can be assigned — determines which services are available |
| User Administrator role | Can create users and manage licenses but cannot manage admin roles |
| License assignment | Can be done via Entra ID, Microsoft 365 admin center, or PowerShell/Graph API |
| Direct vs group licensing | Direct = assigned to individual user; Group = inherited from group membership |
| License verification | Always verify in Entra ID under User → Licenses after assignment |
