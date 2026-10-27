# Lab: Migrating to Group-Based Licensing in Microsoft Entra ID

**Exam Domain:** 1 — Implement identities in Microsoft Entra ID
**Topic:** Group-based licensing
**Difficulty:** Intermediate
**Status:** ✅ Complete

---

## 🎯 Lab Objective

Migrate an organisation of **1,000 users** from a PowerShell-based license assignment script to **Microsoft Entra ID group-based licensing**, enabling automatic license management as users join and leave the organisation.

---

## 🏢 Scenario

An organisation has 1,000 users who all require **Office 365 Enterprise E3** licenses. Currently, a PowerShell script runs on-premises to add and remove licenses as users come and go. This manual approach is error-prone and requires ongoing maintenance.

**Goal:** Replace the PowerShell script with group-based licensing so licenses are managed automatically by Microsoft Entra ID.

---

## 📋 Pre-Migration State

| Item | Current State |
|---|---|
| Users | 1,000 |
| License required | Office 365 Enterprise E3 |
| Assignment method | PowerShell script (on-premises) |
| Assignment type | Direct license assignments per user |
| Management | Manual — IT team runs script as users join/leave |

---

## 🔄 Migration Overview

```
BEFORE:                          AFTER:
PowerShell Script                Microsoft Entra ID
      ↓                                ↓
Direct License Assignment   →   Group-Based License Assignment
  (per user, manual)              (automatic via "All Users" group)
```

---

## 📖 Full Step-by-Step Walkthrough

See [lab-walkthrough.md](./lab-walkthrough.md) for the complete migration guide.

---

## ✅ Key Learning Outcomes

- Assign licenses to groups in Microsoft Entra ID via the Azure portal
- Verify group-based license assignment processing status
- Identify and resolve license assignment errors (insufficient licenses, conflicting plans)
- Understand the dual-assignment state during migration (direct + group)
- Remove direct license assignments after group-based licensing is confirmed
- Run bulk removal of direct licenses using PowerShell automation

---

## 🔑 Key Concepts for SC-300 Exam

| Concept | What to Know |
|---|---|
| Group-based licensing | Licenses assigned to a group are inherited by all members |
| Direct vs inherited | Both can coexist — user has same access either way |
| Processing status | Check "Latest license changes have been applied" confirmation |
| License errors | Insufficient licenses or conflicting plans prevent inheritance |
| All Users group | Built-in group in Entra ID — contains every user in the tenant |
| Bulk removal | PowerShell needed to remove direct licenses at scale |
