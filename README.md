<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />


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

From the “osTicket-Installation-Files” folder
  -install PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi)

From the “osTicket-Installation-Files” folder
  - install the Rewrite Module (rewrite_amd64_en-US.msi)

Create the directory C:\PHP

From the “osTicket-Installation-Files” folder
  - unzip PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) into the “C:\PHP” folder

From the “osTicket-Installation-Files” folder
  - install VC_redist.x86.exe.

From the “osTicket-Installation-Files” folder
  - install MySQL 5.5.62 (mysql-5.5.62-win32.msi)
Typical Setup ->
  - Launch Configuration Wizard (after install) ->
Standard Configuration ->
  - Username: root
  - Password: root

Open IIS as an Admin

Register PHP from within IIS (PHP Manager ->
  - C:\PHP\php-cgi.exe)

Reload IIS (Open IIS, Stop and Start the server)

Install osTicket v1.15.8
From the “osTicket-Installation-Files” folder,
  - unzip “osTicket-v1.15.8.zip” and copy the “upload” folder into “c:\inetpub\wwwroot”
  - Within “c:\inetpub\wwwroot”, Rename “upload” to “osTicket”

Reload IIS (Open IIS, Stop and Start the server)

Go to sites -> Default -> osTicket
On the right, click “Browse *:80”

Note that some extensions are not enabled
  - Go back to IIS, sites -> Default -> osTicket
  - Double-click PHP Manager
  - Click “Enable or disable an extension”
  - Enable: php_imap.dll
  - Enable: php_intl.dll
  - Enable: php_opcache.dll
  - Refresh the osTicket site in your browser, observe the changes

Rename: ost-config.php
  - From: C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php
  - To: C:\inetpub\wwwroot\osTicket\include\ost-config.php

- Assign Permissions: ost-config.php
- Disable inheritance -> Remove All
- New Permissions -> Everyone -> All

-  Continue Setting up osTicket in the browser (click Continue)
-  Name Helpdesk
-  Default email (receives email from customers)

From the “osTicket-Installation-Files” folder, install HeidiSQL.
- Open Heidi SQL
- Create a new session, root/root
- Connect to the session
- Create a database called “osTicket”

Continue Setting up osTicket in the browser
- MySQL Database: osTicket
- MySQL Username: root
- MySQL Password: root
- Click “Install Now!”

<br />
