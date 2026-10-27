# SC-300 Architecture Diagrams

Mermaid diagrams for key SC-300 concepts.
Renders natively on GitHub or at [mermaid.live](https://mermaid.live).

---

## Diagram 1: Group-Based Licensing Migration Flow

```mermaid
flowchart TD
    subgraph BEFORE["❌ Before Migration"]
        PS["⚙️ PowerShell Script\nRuns on-premises\nManual trigger required"]
        DA["📋 Direct License Assignment\nPer user, per script run\nError-prone"]
    end

    subgraph AFTER["✅ After Migration"]
        GBL["👥 All Users Group\nGroup-based licensing\nAutomatic"]
        AUTO["🔄 Automatic Management\nNew user → gets license\nRemoved user → loses license"]
    end

    subgraph MIGRATION["🔄 Migration Steps"]
        S1["Step 1\nAssign E3 to All Users group\nin Azure Portal"]
        S2["Step 2\nVerify processing complete\nCheck for errors"]
        S3["Step 3\nVerify users have both\ndirect + group licenses"]
        S4["Step 4\nTest removal on\nindividual users"]
        S5["Step 5\nBulk remove direct\nlicenses via PowerShell"]
    end

    BEFORE --> MIGRATION
    MIGRATION --> AFTER
    S1 --> S2 --> S3 --> S4 --> S5
```

---

## Diagram 2: User License State During Migration

```mermaid
flowchart LR
    subgraph DURING["During Migration — Dual Assignment"]
        U["👤 User"]
        DL["📋 Direct License\nOffice 365 E3\n(from PowerShell script)"]
        GL["👥 Group License\nOffice 365 E3\n(from All Users group)"]
        ACCESS["✅ Full Access\nOffice 365 E3\n(one license consumed)"]
    end

    U --> DL
    U --> GL
    DL --> ACCESS
    GL --> ACCESS
```

---

## Diagram 3: Conditional Access Policy Evaluation

```mermaid
flowchart TD
    SIGNIN["👤 User Sign-In Attempt"]

    SIGNIN --> SIGNALS

    subgraph SIGNALS["Signals Evaluated"]
        WHO["Who?\nUser / Group / Role"]
        WHAT["What app?\nSalesforce / M365 / Custom"]
        WHERE["Where from?\nLocation / Named IP / Country"]
        DEVICE["Which device?\nCompliant? Hybrid joined?"]
        RISK["Risk level?\nSign-in risk / User risk"]
    end

    SIGNALS --> POLICY["⚙️ Conditional Access\nPolicy Engine"]

    POLICY --> GRANT["✅ Grant Access"]
    POLICY --> MFA["📱 Require MFA"]
    POLICY --> COMP["💻 Require Compliant Device"]
    POLICY --> BLOCK["🚫 Block Access"]

    GRANT --> APP["🏢 Application"]
    MFA -->|MFA passed| APP
    COMP -->|Device compliant| APP
```

---

## Diagram 4: Privileged Identity Management (PIM) Flow

```mermaid
sequenceDiagram
    participant A as 👨‍💻 IT Admin
    participant PIM as 🛡️ PIM (Entra ID)
    participant MGR as 👔 Approver
    participant RES as ⚙️ Azure Resource

    Note over A,RES: Admin has ELIGIBLE role (not yet active)

    A->>PIM: Request role activation
    A->>PIM: Provide justification + select duration
    PIM->>A: Trigger MFA challenge
    A->>PIM: Complete MFA ✅
    PIM->>MGR: Send approval request (if required)
    MGR->>PIM: Approve request ✅
    PIM->>RES: Activate role (time-limited)
    RES-->>A: ✅ Elevated access granted

    Note over A,RES: After time window expires
    PIM->>RES: Role automatically deactivated
    RES-->>A: Access revoked — back to eligible only
```

---

## Diagram 5: Identity Lifecycle — Joiner Mover Leaver

```mermaid
flowchart LR
    subgraph JOIN["🟢 Joiner"]
        J1["HR creates employee record"]
        J2["Lifecycle workflow triggers"]
        J3["Entra ID account created"]
        J4["License assigned via group"]
        J5["Welcome email sent"]
        J6["MFA enrollment prompted"]
    end

    subgraph MOVE["🟡 Mover"]
        M1["HR updates job title/dept"]
        M2["Attributes synced to Entra ID"]
        M3["Dynamic group updates"]
        M4["Access packages updated"]
        M5["New licenses assigned\nOld licenses removed"]
    end

    subgraph LEAVE["🔴 Leaver"]
        L1["HR marks employee inactive"]
        L2["Account disabled immediately"]
        L3["Sessions + tokens revoked"]
        L4["Licenses removed"]
        L5["Account retained 30 days"]
        L6["Account deleted"]
    end

    JOIN --> MOVE --> LEAVE
    J1-->J2-->J3-->J4-->J5-->J6
    M1-->M2-->M3-->M4-->M5
    L1-->L2-->L3-->L4-->L5-->L6
```

---

## Diagram 6: Entra ID License Tiers — Feature Comparison

```mermaid
flowchart TD
    FREE["🆓 Entra ID Free\n• Basic user/group management\n• SSO (up to 10 apps)\n• MFA for admins\n• Security defaults"]

    P1["💎 Azure AD Premium P1\nEverything in Free PLUS:\n• Conditional Access\n• Group-based licensing\n• Dynamic groups\n• SSPR\n• Hybrid identity (PTA, PHS)\n• Password protection"]

    P2["👑 Azure AD Premium P2\nEverything in P1 PLUS:\n• Privileged Identity Management\n• Identity Protection (risk policies)\n• Access Reviews\n• Entitlement Management"]

    FREE --> P1 --> P2
```
