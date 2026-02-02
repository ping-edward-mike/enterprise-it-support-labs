# Lab 3 – Active Directory OU, Users, Groups, and Delegation

## Overview
In this lab, we created and managed Active Directory (AD) Organizational Units (OUs), users, and security groups for a small enterprise scenario. The lab also demonstrated delegating administrative rights and setting up group-based file access, simulating real-world Service Desk and IT Support operations.

**Domain:** `ine.local`  
**Location:** Birmingham  
**Departments:** IT, Finance  

---

## OU Structure
```
ine.local (domain)
    ├── Birmingham (OU)
    │ ├── Computers (OU)
    │ │ ├── Desktops (OU)
    │ │ └── Laptops  (OU)
    │ ├── Groups    (OU)
    │ │ └── Security (OU)
    │ └── Users (OU)
    │ ├── IT-Users (OU)
      └── Finance-Users (OU)

```

**Notes:**
- Users and computers are separated to simplify management and policy application.
- Groups are stored in a dedicated OU to manage access control efficiently.
- Departments are represented through OUs and security groups to ensure clear role-based access.

![Created OUS under domain](/windows-server-labs/lab-3-ad-ou-gpo-user-management-basics/snippets/created-OUs-under-domain-ine-local.PNG)

---

## Users Created

| Name         | Username      | OU                   | Role                     |
|--------------|---------------|--------------------|-------------------------|
| Edward Mike  | edd.mike        | Users > IT          | IT Support (L1)         |
| John Doe     | john.doe         | Users > Finance     | Finance Staff           |

**Security Groups:**
- `IT-Support-L1` -> Edward Mike
- `Finance-Users` -> John Doe

![1 User under IT-Users OU](/windows-server-labs/lab-3-ad-ou-gpo-user-management-basics/snippets/create-user-1-under-IT.PNG)

![1 User under Finance-Users OU](/windows-server-labs/lab-3-ad-ou-gpo-user-management-basics/snippets/create-user-2-under-Finance.PNG)

---

## Lab Tasks

### Task 1 – Create Department Users
**Objective:** Create user accounts for the IT and Finance departments and verify that users can sign in to the domain.

**Steps Performed:**
1. Created Edward Mike in `Users > IT`.
2. Created John Doe in `Users > Finance`.
3. Added each user to their respective security group.
4. Verified that John Doe could sign in to Win11-01.

**Acceptance Criteria:**
- Users exist in the correct OUs.
- John Doe is able to log in successfully.



---

### Task 2 – Delegate Limited Administrative Rights
**Objective:** Allow the IT user to perform password resets and account unlocks without granting full administrative privileges.

**Steps Performed:**
1. Added Edward Mike to the `IT-Support-L1` group.
2. Delegated control on the `Users` OU to allow:
   - Password reset
   - Account unlock
3. Confirmed that other administrative actions remained restricted.

**Acceptance Criteria:**
- Edward Mike can reset passwords and unlock accounts.
- Edward Mike cannot create users, manage groups, or access Domain Admin privileges.

---

### Task 3 – Create a Restricted Finance File
**Objective:** Set up group-based file access so that only Finance users can access sensitive data.

**Steps Performed:**
1. Created a folder named `Finance-Data`.
2. Assigned NTFS permissions:
   - `Finance-Users` → Read/Modify
   - Removed `Everyone` and other unnecessary access.
3. Verified access:
   - John Doe could access the folder.
   - Edward Mike could not access the folder.

**Acceptance Criteria:**
- Finance users have access.
- Other users do not have access.
- Permissions are applied through groups, not individual users.
