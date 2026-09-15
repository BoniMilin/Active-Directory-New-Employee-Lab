# Active Directory New Employee & Troubleshoot Lab

## Overview
This lab simulates a common IT Support/IT Engineer task involving the onboarding of a new employee into an Active Directory environment.

The objective was to create a user account, configure group membership, apply Group Policy, test authentication from a domain-joined workstation and 
troubleshoot a locked user account.

This lab was completed as part of my refresher for IT Support/ IT engineer roles, feel free to use this lab.

---


## Scenario

A new employee named **Sarah Murphy** has joined the Event Operations department.

The IT team has been asked to:

* Create her Active Directory account
* Place the account in the correct Organizational Unit
* Add her to the Event Operations security group
* Ensure the correct Group Policy applies
* Allow her to authenticate from a domain workstation
* Troubleshoot her account if she becomes locked out

---

## Lab Environment

### Domain Controller

* Windows Server
* Active Directory Domain Services
* DNS
* Group Policy Management

### Client

* Windows 10/11
* Joined to the Active Directory domain

### Tools Used

* Active Directory Users and Computers
* Group Policy Management
* Command Prompt
* `gpupdate`
* `gpresult`

---

# Part 1 - Creating the OU Structure

I created an Organizational Unit structure to separate users, computers, and groups.

Example structure:

```text
MagicPark
│
├── Users
│   └── Event Operations
│
├── Computers
│
└── Groups
```

Using OUs makes it easier to manage users, computers, permissions, and Group Policies within a domain environment.

### Screenshot

c:\Users\bonib\OneDrive\Desktop\GitHub\Active Directory Labs\Active-Directory-NewStarter-Lab\screenshots\01-ou-structure.png
---

# Part 2 – Creating the User

I created a new Active Directory user:

```text
Name: Sarah Murphy
Username: smurphy
Department: Event Operations
```

I configured the account so the user would be required to change their temporary password when logging in for the first time.

This is a common security practice during employee onboarding.

### Screenshot

C:\Users\bonib\OneDrive\Desktop\GitHub\Active Directory Labs\Active-Directory-NewStarter-Lab\screenshots\02-user-creation.png

---

# Part 3 – Creating a Security Group

I created a security group:

```text
GG_EventOperations
```

Sarah's account was then added to this group.

Using security groups instead of assigning permissions directly to individual users makes access easier to manage and scale.

For example:

```text
User
 ↓
Security Group
 ↓
Resource Permission
```

Instead of:

```text
User
 ↓
Resource Permission
```

### Screenshot

c:\Users\bonib\OneDrive\Desktop\GitHub\Active Directory Labs\Active-Directory-NewStarter-Lab\screenshots\03-security-group-creation.png

Active-Directory-NewStarter-Lab\screenshots\03-security-group-creation.png

---

# Part 4 – Testing the Domain Workstation

I confirmed that the Windows client was joined to the domain and tested logging in using:

```text
BONISDOMAIN\smurphy
```

The login was successful and confirmed that the client could communicate with the Domain Controller.

---

# Part 5 – Configuring Group Policy

I created a Group Policy Object for the Event Operations users.

Policy Name:

```text
Event Operations User Policy
```

The policy was linked to the relevant OU.

After configuring the GPO, I updated Group Policy on the client using:

```cmd
gpupdate /force
```

I then verified which policies were being applied using:

```cmd
gpresult /r
```

### Screenshot

```text
screenshots/03-security-group-creation.png
screenshots/12-gpresult.png
```

---

# Part 6 – Simulating an Account Lockout

To simulate a real support ticket, I intentionally entered the incorrect password multiple times.

The user then received a login problem.

Example ticket:

```text
User: Sarah Murphy
Issue: Unable to log into workstation.

User reports that their password is not being accepted.
```

---

# Troubleshooting Process

Instead of immediately resetting the password, I followed a structured troubleshooting process.

### Step 1 – Confirm the user

Verified that the username was:

```text
smurphy
```

### Step 2 – Confirm connectivity

Confirmed that the workstation could communicate with the domain.

### Step 3 – Check the AD account

Opened Active Directory Users and Computers and inspected the account.

The account was found to be locked.

### Step 4 – Unlock the account

I unlocked the user's Active Directory account.

### Step 5 – Test authentication

The user attempted to log in again and authentication was successful.

---

# Ticket Resolution Notes

```text
User: Sarah Murphy

Issue:
Unable to authenticate to domain workstation.

Investigation:
- Confirmed username.
- Checked workstation/domain connectivity.
- Checked Active Directory account.
- Account was locked following multiple failed login attempts.

Resolution:
- Unlocked account in Active Directory.
- Confirmed account was enabled.
- Verified security group membership.
- User successfully authenticated.
- Verified Group Policy application.

Status:
Resolved.
```

---

# Commands Used

### Force Group Policy Update

```cmd
gpupdate /force
```

### View Applied Group Policies

```cmd
gpresult /r
```

### Check Domain Information

```cmd
whoami
```

```cmd
whoami /groups
```

```cmd
systeminfo
```

```cmd
ipconfig /all
```

---

# What I Learned

This lab helped reinforce my understanding of:

* Active Directory user management
* Organizational Units
* User onboarding
* Security groups
* Group Policy
* Domain authentication
* Account lockouts
* Password troubleshooting
* Structured IT troubleshooting
* IT ticket documentation

One of the key lessons from this lab was that account access should be managed using groups where possible instead of assigning permissions directly to individual users it not only saves time but it is more secure.

I also practised verifying Group Policy using tools such as `gpresult` rather than assuming that a GPO had applied successfully.

---

# Skills Demonstrated

* Active Directory Domain Services
* Active Directory Users and Computers
* Group Policy
* Windows Server
* Windows Client Administration
* User Account Management
* Security Groups
* Troubleshooting
* IT Support
* Technical Documentation

---

# Future Improvements

Future versions of this lab could include:

* Shared folder permissions
* NTFS permissions
* Network drive mapping
* Password policies
* Account lockout policies
* PowerShell user creation
* Automated onboarding
* Multiple departments
* Printer deployment using Group Policy
