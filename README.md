<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This guide covers the installation of the open-source help desk system osTicket, including server requirements, database setup, and configuration, using Azure resources and VMs.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Web Server: Apache, LiteSpeed, or IIS (with URL Rewrite module enabled)
- PHP Version: 8.1 - 8.2 (8.2 recommended)
- Database: MySQL 5.0 or newer
- MySQL Requirements:
  - One database with a valid user, password, and hostname
  - User must have FULL privileges on the database

<h2>Installation Steps</h2>
- In Azure Portal:

  - Creeate a virtual machine (Windows 10)
    
  - Get it's ip
    
  - Use Remote Desktop Protocol(RDP) to connect to Vm
<p>
 <img src="https://i.imgur.com/HYl6ZmN.png"/>
</p>

RDP
<p>
<img src="https://i.imgur.com/V6xOT8l.png"/>

</p>
<br />
Within the VM (osticket-vm), download the osTicket-Installation-Files.zip and unzip it onto your desktop. The folder should be called “osTicket-Installation-Files”
We will use the files in this folder to install osTicket and some of the dependencies.

https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD
<p>
<img src="https://i.imgur.com/HmMf6Yp.png" />
  
Install / Enable IIS in Windows WITH CGI
World Wide Web Services -> Application Development Features -> [X] CGI
<p>
<img src="https://i.imgur.com/kERWGk7.png" />

</p>
We should see that IIS is running:
<p>
<img src="https://i.imgur.com/MMwNA6o.png" />

</p>
## osTicket Installation Steps

### 1. Install Required Components  
From the **"osTicket-Installation-Files"** folder:  
- Install **PHP Manager for IIS** (`PHPManagerForIIS_V1.5.0.msi`)  
- Install **Rewrite Module** (`rewrite_amd64_en-US.msi`)  
- Create the directory `C:\PHP`  
- Unzip **PHP 7.3.8** (`php-7.3.8-nts-Win32-VC15-x86.zip`) into `C:\PHP`  
- Install **VC Redist** (`VC_redist.x86.exe`)  
- Install **MySQL 5.5.62** (`mysql-5.5.62-win32.msi`)  
  - Select **Typical Setup**  
  - Launch **Configuration Wizard** after installation  
  - Choose **Standard Configuration**  
  - Set **Username: root**, **Password: root**  

### 2. Configure IIS  
- Open **IIS as Administrator**  
- Register PHP in IIS:  
  - Open **PHP Manager** -> Set path to `C:\PHP\php-cgi.exe`  
- Reload IIS: **Stop and Start the server**  

### 3. Install osTicket  
From the **"osTicket-Installation-Files"** folder:  
- Unzip **osTicket v1.15.8** (`osTicket-v1.15.8.zip`)  
- Copy the **"upload"** folder to `C:\inetpub\wwwroot`  
- Rename **"upload"** to **"osTicket"**  
- Reload IIS: **Stop and Start the server**  

### 4. Verify Installation  
- In IIS, navigate to:  
  - **Sites** -> **Default** -> **osTicket**  
  - On the right, click **“Browse *:80”**  
- You should see the **"Congratulations!"** page 🎉  

<p>
<img src="https://i.imgur.com/70zx2LU.png" />
</p>

### 4. Enable Required PHP Extensions  
- Open **IIS** -> **Sites** -> **Default** -> **osTicket**  
- Double-click **PHP Manager**  
- Click **“Enable or disable an extension”**  
- Enable the following extensions:  
  - `php_imap.dll`  
  - `php_intl.dll`  
  - `php_opcache.dll`  
- Refresh the osTicket site in your browser and observe the changes  

### 5. Rename Configuration File  
- Rename `ost-sampleconfig.php` to `ost-config.php`:  
  ```text
  From: C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php  
  To:   C:\inetpub\wwwroot\osTicket\include\ost-config.php

### 6. Assign Permissions to `ost-config.php`  
- Disable **inheritance** -> **Remove All**  
- Set new permissions:  
  - **User:** Everyone  
  - **Permission:** Full Control  

### 7. Complete osTicket Setup in Browser  
- Click **Continue** in the setup page  
- Configure basic settings:  
  - **Helpdesk Name**  
  - **Default Email** (receives emails from customers)  

### 8. Install and Configure HeidiSQL  
From the **"osTicket-Installation-Files"** folder:  
- Install **HeidiSQL**  
- Open **HeidiSQL**  
- Create a new session with credentials:  
  - **Username:** root  
  - **Password:** root  
- Connect to the session  
- Create a new database named **osTicket**  

### 9. Finalize Database Setup in osTicket  
- In the osTicket browser setup page, enter:  
  - **MySQL Database:** osTicket  
  - **MySQL Username:** root  
  - **MySQL Password:** root  
- Click **"Install Now!"**  

### 10. Access osTicket Admin Panel  
- Open **IIS**  
- Navigate to the osTicket admin login page  


<p>
  <img src="https://i.imgur.com/aA0Kt4r.png" />
</p>

[CONTINUE TO NEXT SECTION](https://github.com/tech-tonio-ai/post-install-config)

  - And the User login page
<p>
  <img src="https://i.imgur.com/m1Ghe7j.png" />
</p>

<br />
