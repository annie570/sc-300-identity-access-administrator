# SC-300 Exam Domain Notes

Key concepts, definitions, and exam tips for each domain of the SC-300 exam.

---

## Domain 1 — Implement Identities in Microsoft Entra ID (~25%)

### User Management
- **Cloud-only users** — created directly in Entra ID
- **Synced users** — created on-premises AD, synced via Azure AD Connect
- **Guest users** — external B2B collaboration accounts (type: member vs guest)
- **Usage Location** — must be set before assigning licenses

### Group Types

| Type | Description | Use Case |
|---|---|---|
| Security group | Controls access to resources | License assignment, app access |
| Microsoft 365 group | Includes mailbox, Teams, SharePoint | Collaboration |
| Dynamic group | Auto-membership based on user attributes | Automatic license management |
| Assigned group | Manually managed membership | Specific controlled access |

### Group-Based Licensing Key Points
- Requires **Azure AD Premium P1** for dynamic groups
- Built-in **All Users** group includes all tenant members
- License errors visible in Group → Licenses blade
- Processing is **asynchronous** — check completion status before proceeding
- Users can have both **direct** and **group** licenses simultaneously
- Removing direct license when group license exists = **no disruption**

### Hybrid Identity
- **Azure AD Connect** — syncs on-prem AD to Entra ID
- **Password Hash Sync (PHS)** — password hashes synced to cloud (most common)
- **Pass-Through Authentication (PTA)** — authentication happens on-premises
- **Federation (ADFS)** — complex, on-prem federation server handles auth
- **Seamless SSO** — users auto sign-in on domain-joined devices

---

## Domain 2 — Implement Authentication and Access Management (~25%)

### Multi-Factor Authentication (MFA)
- Methods: Authenticator app (push/TOTP), FIDO2 keys, SMS (not recommended), voice call
- **Per-user MFA** — legacy method, avoid for new deployments
- **Security defaults** — basic MFA for all users, free tier
- **Conditional Access + MFA** — recommended, granular control

### Conditional Access
- **Signals:** User/group, location, device compliance, app, risk level
- **Controls:** Require MFA, block, require compliant device, require hybrid join
- **Named locations** — trusted IP ranges, countries
- **Report-only mode** — test policies before enforcing
- **Always evaluate** — even trusted locations can be required to MFA for sensitive apps

### Identity Protection
- **Sign-in risk** — likelihood that sign-in is not by the legitimate user
- **User risk** — likelihood that user account is compromised
- Risk levels: Low, Medium, High
- **Risk policies** — auto-remediate (require MFA, force password reset, block)
- Requires **Azure AD Premium P2**

### Password Policies
- **Self-Service Password Reset (SSPR)** — users reset own passwords
- **Password protection** — block common/custom banned passwords
- **Smart lockout** — protects against brute force

---

## Domain 3 — Implement Access Management for Applications (~25%)

### Enterprise Applications vs App Registrations

| | Enterprise Application | App Registration |
|---|---|---|
| What it is | Instance of an app in your tenant | Definition of your own app |
| Used for | SSO to 3rd party apps (Salesforce, Slack) | Building your own app |
| Configured in | Entra ID → Enterprise Applications | Entra ID → App Registrations |

### SSO Methods

| Method | Description | When to Use |
|---|---|---|
| **SAML** | XML-based federation | Legacy enterprise apps |
| **OIDC/OAuth 2.0** | Modern token-based | Modern cloud apps |
| **Password-based** | Vaulted credentials | Apps with no SSO support |
| **Linked** | Link to existing SSO | Already configured elsewhere |
| **Header-based** | HTTP header injection | Legacy apps (needs agent) |

### App Permissions
- **Delegated permissions** — app acts on behalf of signed-in user
- **Application permissions** — app acts as itself (no user — daemon/service)
- **Admin consent** — required for high-privilege permissions
- **User consent** — users can grant low-privilege permissions themselves

---

## Domain 4 — Plan and Implement Identity Governance (~25%)

### Entitlement Management
- **Access packages** — bundle of resources (groups, apps, SharePoint sites)
- **Catalogs** — containers for access packages
- **Policies** — who can request, approval workflow, expiry
- Requires **Azure AD Premium P2**

### Access Reviews
- Periodic reviews of who has access to what
- Reviewers: resource owners, managers, users themselves, designated reviewers
- On expiry: remove access, keep access, require approval
- Can review: group members, app assignments, privileged roles

### Privileged Identity Management (PIM)
- **Just-In-Time (JIT)** access — elevate privileges only when needed
- **Eligible** role — user can activate when needed
- **Active** role — permanently assigned (avoid for sensitive roles)
- Activation requires: MFA, justification, approval (optional), time limit
- Requires **Azure AD Premium P2**

### Lifecycle Workflows
- Automate identity lifecycle: joiner, mover, leaver
- **Joiner** — create account, send welcome email, assign license
- **Mover** — update attributes, change group membership
- **Leaver** — disable account, remove licenses, delete after retention period

---

## Exam Tips

| Tip | Detail |
|---|---|
| Know license requirements | P1 vs P2 features are frequently tested |
| Understand risk-based CA | Know when to use sign-in risk vs user risk policies |
| PIM vs direct assignment | PIM = eligible (JIT); direct = always active |
| Dynamic groups | Require P1; auto-manage membership via rules |
| SSPR requirements | Methods, admin policy, writeback (requires P1) |
| Consent framework | Know delegated vs application permissions |
| Access packages | Know the catalog → package → policy hierarchy |
| Hybrid identity | Know PHS vs PTA vs federation differences |
