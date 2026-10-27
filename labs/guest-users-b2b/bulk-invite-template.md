# Bulk Invite CSV Template — Guest Users

## CSV File Structure

The bulk invite CSV template contains the following columns:

| Column Header | Required | Description |
|---|---|---|
| `Email address to invite` | ✅ Yes | Individual email address of the guest user |
| `Redirection url` | ✅ Yes | URL the guest is redirected to after accepting the invitation |

---

## Example CSV Content

```csv
Email address to invite,Redirection url
john.partner@externalcompany.com,https://myapps.microsoft.com
sarah.vendor@supplierco.com,https://myapps.microsoft.com
mike.contractor@freelance.com,https://teams.microsoft.com
alice.consultant@advisory.com,https://portal.azure.com
bob.auditor@auditfirm.com,https://myapps.microsoft.com
```

---

## Redirection URL Options

The redirection URL is where the guest lands after accepting the invitation.
Choose the most appropriate destination for your use case:

| URL | Best For |
|---|---|
| `https://myapps.microsoft.com` | General app portal — shows all apps the guest can access |
| `https://teams.microsoft.com` | Guests invited primarily for Teams collaboration |
| `https://portal.azure.com` | Technical guests who need Azure portal access |
| Your company intranet URL | Guests who need access to a specific internal site |
| Specific SharePoint URL | Guests invited to collaborate on a specific SharePoint site |

---

## Email Address Rules — Important

Before completing the CSV, check every email address against these rules:

| Rule | ✅ Correct | ❌ Incorrect |
|---|---|---|
| Individual email only | `john@company.com` | `team@company.com` (group email) |
| No plus (+) symbols | `john@company.com` | `john+work@company.com` |
| Valid domain | `user@validomain.com` | `user@` (incomplete) |
| Standard format | `firstname.lastname@company.com` | `user@@company.com` |

---

## Step-by-Step: Complete and Upload the CSV

### Step 1 — Download the template
In Entra admin center:
`Identity → Users → All Users → Bulk operations → Bulk invite → Download sample CSV`

### Step 2 — Open in Excel or text editor
- Open the downloaded `.csv` file
- Keep the header row exactly as downloaded — do not rename columns

### Step 3 — Add guest users
- Add one row per guest
- Column A: email address to invite
- Column B: redirection URL

### Step 4 — Save the file
- Save as **CSV (Comma delimited)** format
- Do NOT save as .xlsx — must remain .csv

### Step 5 — Upload and validate
- Return to **Bulk invite users** pane
- Browse and select your saved CSV file
- Wait for validation to complete

### Step 6 — Fix errors if any
Common errors and fixes:

| Error Message | Fix |
|---|---|
| Invalid email format | Check for typos, missing @ symbol, or invalid domain |
| Plus symbol detected | Remove + and everything between it and @ |
| Group mailbox detected | Replace with individual email address |
| Missing redirection URL | Add a valid https:// URL in Column B |
| Empty row | Delete any blank rows in the CSV |

### Step 7 — Submit
- Click **Submit** once validation shows **"File uploaded successfully"**
- Monitor progress in **Bulk operation results**

---

## Bulk Operation Results — How to Read

After submission, navigate to:
`Identity → Users → Bulk operation results`

| Column | What It Means |
|---|---|
| Operation | Type (Bulk invite) |
| Status | Completed / In progress / Failed |
| # Success | Number of invitations sent successfully |
| # Failure | Number that failed — click to see details |
| Total Requests | Total rows in your CSV |
| Submitted by | Admin who ran the operation |
| Date | When the operation was submitted |

---

## After the Bulk Operation Completes

- All successfully invited guests appear in **All Users** with User type = **Guest**
- Guests receive invitation emails at their provided addresses
- Guests must **accept the invitation** before their account becomes active
- Pending invitations show as **Invited** state in the directory
- You can resend invitations from the user's profile if they did not receive it
