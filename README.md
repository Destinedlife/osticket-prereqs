# osticket-prereqs
<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How To Install osTicket with Prerequisites](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Azure Subscription
- How to use Windows os
- Item 3
- Item 4
- Item 5

<h2>Installation Steps</h2>

![Step 1](https://github.com/user-attachments/assets/c48b91cf-fbd0-4eb0-b4ed-812929946c59)


<p>
Go to the Azure portal and go to virtual machines (VM). Create a new "Azure virtual machine". Under "Basics" create a new resource group and call it "osTicket". Then name the virtual machine "osticket-VM" and choose a region. Scroll down to "image" and choose "Windows 10 Pro, version 22H2 - x64 Gen2". For size pick something that has "2 vcpus" In this example I chose "Standard_D2s_v3 - 2 vcpus, 8 GiB memory". Then under "Administrator account" create a username and password. For this tutorial, you can use the following:
  
  usename: Labuser
  
  Password: osTicketPassword1!

*FOR LAB USE ONLY*

lastly, check the licensing agreement at the bottom and click "review + create" > create.
<br />

![Step 2](https://github.com/user-attachments/assets/86b6cae5-61c9-4beb-a712-4a2f629a06cf)

<p>
After the VM has been deployed we will remotely connect to it using Remote Desktop Connection. Go to the Virtual machine page in Azure and copy the public IP address. Open the Remote desktop connection and paste the IP address and the username created in the last step (you may have to click show more at the bottom of the panel). Then click connect > put in the password > click ok > click yes. Once logged in you can say no or yes to all the privacy settings then click accept ( it doesn't matter). Then inside the VM use this link to download osTicket and some dependencies: 
</p>

[Osticket installation files](https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD)

<p>
right click the the zip folder and extract all on to the desktop.
</p>
<br />

![Step 3](https://github.com/user-attachments/assets/4c40c437-c89c-4dea-9bab-69f038c8e06e)

<p>
Now, we will turn this virtual machine into a web server by enabling Internet Information of Services (IIS), this is a requirement for osTicket. In the search bar below search for the control panel. Inside the control panel click uninstall programs, then on the left click "Turn Windows features on or off". Next in the pop-up check "Internet Information Service". Click on the plus sign next to it to expand it, then expand World Wide Web services > application Development features > then check CGI. Hit ok and it will begin to install. Now if we go to the internet (edge) and go to 127.0.0.1 (the loopback server) it will take us to the webpage for the server (This would have taken us to an error page if the previous setting wasn't enabled).
</p>
<br />

![step 4](https://github.com/user-attachments/assets/558079f5-d7d8-434c-8aef-f861f8ba4329)

<p>
Now from inside the "osTicket-installation-Files" folder, we will install the PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi) ". Open the installer and hit next and I agree until it is installed. Then install Rewrite Module (rewrite_amd64_en-US.msi)
</p>
<br />

![step 5](https://github.com/user-attachments/assets/f8547578-77df-4331-b7b9-199880f928c0)

<p>
Now on the list on the left, click the drop-down menu next to "this pc". Next, right-click "windows (C:)" > open in a new window. Now, create a new folder here called "PHP". Next, back in the "osTicket-installation-Files" folder right right-click on php-7.3.8-nts-Win32-VC15-x86.zip extract all and browse to the the PhP folder we created.
</p>

![step 6](https://github.com/user-attachments/assets/523cb7eb-1855-4dd7-9dfe-806db946cddc)

<p>Next, install  VC_redist.x86.exe from the "osTicket-installation-Files" folder. Then install MySQL 5.5.62 (mysql-5.5.62-win32.msi), which is a database that osTicket will use to store all our data. When you get to the setup type page choose typical. Then on the complete page make sure "launch the MySQL wizard..." is checked and hit finished.
</p>
<br />

![step 7](https://github.com/user-attachments/assets/9b26ba78-5a44-442b-a253-0440f76713b1)

<p>
Now go click next > Standard Configuration > next > then for Modify Security Settings set the username and password to "root" (Only do this for this tutorial,*DO NOT DO THIS IN REAL LIFE*) I suggest you create a notepad on your desktop named Credentials with the username and password for later. then next > execute > finished
</p>
<br />

![step 8](https://github.com/user-attachments/assets/d943cf2d-9aa5-4db4-abf8-2c95a2723b5c)


<p>
Search for IIS in the taskbar and run it as an admin. Then go to PHP manager> Register new PHP Version. Click the three dots and browse to our PHP folder. Then double click on "php-cgi.exe" then click ok. Then back in IIS Manager under connections on the left choose osticket-vm and right click and hit stop then start the server.
</p>
<br />

![step 9](https://github.com/user-attachments/assets/a20cea77-ea1a-48d3-92be-376bc4d58546)

<p>
Back in the "osTicket-installtion-Files" folder, extract the osticket-v1.15.8 zipp. Then when it opens copy the upload folder to this location “c:\inetpub\wwwroot”. Rename the folder to "osTicket". Open the IIS manager and stop and start the server again.
</p>
<br />

![step 10](https://github.com/user-attachments/assets/827db316-6545-4d21-9118-09a609ef212c)

<p>
In IIS Manager, go to Sites > Default > osTicket. Then on the right click "Browse: 80 (HTTP)" under the Manage folder. The osTicket installer will open in your browser. Some of the extensions are not enabled. Go back to IIS Manager, go to Sites > Default > osTicket. Then 
 double click PHP manager > Enable or disable extension. Right-click and enable the following: 
 
  - Enable: php_imap.dll
  - Enable: php_intl.dll
  - Enable: php_opcache.dll

  Refresh the osTicket Site in your browser and see that extensions are now available 
</p>
<br />

![step 11](https://github.com/user-attachments/assets/4e02696a-dfb4-456d-9f9c-ab1f9f0da8aa)

<p>
Now we are to going to rename: ost-sampleconfig.php
  From: C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php
  To: C:\inetpub\wwwroot\osTicket\include\ost-config.php

Now we are going to assign permissions to allow osTicket to make changes to ost-config.php. Right-click on it and go to properties > security> advance. Then click disable all inheritance> remove all.
then click add > select a principle > type "Everyone" in box and hit ok (*DON"T DO THIS IN REAL LIFE*) > Check Full control > ok > apply > Ok.
<br />

![step 12](https://github.com/user-attachments/assets/5d8ceee0-bde1-4a37-9eae-bb38248c6fb1)

<p>
Now back to the broswer with osTicket installer click continue. Finsish settings:

  - name helpdask
  -Default email (can be fake for tutorial)
  - First name
  - last name
  - email address ( must be differnet from default email, can be fake for tutorial)
  - Username: Adminuser
  - password: Password1

*Save username and password in the creditials notepad for later*
<br />

![step 13](https://github.com/user-attachments/assets/0f696863-982a-450b-a2fa-c441979d125e)

<p>
Back in the "osTicket-installation-Files" folder open HeidiSQL_12.3.0.6589_Setup. Install it and Check once completed. Hedidi SQl opens click skip > new. The password is "root" then click open. On the left right-click "unnamed" > create > database. Name the database "osticket". Back to the browser fill out the database settings:

- mySQL database: osticket
- MySQL username: root
- Mysul passowrd: root
the click install.

YAY!!! hopefully you have successfully install osticket.
<br />


<p>
you can use this link to login as admin 

  http://localhost/osTicket/scp/login.php

and this link to login as a Enduser.

http://localhost/osTicket/ 

For of osTicket Post-install configuration follow this link:

[osTicket - Post-Install Configuration](https://github.com/Destinedlife/post-install-config)

If you want to take a break and save money in your Azure account
Go back to Azure portal > Virtual machine then select your VM and click stop. When you are ready to continue select Start on this page.
<br />
