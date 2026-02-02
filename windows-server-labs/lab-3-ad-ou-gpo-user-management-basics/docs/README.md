# Lab 3 – Active Directory OU, Users, Groups, and Delegation

## Overview
In this lab, we **created and managed Active Directory (AD) Organizational Units (OUs), users, and security groups** for a small enterprise scenario. We also **delegated administrative rights**, simulating real-world Service Desk and IT Support operations.

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
- Security groups are stored in a dedicated OU to manage access control efficiently.  
- Departments are represented through OUs and security groups to ensure clear role-based access.

![Created OUs under domain](/windows-server-labs/lab-3-ad-ou-gpo-user-management-basics/snippets/created-OUs-under-domain-ine-local.PNG)

---

## Security Groups


**Security Groups:**  
- `IT-Support-L1` 
- `Finance-Users` 

![Security Group for IT-Support-L1](/windows-server-labs/lab-3-ad-ou-gpo-user-management-basics/snippets/Security-Group-IT-Support-Lv1.PNG)

![Security Group for Finance-Users](/windows-server-labs/lab-3-ad-ou-gpo-user-management-basics/snippets/Security-Group-Finance-USers.PNG)

---

## Lab Tasks

### Task 1 – Create Department Users
**Objective:** Created user accounts for the IT and Finance departments and verified that users could sign in to the domain.

| Name         | Username      | OU             | Role              |
|--------------|---------------|----------------|-----------------|
| Edward Mike  | edd.mike      | Users > IT-Users     | IT Support (L1)  |
| John Doe     | john.doe      | Users > Finance-Users | Finance Staff    |


**Steps Performed:**  
1. Created Edward Mike in `Users > IT-Users`.  
2. Created John Doe in `Users > Finance-Users`.  
3. Added each user to their respective security group.  

**Acceptance Criteria:**  
- Users exist in the correct OUs.  
- John Doe successfully signed in to the domain on Win11-01. 

![User under IT-Users OU](/windows-server-labs/lab-3-ad-ou-gpo-user-management-basics/snippets/create-user-1-under-IT.PNG)

![User under Finance-Users OU](/windows-server-labs/lab-3-ad-ou-gpo-user-management-basics/snippets/create-user-2-under-Finance.PNG)

![John signed in successfully to Win11-01](/windows-server-labs/lab-3-ad-ou-gpo-user-management-basics/snippets/john-signed-in-successsfuly-to-Win11-01.PNG)

## Users as Members of Groups

![Edward in IT-Support](/windows-server-labs/lab-3-ad-ou-gpo-user-management-basics/snippets/Edward-in-IT-Support-Lv1-Security-Group.PNG)

![John in Finance-Security](/windows-server-labs/lab-3-ad-ou-gpo-user-management-basics/snippets/John-in-Finance-Security-Group.PNG)

---

### Task 2 – Basic Delegation Of Administrative Rights
**Objective:** Delegated control to allow the IT user to **reset passwords and unlock accounts** without granting full administrative privileges.

**Steps Performed:**  
1. Added Edward Mike to the `IT-Support-L1` group.  
2. Delegated control on the `Users` OU to allow:  
   - Password reset  
   - Account unlock  
3. Confirmed that other administrative actions remained restricted.  

**Acceptance Criteria:**  
- Edward Mike could reset passwords and unlock accounts.  
- Edward Mike could **not** create users, manage groups, or access Domain Admin privileges.  

> **Note:** Delegation via groups ensures easier management, scalability, and auditability compared to assigning rights directly to individual users.

![John in Finance-Security](/windows-server-labs/lab-3-ad-ou-gpo-user-management-basics/snippets/Delegate-control-to-it-support-step-1.PNG)
![John in Finance-Security](/windows-server-labs/lab-3-ad-ou-gpo-user-management-basics/snippets/Delegate-control-to-it-support-step-2.PNG)
![John in Finance-Security](/windows-server-labs/lab-3-ad-ou-gpo-user-management-basics/snippets/Delegate-control-to-it-support-step-3.PNG)

### Verify Delegation

![Verify Delegation-Global-Level](/windows-server-labs/lab-3-ad-ou-gpo-user-management-basics/snippets/Verify-Reset-password-on-IT-support-lv-1.PNG)

![Verifiy Delegation-User-level](/windows-server-labs/lab-3-ad-ou-gpo-user-management-basics/snippets/Verify-Reset-password-on-IT-support-lv-1-edward-profile.PNG)

---

### Simulated John Doe Account Disable and Password Reset

- The John Doe account was intentionally disabled to simulate a common support scenario.
- Edward Mike, acting as IT Support (L1), logged into the domain controller to re-enable the account and reset the password using delegated permissions.

#### Verification Steps

- John Doe’s login attempt failed due to the disabled account.  
![Verify delegation – account disabled](/windows-server-labs/lab-3-ad-ou-gpo-user-management-basics/snippets/John-Account-disabled.jpg)

- Edward Mike successfully logged into the domain controller (`Win2k22-DC-01`).  
![Verify delegation – Edward login to DC](/windows-server-labs/lab-3-ad-ou-gpo-user-management-basics/snippets/edward-login-into-DC.PNG)

- The John Doe account was located and re-enabled (Account disabled checkbox unchecked).  
![Enable John Doe account](/windows-server-labs/lab-3-ad-ou-gpo-user-management-basics/snippets/find-john-account.PNG)

- John Doe’s password was reset by Edward Mike.  
![Password reset initiated](/windows-server-labs/lab-3-ad-ou-gpo-user-management-basics/snippets/john-psswd-reset.PNG)  
![Password reset completed](/windows-server-labs/lab-3-ad-ou-gpo-user-management-basics/snippets/passwd-changed-done.PNG)

- John Doe successfully logged in and was prompted to change his password at first logon.  
![Successful login after reset](/windows-server-labs/lab-3-ad-ou-gpo-user-management-basics/snippets/john-logginh-in-successful.jpg)


---

## Lab Summary / Reflection
This lab reinforced key Active Directory administration skills, including **OU design, user and group management, delegation of administrative rights**. By completing these tasks, we ensured that IT support staff could perform essential functions without exposing the domain to unnecessary risk, demonstrating best practices in enterprise AD management.

---

### Next Lab

Lab 4: Configure File and Print Services with Permissions and Shares
