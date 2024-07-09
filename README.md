<h2> Active Directory Home Lab UNDER CONSTRUCTION </h2>

<h2>Summary</h2>
I learned a great deal from doing this lab. I enjoyed seeing how active directory and the domain controller worked together to create a network. I first created a VM and installed Windows Server 2019 and used Server Manager which offers many different tools and services to implement small and large enterprise networks together. Creating and provisioning to deprovisioning active directory accounts to administering and securing the small enterprise network. As well as configuring dhcp and dns services alike. I also created NAT/RAT so that internal network could communicate over the network/internet. I used a power shell script located on github to create a list of users to be created inside Active Directory. vs making them one by one. I proceeded to create another VM with a client to connect to the domain controller. At the login screen any user with a user name and password can login with their credentials. Here is a quick overview on how I created this small enterprise environment.

<h2>Network Topology Diagram</h2>
<img src="https://i.imgur.com/CaRGqb0.png" height="80%" width="80%" alt="Network Topology Steps"/>

<h2>Technology Used</h2>

- <b>Virtual Box</b> 
- <b>Windows Server 2019.iso</b>
- <b>Windows 10 Enterprise 64 bit.iso</b>

<h2>Environments Used </h2>

- <b>VM's (Virtual Machines) </b> 

<h2> Walk-through:</h2>

<p align="center">
Step 1: Create a VM for Windows Server 2019 (Assuming we already know how to create a VM)
<br> <br>Open Virtual Box and to create a VM and select processor, storage and memory based on what your system can handle and select the .iso for the vm server.iso <br/>
<img src="https://i.imgur.com/HhhjlKw.png" height="80%" width="80%" alt="Step 1"/>
<br />
<br />
Step 2: Install Windows Server 2019 onto the virtual box/ enviroment  <br/>
Step 3: Configure Network Adapters and Rename PC
<img src="https://i.imgur.com/Kap41cH.png" height="80%" width="80%" alt="Config Adapt"/>
<br />
<br />
Right Click each network and click status > details and note down each of their ip addresses.  <br/>
<br><img src="https://i.imgur.com/S2RIKha.png" height="80%" width="80%" alt="Review IP"/>
<br />
<br />

We have two IP addresses here for each individual network:
<ol>
<li>10.0.2.15</li>
<li>169.254.138.229</li>
</ol>
Rename the network with an IP address similar to IP 1. to > “INTERNET” and rename the network with an IP address similar to IP 2. to > “INTERNAL”.

<br>b) We have to assign the IP address to internal adapter now.

Right click “INTERNAL” go to properties > double click on “Internet Protocol Version 4” > Click on “Use the following address”. Use the following values:

IP address : 172.16.0.1
<br>Subnet Mask: 255.255.255.0

Click on “Use the following DNS server addresses”. Use the following values:

Preferred DNS server: 127.0.0.1

This 127.0.0.1 is a loopback address which just means it communicates back to the local system.


<img src="https://i.imgur.com/P1IQs67.png" height="80%" width="80%" alt="IPV Properties"/>
<br />

Now we have to rename the PC.
<br><br>Inside your VM, right click start menu then click > System > click “Rename your PC”. <br/>
<br><img src="https://i.imgur.com/T7Fmuz9.png" height="80%" width="80%" alt="Rename PC"/>
<br />
<br />
Step 5: <b>Install Active Directory Domain Services</b>

<br>Open “Server Manager”.

Go to > “Add roles and features” > click on “next” until you reach the following page and then select “Active Directory Domain Services” > click on “Add Features”.  <br/>
<br><img src="https://i.imgur.com/edUAWXx.png" height="80%" width="80%" alt="ADD Features"/>
<br />
<br />
Continue pressing Next until you can click install and when finished click closed.
<br><br>Now you will see a yellow flag on the top right corner, click on it and proceed to click on “Promote this server to a domain controller”.  <br/>
<br><img src="https://i.imgur.com/npMf1SS.png" height="80%" width="80%" alt="Promote Server"/>

Now click on “Add a new forest” and name it “Joshsdomain.com” and click “Next”.
<br><br>Set your password and click Next.
<br><img src="https://i.imgur.com/o54KNGr.png" height="80%" width="80%" alt="Domain Controller Options"/>

Click Next and let the VM restart.

Step 6: Create Domain Admin Account

Go to Start >Windows Administrative Tools > Active Directory Users and Computers

Right click on mydomain.com > New > Organizational Unit. Name it “_ADMINS” and uncheck the box.

  <br/>
<img src="https://i.imgur.com/Wz5Dkf6.png" height="80%" width="80%" alt="Admins"/>

Now right click _ADMINS > New > User and fill it in the parameters.

Uncheck “User must change password at next logon”.
Check “Password never expires”.

Now right click your user > properties > member of > Add > type “Domain Admins” > Click “Check Names” and Apply.

Step 7: <b>Re-login with Domain Admin account</b>

Sign out of the account you are logged in as. On the login page click on “Other User” and use the credentials you made in the previous step.  <br/>
<img src="https://i.imgur.com/OmK1L5U.png" height="80%" width="80%" alt="Other User Login Screen"/>

Step 8: <b>Install and configure RAS/NAT</b>

Now we have to install and configure RAS/NAT , go to Server Manager > Add roles and features > click next until you reach “Select server roles” and click “Remote Access”.  <br/>
<img src="https://i.imgur.com/kcFYVZL.png" height="80%" width="80%" alt="ADD Roles and Features RAT"/>


Click next until you reach “Select role services”, tick “Routing” and add the feature , now continue through the rest of the installation.

Once its done we can close it.

Now from the top right corner of Server Manager , go to Tools > Routing and Remote Access.

Right click “DOMAINCONTROLLER” and click “Configure and Enable Routing and Remote Access”

Select “NAT”

Now click on “Use this public interface to connect to the Internet:” and select/highlight the “Internet” interface then click next and complete the configuration.

NOTE: If you are unable to select this option then close all the windows and try again.

Now we are done configuring the RAS/NAT and can continue to the next step.

Step 8: <b>Install and Configure DHCP Server</b>

In Server Manager go to “ Add roles and features”

Select “DHCP Server” and continue to install.  <br/>
<img src="https://i.imgur.com/3qJD2v0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/AeZkvFQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
