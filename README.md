<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Open Source Ticketing System Walkthrough</h1>
This tutorial outlines the following for the open-source help desk ticketing system osTicket: 

- Installation
- Configuration
- Ticket Lifecycle Examples


---


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop/Azure Bastion
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 11</b>

<h2>List of Prerequisites</h2>

- Windows VM 
- Connection capability (RDP or Bastion)
- osTicket Installation Files
- Basic familiarity with Windows (UI, installing programs, file systems)

---

**<h1>Installation Steps</h1>**

### 1. Prepare the VM
- Log into the VM using Remote Desktop/Bastion  
- Download and extract: osTicket-Installation-Files.zip (LINK?)




---

### 2. Enable IIS with CGI
Enable this Windows feature:
Internet Information Services (IIS)
→ World Wide Web Services
→ Application Development Features
→ [✔] CGI


---

### 3. Install Required Components
From the installation folder, install:
- PHP Manager for IIS  
- IIS Rewrite Module  
- VC_redist.x86.exe  
- MySQL 5.5.62  
  - Typical Setup  
  - Standard Configuration  
  - Username: root  
  - Password: root
  - 
<img width="856" height="291" alt="full install list" src="https://github.com/user-attachments/assets/0e483f97-5686-4ce6-8749-b0a1fb0e1f8d" /> 
<!-- INSTALL LIST-->
---

### 4. Install PHP
Create folder:
C:\PHP
Extract into it:
php-7.3.8-nts-Win32-VC15-x86.zip



---

### 5. Configure IIS for PHP
- Open IIS Manager as Administrator  
- Open **PHP Manager**  
- Register PHP path:
C:\PHP\php-cgi.exe

- Restart IIS (Stop → Start)

---

### 6. Install osTicket
- Extract:
- osTicket-v1.15.8.zip

- Copy the `upload` folder to:


C:\inetpub\wwwroot

- Rename:


upload → osTicket

- Restart IIS

---

### 7. Open the Installer
Open browser and go to:


http://localhost/osTicket


You should see the osTicket setup page.

<img width="1417" height="967" alt="osTicket installer local host page " src="https://github.com/user-attachments/assets/661dde50-6b89-459c-9e40-5e4b5270bd2e" />
<!-- INSTALLER LOCAL HOST PAGE-->
---

### 8. Enable Required PHP Extensions
In IIS → PHP Manager → Enable or disable extensions:
- php_imap.dll  
- php_intl.dll  
- php_opcache.dll  

Refresh the browser after enabling.

---

### 9. Configure osTicket File
Rename:


C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php

To:


ost-config.php


Update permissions:
- Disable inheritance  
- Remove all existing permissions  
- Add:


Everyone → Full Control


---

### 10. Create Database
Open HeidiSQL:
- Login: root / root  
- Create database:


osTicket


---

### 11. Complete Installation in Browser
Enter database details:


Database: osTicket
Username: root
Password: root


Click:


Install Now


If successful, osTicket will complete setup.

<img width="1030" height="801" alt="osTicket install success" src="https://github.com/user-attachments/assets/6425f303-1b11-4bd9-a9b6-a67313ad9f42" />
<!-- OSTICKET INSTALL SUCCESS-->
---

## Access URLs

Staff / Admin Login:


http://localhost/osTicket/scp/login.php


End User Portal:


http://localhost/osTicket/


---
## Configuration (Admin & Workflow Setup)

This section demonstrates how osTicket can be configured to simulate a real help desk environment.

---

### 1. Configure Roles (Permissions)
Used to group permissions for agents.

Path:
Admin Panel → Agents → Roles

Example Role:
- Super Admin

---

### 2. Configure Departments
Used to control ticket visibility and separation of duties.

Path:
Admin Panel → Agents → Departments

yaml
Copy code

Example Department:
- SysAdmins
  
<img width="1205" height="452" alt="add new department" src="https://github.com/user-attachments/assets/97e8c1b0-c5fd-4109-8de1-3df4d70728a3" />

---

### 3. Configure Teams
Teams allow agents from different departments to collaborate.

Path:
Admin Panel → Agents → Teams

yaml
Copy code

Example Team:
- Online Banking
  
<img width="1197" height="681" alt="add new team" src="https://github.com/user-attachments/assets/24792068-e490-4453-b8f9-b638d6b88509" />

---

### 4. User Registration Settings
Control whether anyone can submit tickets.

Path:
Admin Panel → Settings → User Settings

yaml
Copy code

Configured as:
- Unchecked: Unregistered users can create tickets  
- Enabled: Registration required to create tickets  

This forces users to log in before submitting tickets.

---

### 5. Configure Agents (Workers)
Agents represent internal IT staff.

Path:
Admin Panel → Agents → Add New

<img width="1198" height="692" alt="add new agent" src="https://github.com/user-attachments/assets/97b87a52-0f02-4aa5-bf60-7bd73abdb0a2" />

