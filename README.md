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

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go to Azure portal and go to virtual machines (VM). Create a new "azure virtual machine". Under "Basics" create a new resource group and call it "osTicket". Then name the virtual machine "osticket-VM" and choose a region. Scroll down to image and choose "Windows 10 Pro, version 22H2 - x64 Gen2". For size choose a something that has "2 vcpus" in this example I chose "Standard_D2s_v3 - 2 vcpus, 8 GiB memory". Then under "Administrator account" create a user name and password. For this tutoriol you can use the following:
  
  usename: Labuser
  
  Password: osTicketPassword1!

*FOR LAB USE ONLY*

lastly check the licensing agreement at the bottom and click "review + create" > create.
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After the VM has been deployed we will remotely connect to it using Remote Desktop Connection. Go to the Virtual machine page in azure and copy the public Ip address. Open Remote desktop conection and paste the the IP address and the username created in the last step (you may have to click show more at the bottom of the panel). then click connect > put in the password > click ok > click yes. Once logged in you can say no or yes to all the privacy settings then click accept ( it doesn't really matter). Then inside the VM use this link to download osTicket and some dependencies: 
</p>

[Osticket installation files](https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD)

<p>
right click the the zip folder and extract all on to the desktop.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now we will turn this virtual machine in to a webserver by enabling Internet Information of services (IIS), this is a requirement for osTicket. In the search bar below serach for control panel. Inside control panel click uninstall programs, then on the left click "Turn windows features on or off". Next in the pop up check "Internet Information Service". Click on the plus sign next to it to expand it, then expand World Wide Web services > application Developemnt features > then check CGI. Hit ok and it will begin to install. now if we go to internet (edge) and go to 127.0.0.1 (the loop back server) it will takes us to the webpage for the server (This would have taken us to an error page if the previous setting wasn't enabled).
</p>
<br />


<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now from inside "osTicket-installtion-Files" folder we will install the PHP Manger for IIS (PHPManagerForIIS_V1.5.0.msi) ". Open the installer and hit next and I agree until its is installed. then install Rewrite Module (rewrite_amd64_en-US.msi)
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now on the list on the left click the drop down menu next "this pc". next right click "windows (C:)" > open in new window. Now create a new folder here called "PHP". Next back in the "osTicket-installtion-Files" folder right click on php-7.3.8-nts-Win32-VC15-x86.zip an extract all and browse to the the PhP folder we created.
</p>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next install  VC_redist.x86.exe from "osTicket-installtion-Files" folder. Then install MySQL 5.5.62 (mysql-5.5.62-win32.msi), which is database that osTicket will use to store all our data. When you get to the setup type page choose typical. Then when get the complete page make sure "launch the mysqul wizard..." is checked and hit finsihed.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now go click next > Standard Configuration > next > then for Modify Secruity Settings set the username and password to "root" (Only do this for this tutorial,*DO NOT DO THIS IN REAL LIFE*) I suggest you create a notepad on your desktop named Creditials with the username and password for later. then next > excute > finsihed
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
search for IIS in the task bar and run it as an admin. then got to PHP manger > Register new PHP Version. The clcik the three dots and browse to our PHP folder. then double click on "php-cgi.exe" then click ok. then back in IIS Manager under connections on the left choose osticket-vm and right click and hit stop then start the server.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
back in the "osTicket-installtion-Files" folder extract the osticket-v1.15.8 zipp. Then when opens copy the upload folder to this location “c:\inetpub\wwwroot”. Rename thw folder to "osTicket". Open IIS manager and stop and start the server again.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In IIS Manager, go to Sites > Default > osTicket. Then on the right click "Browse: 80 (http)" under Manage folder. the osTicket installer will open in your broweser. Some of the extensions are not enabled. go back to IIS Manager, go to Sites > Default > osTicket. then 
 double click PHP manager > Enable or diaable extension. Right click and anable the following: 
 
  - Enable: php_imap.dll
  - Enable: php_intl.dll
  - Enable: php_opcache.dll

  refresh the osTicket Site in your browser and see that extenions are 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now we are to going to rename: ost-sampleconfig.php
  From: C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php
  To: C:\inetpub\wwwroot\osTicket\include\ost-config.php

Now we are going to assgin permissions to allow osTicket to make changes to ost-config.php. Right click on it and go to properties > sercuity > advance. then click disable all inheritence > revmove all.
then click add > select a principle > type "Everyone" in box and hit ok (*DON"T DO THIS IN REAL LIFE*) > Check Full control > ok > apply > Ok.
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
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

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
back in the "osTicket-installtion-Files" folder open HeidiSQL_12.3.0.6589_Setup. install it and Check once completed. Hedidi SQl opens click skip > new. The password is "root" then click open. on the left right click "unamed" > create > database. Nmae the database "osticket". Back to the browser fill out the data basebase settings

- mySQL database: osticket
- MySQL username: root
- Mysul passowrd: root
the click install.

YAY!!! hopefully you have successfully install osticket.
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
you can use this links to login as admin 

  http://localhost/osTicket/scp/login.php

and this link to login as a Enduser.

http://localhost/osTicket/ 

<br />
