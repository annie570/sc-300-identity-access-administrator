# SAML 2.0 and WS-Fed Required Attributes Reference

Quick reference for the required attributes and claims when configuring
SAML/WS-Fed IdP federation in Microsoft Entra ID.

---

## SAML 2.0 Configuration

### Required Attributes in the SAML 2.0 Response from the IdP

| Attribute | Value — Workforce Tenant | Value — External Tenant |
|---|---|---|
| `AssertionConsumerService` | `https://login.microsoftonline.com/login.srf` | `https://<tenantID>.ciamlogin.com/login.srf` |
| `Audience` | `https://login.microsoftonline.com/<tenant ID>/` | `https://login.microsoftonline.com/<tenant ID>/` |
| `Issuer` | Partner IdP issuer URI e.g. `https://www.example.com/exk10l6w90DHM0yi...` | Partner IdP issuer URI |

> 💡 **Audience note:** New federations should use the tenanted endpoint
> (`https://login.microsoftonline.com/<tenant ID>/`).
> Existing federations using the global endpoint (`urn:federation:MicrosoftOnline`)
> continue to work but new ones should use the tenanted endpoint.

### Required Claims in the SAML 2.0 Token

| Claim | Value |
|---|---|
| `NameID Format` | `urn:oasis:names:tc:SAML:2.0:nameid-format:persistent` |
| `emailaddress` | `https://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` |

---

## WS-Federation Configuration

### Tested Compatible WS-Fed Providers
- **AD FS** (Active Directory Federation Services)
- **Shibboleth**

### Required Attributes in the WS-Fed Message from the IdP

| Attribute | Value — Workforce Tenant | Value — External Tenant |
|---|---|---|
| `PassiveRequestorEndpoint` | `https://login.microsoftonline.com/login.srf` | `https://<tenantID>.ciamlogin.com/login.srf` |
| `Audience` | `https://login.microsoftonline.com/<tenant ID>/` | `https://login.microsoftonline.com/<tenant ID>/` |
| `Issuer` | Partner IdP issuer URI | Partner IdP issuer URI |

### Required Claims in the WS-Fed Token

| Claim | Value |
|---|---|
| `ImmutableID` | `https://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID` |
| `emailaddress` | `https://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` |

---

## Domain Namespace Rules

| Rule | Detail |
|---|---|
| Federation is domain-scoped | Tied to namespaces like `contoso.com` or `fabrikam.com` |
| Multiple domains | You can associate multiple domains with a single federation config |
| Verified or unverified | Partner domain can be either Entra ID verified or unverified |
| DNS TXT record required | If passive authentication URL domain doesn't match the target domain, the partner must add a DNS TXT record |

---

## Configuration Methods

You can configure SAML/WS-Fed federation in two ways:

**Method 1 — Metadata XML URL (Recommended)**
- Link to the partner IdP's online security token service XML file
- Attributes are read and populated automatically
- Easier to maintain — updates automatically when IdP metadata changes

**Method 2 — Manual Entry**
- Enter each attribute value manually
- Use when the partner IdP does not publish a metadata URL
- Requires more coordination with the partner's IT team

---

## Key Exam Points

| Point | Detail |
|---|---|
| New guests only | SAML/WS-Fed federation only affects new guest invitations |
| Existing guests unaffected | Already-redeemed invitations keep their original auth method |
| Reset redemption status | Required to move an existing guest to federated auth |
| Deletion impact | Deleting federation = affected guests cannot sign in |
| Reinvite to fix | After deletion, delete the guest account and reinvite to restore access |
