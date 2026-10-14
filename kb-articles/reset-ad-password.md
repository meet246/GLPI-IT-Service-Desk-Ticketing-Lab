# Reset a user's AD password (forgotten password / account locked out)

**Category:** Account & Access
**Audience:** IT Service Desk technicians (not visible to Self-Service users, not in the FAQ)
**Applies to:** standard domain user accounts in `corp.local`. **Not** for admin, service, or executive accounts (see Escalation).
**Written from:** ticket #11 (Ticket Scenario 1)

## Symptoms
- User calls saying they forgot their password, their password expired, or they're locked out of their PC.
- Windows login error: "The referenced account is currently locked out" or "The user name or password is incorrect."

## Before you start: verify identity (required)
Do not reset anything until identity is confirmed. Caller ID, name, or username alone is **not** verification.
1. Look up the user in AD and note the **Telephone** number on file.
2. Tell the caller you'll call them back. Hang up and call the **number on file**, never a number the caller gives you.
3. Confirm the request with the user's **manager** through a known channel (directory phone, or Teams/email from the manager's own account).
4. If you can't verify, don't reset. Add a follow-up to the ticket and escalate.

## Ticket
1. Create a ticket. Type: **Request**. Category: **Account & Access > Password reset**. Requester: **the user**. Request source: **Phone**.
2. Assign it to yourself.
3. Add a follow-up: `Identity verified via callback to directory number + manager confirmation.`

## Reset the password
1. On DC01, open **Active Directory Users and Computers**.
2. Find the user (right-click the domain → Find), then right-click the user → **Reset Password**.
3. Enter a temporary password that meets the domain password policy.
4. Tick **User must change password at next logon**.
5. Tick **Unlock the user's account** if it shows as locked.
6. Click OK. Give the user the temporary password **verbally on the callback**. Never send it by email or chat, and never put it in the ticket.

## Verify
1. Have the user sign in to their PC with the temporary password and set a new one.
2. Confirm they reach the desktop.
3. Add a follow-up: `User confirmed successful login and password change.`
4. Solve the ticket with a short solution (what was done, no passwords), then close after the user confirms.

## Known issues
- **The account locks again right away:** something is still using the old password, like a mapped drive, a phone's email, or saved credentials. Check Credential Manager on the PC.
- **Repeated lockouts the user didn't cause:** stop and treat it as a **security incident**. Change the ticket type to Incident and escalate. Don't keep unlocking it.

## Escalation
- Admin, service, or executive accounts → escalate to the senior admin. Don't reset these from a phone request.
- You can't verify identity → escalate and inform the manager.
