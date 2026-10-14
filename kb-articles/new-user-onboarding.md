# New user onboarding: account, access, and workstation setup

**Category:** Onboarding & Offboarding
**Audience:** IT Service Desk technicians (target: IT Service Technicians group, not in the FAQ)
**Applies to:** new standard employees in `corp.local`. Contractors and admin accounts follow a separate approval process (see Escalation).
**Written from:** ticket #12 (Scenario 2), created with GLPI's "Save & add to the knowledge base" option on the solution

## Trigger
- A hiring manager submits an onboarding request with the new hire's name, title, department, start date, and the access they need.
- Requests from anyone other than the manager (or HR) need manager confirmation before you start.

## Before you start
1. Confirm the request comes from the new hire's **manager** or HR. If someone else sent it, confirm with the manager through a known channel.
2. Check that every required field is there: full name, title, department, start date, manager, and the access needed. If anything is missing, add a follow-up asking for it and set the ticket to **Pending**.
3. Never grant access the manager didn't request. "Same as Bob" requests need the exact groups listed, because copying someone else's access spreads extra permissions.

## Ticket
1. Type: **Request**. Category: **Onboarding & Offboarding**. Requester: **the manager**.
2. Assign it to yourself and add a task covering:
   - Create AD account
   - Add to groups
   - Assign workstation
   - Verify first login

## Create the AD account
1. On DC01, open **Active Directory Users and Computers** and go to the department OU (e.g. `corp.local → Departments → HR`).
2. Right-click → New → User. Fill in first/last name and the logon name per the naming convention.
3. Set a temporary password that meets policy, and tick **User must change password at next logon**.
4. Open the new user's Properties and fill in **Title, Department, Manager** (Organization tab) and **Telephone** (General tab). The phone number is required, because password-reset identity verification depends on it.

## Add to groups
1. Add the user to the department group plus anything the manager listed.
2. Do **not** add them to `GLPI-Techs` or any admin group without separate approval.

## Assign workstation
1. In GLPI → Assets → Computers, open the assigned PC and set **User** to the new hire.
2. This links the device to the user, so they can pick it when they open tickets.

## Give credentials to the user
- Give the temporary password to the **manager by phone** (or to the new hire in person on day one). Never send it by email or chat, and never put it in the ticket.

## Verify first login
1. The new hire signs in to Windows on their PC and sets a new password.
2. They then sign in to GLPI at `http://glpi.corp.local` with their AD credentials. Their GLPI account is created automatically from AD and given the **Self-Service** profile in the IT Service Desk entity. No manual setup in GLPI.

## Close out
1. Add a follow-up: `Account created, groups assigned, workstation assigned, first login verified.`
2. Solve the ticket and close it after the manager confirms.

## Known issues
- **GLPI login fails for the new user:** they haven't finished the password change at Windows sign-in yet, or the account is outside the part of AD that GLPI searches (LDAP BaseDN). Check both.
- **The user gets the wrong GLPI profile:** check their AD group membership. Authorization rules run at login, so fix the group and have them log out and back in.

## Escalation
- Admin rights, `GLPI-Techs` membership, or access outside the department → needs separate approval from IT management.
- Start date is under 24 hours away and information is missing → contact the manager directly.

**Related:** [Reset a user's AD password](reset-ad-password.md)
