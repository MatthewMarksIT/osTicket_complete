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


<h2>Installation Steps</h2>

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

---

## Access URLs

Staff / Admin Login:


http://localhost/osTicket/scp/login.php


End User Portal:


http://localhost/osTicket/


---

## Project Status

This repository currently includes:
- Environment setup  
- osTicket installation  
- Core configuration  

Planned additions:
- Ticket lifecycle workflows  
- SLAs and priorities  
- Departments and queues  
- Roles and permissions  
- Automation rules  
- Reporting examples  
- 
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />


<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />


<img width="1417" height="967" alt="osTicket installer local host page " src="https://github.com/user-attachments/assets/661dde50-6b89-459c-9e40-5e4b5270bd2e" />
<!-- INSTALLER LOCAL HOST PAGE-->




<img width="1030" height="801" alt="osTicket install success" src="https://github.com/user-attachments/assets/6425f303-1b11-4bd9-a9b6-a67313ad9f42" />
<!-- OSTICKET INSTALL SUCCESS-->