---

Example Agents:
- Jane (Department: SysAdmins)  
- John (Department: Support)  

---

### 6. Configure Users (Customers)
Users represent employees or customers submitting tickets.

Path:
Agent Panel → Users → Add New


Example Users:
- Karen  
- Ken  

<img width="800" height="492" alt="add a user" src="https://github.com/user-attachments/assets/5314e6ab-eb1d-4b30-8296-17aee6944311" />

---

### 7. Configure SLA Plans
SLA plans define response expectations.

Path:
Admin Panel → Manage → SLA


Configured SLAs:
- Sev-A  
  - Grace Period: 1 hour  
  - Schedule: 24/7  
- Sev-B  
  - Grace Period: 4 hours  
  - Schedule: 24/7  
- Sev-C  
  - Grace Period: 8 hours  
  - Schedule: Business Hours  

<img width="1197" height="827" alt="SLA addition" src="https://github.com/user-attachments/assets/31a900a6-9e91-4b28-9176-f8b472649e4e" />

---

### 8. Configure Help Topics
Help Topics guide users when creating tickets.

Path:
Admin Panel → Manage → Help Topics

Configured Topics:
- Business Critical Outage  
- Personal Computer Issues  
- Equipment Request  
- Password Reset  
- Other  

<img width="1201" height="747" alt="add help topics" src="https://github.com/user-attachments/assets/079b2130-3a07-4847-96f1-688138d51658" />

## Ticket Lifecyle Examples (Simulation Lab)

This section focuses on using the system like a real help desk: creating tickets, triaging, assigning, escalating, and resolving issues.

Login URLs:
- Agent/Admin Login: http://localhost/osTicket/scp/login.php
- End User Portal: http://localhost/osTicket


In this lab:
- Tickets are created as end users  
- Tickets are reviewed and worked by agents  
- Properties such as Priority, SLA, Department, and Assignment are evaluated  

---

### Environment Cleanup
- Change **SysAdmins** to a Top-Level Department  
- Delete the **Maintenance** Department (do not archive; tickets are automatically routed here, so we need to remove this)  

---

### Ticket Scenario 1: Critical Outage

End User submits ticket:
> "Entire mobile/online banking system is down"
> 
<img width="1056" height="612" alt="open a new ticket" src="https://github.com/user-attachments/assets/bdef83af-a524-4168-92fc-8c8048a11376" />


<img width="1052" height="863" alt="open a new ticket 2" src="https://github.com/user-attachments/assets/42181ea9-def8-43f8-918e-b6c681eaca1f" />



As an Agent, observe:
- Priority  
- Department  
- SLA  
- Assigned To  

<img width="1197" height="642" alt="new ticket initial view" src="https://github.com/user-attachments/assets/c368f890-cc7f-426e-88e9-64374c7aaefd" />


Set ticket properties:
- SLA: Sev-A (1 hour, 24/7)  
- Department: Online Banking 


Complete ticket. 

<img width="802" height="312" alt="agent view once assigned" src="https://github.com/user-attachments/assets/bb5979fb-bd0c-45f4-bfa2-112de70fca71" />

---

### Ticket Scenario 2: Software Issue

End User submits ticket:
> "Accounting department needs Adobe upgrade, broken"

As Agent, observe:
- Priority  
- Department  
- SLA  
- Assigned To  

Set properties:
- SLA: Sev-B (4 hours, 24/7)  
- Department: Support  

Work ticket to completion.

---

### Ticket Scenario 3: Executive Hardware Issue

End User submits ticket:
> "CFO’s laptop will no longer turn on"

As Agent, observe:
- Priority  
- Department  
- SLA  
- Assigned To  

Set properties:
- SLA: Sev-B (4 hours, 24/7)  
- Department: Support  

Work ticket to completion.

---

### Escalation and Access Testing

- Set all tickets to Sev-A  
- Assign SysAdmins department last  
- Observe ticket becomes inaccessible  
- Switch to Admin Panel  
- Grant yourself View access to SysAdmins  
- Return to Agent Panel  
- Observe escalated ticket  
- Confirm that edits are restricted  

---

### Ticket Resolution
- Resolve all open tickets  
- Close tickets properly  

Note: In real environments, most ticketing systems (including osTicket) can send email notifications. Each update to a ticket typically sends an email to the user, and users can often reply directly via email to continue the conversation.

---

## Real-World Ticket Intake Notes

In real environments, tickets may come from:
- Web forms  
- Email  
- Phone calls  
- Chat systems (Slack, Teams, etc.)  
- Walk-ups / hallway conversations  

Even if you fix an issue on the spot, it is considered best practice to **still create a ticket** for the work performed. This ensures:
- Accurate metrics  
- Workload tracking  
- Accountability  
- Historical documentation  
- Better reporting for leadership  







