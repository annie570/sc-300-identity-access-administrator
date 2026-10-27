# Lab: Set Up Self-Service Password Reset (SSPR)

**Exam Domain:** 2 — Implement authentication and access management
**Topic:** Self-Service Password Reset (SSPR)
**Platform:** Microsoft Entra admin center
**Status:** ✅ Complete

---

## 🎯 Lab Objectives

1. Create a security group for a limited SSPR rollout
2. Create a test user and assign them to the group
3. Enable and configure SSPR for the group
4. Register an email authentication method for the test user
5. Test the full SSPR password reset flow end-to-end

---

## 🏢 Scenario

Before rolling out Self-Service Password Reset to all users in your organisation,
you want to test the configuration with a limited group first. You will create a
security group called **SSPRTesters**, create a test user called **Bala Sandhu**,
enable SSPR for that group, and verify the entire reset flow works correctly
using email verification.

---

## 📋 Prerequisites

| Requirement | Detail |
|---|---|
| Tenant | Microsoft Entra tenant |
| Role required | Global Administrator or Authentication Policy Administrator |
| Test email address | A personal email address to register for SSPR testing |
| Browser | Private/incognito window recommended for user testing |

---

## 📁 Lab Files

| File | Description |
|---|---|
| [lab-walkthrough.md](./lab-walkthrough.md) | Complete step-by-step SSPR setup and test guide |
| [verification-checklist.md](./verification-checklist.md) | Checklist + exam-style questions |

---

## ✅ Key Learning Outcomes

- Create a security group and assign users to it
- Enable SSPR for a specific group (scoped rollout)
- Configure SSPR authentication methods (email)
- Set a custom helpdesk contact URL
- Register an authentication method as an end user
- Complete the full self-service password reset flow
- Understand SSPR licensing requirements

---

## 🔑 Key Concepts for SC-300 Exam

| Concept | What to Know |
|---|---|
| SSPR scope | None / Selected (group) / All — start with Selected for pilots |
| Authentication methods | Email, mobile app, phone, security questions — at least 1 required |
| Registration | Users must register before they can use SSPR |
| Combined registration | Registers MFA and SSPR methods in one flow |
| SSPR licensing | Requires Azure AD Premium P1 for writeback to on-premises AD |
| Password writeback | Syncs cloud password resets back to on-premises AD — requires P1 |
| Custom helpdesk | Optional — replaces default "contact your admin" link |
| SSPR portal | https://aka.ms/sspr — where users reset passwords |
| Registration portal | https://aka.ms/ssprsetup — where users register methods |
| Admin reset | Admins always use email — cannot use security questions |
