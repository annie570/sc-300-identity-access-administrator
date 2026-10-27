# 🔐 SC-300: Microsoft Identity and Access Administrator

> Microsoft Certification Study Repository | Exam SC-300 | Microsoft Entra ID | Identity & Access Management

---

## 📋 About This Repository

This repository documents my hands-on labs, study notes, and practical exercises completed while preparing for the **Microsoft SC-300: Identity and Access Administrator** certification exam.

The SC-300 exam measures the ability to implement, manage, and monitor identity and access environments using Microsoft Entra ID (formerly Azure Active Directory). It is a core certification for cybersecurity professionals specialising in **Identity & Access Management (IAM)**.

---

## 🎯 Exam Overview

| Detail | Information |
|---|---|
| **Exam** | SC-300: Microsoft Identity and Access Administrator |
| **Certification** | Microsoft Certified: Identity and Access Administrator Associate |
| **Study Status** | 🔄 In Progress |
| **Candidate** | Ann Okwach |
| **Credly Profile** | [credly.com/users/ann-okwach](https://www.credly.com/users/ann-okwach) |
| **Related Cert** | SC-900 ✅ (already achieved — Security, Compliance & Identity Fundamentals) |

---

## 📚 SC-300 Exam Domains

| Domain | Weight | Coverage |
|---|---|---|
| **1. Implement identities in Microsoft Entra ID** | ~25% | Users, groups, external identities, hybrid identity |
| **2. Implement authentication and access management** | ~25% | MFA, Conditional Access, identity protection |
| **3. Implement access management for applications** | ~25% | Enterprise apps, app registrations, SSO, permissions |
| **4. Plan and implement identity governance** | ~25% | Entitlement management, access reviews, PIM, compliance |

---

## 📁 Repository Structure

```
sc-300-identity-access-administrator/
├── README.md                              # This file
├── notes/
│   └── exam-domain-notes.md              # Key concepts per exam domain
├── labs/
│   ├── group-based-licensing/
│   │   ├── README.md                     # Lab overview
│   │   ├── lab-walkthrough.md            # Step-by-step migration guide
│   │   └── powershell-reference.md       # PowerShell commands reference
│   └── conditional-access/
│       └── README.md                     # Conditional Access lab (coming soon)
└── assets/
    └── diagrams.md                       # Architecture and flow diagrams
```

---

## 🧪 Labs Completed

| Lab | Topic | Domain | Status |
|---|---|---|---|
| [User License Assignment](./labs/user-license-assignment/) | Creating users in Entra ID and assigning Microsoft 365 licenses | Domain 1 | ✅ Complete |
| [Group-Based Licensing Migration](./labs/group-based-licensing/) | Migrating from PowerShell scripts to Entra ID group-based licensing | Domain 1 | ✅ Complete |
| [Guest Users — B2B Collaboration](./labs/guest-users-b2b/) | Inviting single and bulk guest users, managing B2B access and Conditional Access for guests | Domain 1 | ✅ Complete |
| [Configure Identity Providers](./labs/configure-identity-providers/) | SAML/WS-Fed IdP federation, Google federation for Gmail B2B guests, Facebook federation for self-service sign-up | Domain 1 | ✅ Complete |
| Conditional Access Policies | Creating and testing Conditional Access rules | Domain 2 | 🔄 Coming Soon |
| Privileged Identity Management | Configuring JIT access and PIM roles | Domain 4 | 🔄 Coming Soon |
| Access Reviews | Scheduling and completing access reviews | Domain 4 | 🔄 Coming Soon |
| Enterprise App SSO | Configuring SAML SSO for an enterprise application | Domain 3 | 🔄 Coming Soon |

---

## 🔗 Related Projects

- [MFA & SSO Implementation](https://github.com/annie570/mfa-sso-implementation) — Full MFA and SSO design project
- [IAM Solution Design](https://github.com/annie570/Designing-IAM-Solution) — IAM architecture design
- [Google IT Support Portfolio](https://github.com/annie570/google-it-support-portfolio) — Broader IT portfolio
- [Credly Badges](https://www.credly.com/users/ann-okwach) — Verified certifications

---

## 📖 Study Resources

- [Microsoft Learn — SC-300 Learning Path](https://learn.microsoft.com/en-us/certifications/exams/sc-300)
- [Microsoft Entra ID Documentation](https://learn.microsoft.com/en-us/entra/identity/)
- [SC-300 Exam Skills Outline](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/sc-300)
