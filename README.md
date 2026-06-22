# freeipa-user
freeipa-user-group-management-lab/

├── README.md
├── commands/
│   └── ipa_commands.sh
├── notes/
│   └── troubleshooting.md
└── screenshots/
    └── user-added-to-group.png

==================== README.md ====================

# FreeIPA User & Group Management Lab

## Overview

This project demonstrates managing users and groups using FreeIPA, including creating users, modifying user attributes, resetting passwords, and assigning users to groups through both CLI and web interface.

## Objective

Strengthen skills in centralized identity and access management by configuring a FreeIPA user and assigning appropriate group permissions.

## Technologies Used

- FreeIPA
- Linux (RHEL/CentOS)
- Kerberos Authentication
- SSSD
- Web UI (FreeIPA Interface)

## Setup Process

Authenticate to FreeIPA:

kinit admin

Verify authentication:

klist

Create User:

ipa user-add jborja \
  --first=Joy \
  --last=Borja \
  --shell=/bin/bash \
  --password

Verify User:

ipa user-show jborja

List Users:

ipa user-find

Add User to Group (CLI):

ipa group-add-member support --users=jborja

Verify Group Membership:

ipa group-show support

Check User on System (SSSD):

id jborja
getent passwd jborja

Reset User Password:

ipa passwd jborja

Alternative Password Change (User):

passwd
kpasswd

## Web UI Configuration

- Logged into FreeIPA web interface
- Located user `jborja`
- Navigated to group membership section
- Selected `support` group
- Added user to group
- Applied and verified changes

## Verification

Check user details:

ipa user-show jborja

Check group membership:

ipa group-show support

Confirm system recognition:

id jborja
getent passwd jborja

Check Kerberos ticket:

klist

## Outcome

User `jborja` successfully configured in FreeIPA, password set, and assigned to the `support` group with proper centralized access.

## Troubleshooting

- Kerberos authentication failure due to missing or incorrect credentials
- User not visible locally due to centralized identity (SSSD behavior)
- Password reset required proper authentication
- Group assignment required confirmation via CLI or UI

## Author

Farrell L. Shelton

==================== commands/ipa_commands.sh ====================

#!/bin/bash

# Authenticate to FreeIPA
kinit admin

# Verify Kerberos ticket
klist

# Create user
ipa user-add jborja --first=Joy --last=Borja --shell=/bin/bash --password

# Verify user
ipa user-show jborja

# List users
ipa user-find

# Add user to group
ipa group-add-member support --users=jborja

# Verify group
ipa group-show support

# Check user locally via SSSD
id jborja
getent passwd jborja

# Reset password (admin)
ipa passwd jborja

# User password change
passwd
kpasswd

==================== notes/troubleshooting.md ====================

# Troubleshooting Notes

## Issue: Kerberos authentication failed

Cause:

- Missing or incorrect credentials

Fix:

- Ran:
  kinit admin
- Verified with:
  klist

## Issue: User not visible on local system

Cause:

- FreeIPA uses centralized identity (not stored in /etc/passwd)

Fix:

- Verified using:
  id jborja
  getent passwd jborja

## Issue: Unable to run IPA commands

Cause:

- No Kerberos ticket

Fix:

- Re-authenticated using:
  kinit admin

## Issue: Incorrect password errors

Cause:

- Wrong admin credentials

Fix:

- Retrieved correct credentials and re-ran authentication

## Issue: Group not applied

Cause:

- User not properly added or changes not confirmed

Fix:

- Verified using:
  ipa group-show support

==================== GIT COMMANDS ====================

git init
git add .
git commit -m "FreeIPA user and group management lab with CLI and web UI configuration"
git branch -M main
git remote add origin <your-repo-link>
git push -u origin main
```

---

There. Clean, structured, and looks like you didn’t fight Kerberos for 30 minutes straight.
