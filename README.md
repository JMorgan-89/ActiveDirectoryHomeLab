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


Now after that is complete go to Tools > DHCP > Right click IPv4 > New Scope.

Now copy the following parameters, leave blank or click next if not specified

172.16.0.100–200 *(range of ip address to be used by clients)  <br/>
<img src="https://i.imgur.com/VgvQuum.png" height="80%" width="80%" alt="IP Scope"/>

Click Next  <br/>
<img src="https://i.imgur.com/yyrHAQU.png" height="80%" width="80%" alt="IP Address Ramge"/>

The next page will show default gateway ip address Enter “172.16.0.1”

After you are done with the scope wizard, right-click your domain server > click refresh and then right click IPv4 and click refresh. Your IPv4 should turn green.  <br/>
<img src="https://i.imgur.com/ExXHjm5.png" height="80%" width="80%" alt="Refresh"/>

Step 9: <b>Enable Browsing and Download PowerShell Scripts</b>

Go to Server Manager > Configure this local server > Turn “IE Enhanced Security Configuration” Off.

b) Now we will download the PowerShell script, inside the domain controller (VM) go to https://github.com/joshmadakor1/AD_PS/archive/master.zip and download the file. * script is not my own but on GitHub credit: Josh Makador

Extract the file then open names.txt and add your name to the top of the file.

Click on Start > Windows PowerShell >Right-click Windows PowerShell ISE > More > Run as administrator.

Now go to File > Open and then open the script we downloaded named “1_CREATE_USERS”

Enter the following command:

Set-ExecutionPolicy Unrestricted

Click “Yes to all”  <br/>
<img src="https://i.imgur.com/d84UThj.png" height="80%" width="80%" alt="PS Script"/>

<b>Script Explanation:</b>

All the users will use the password = “Password1” and then all names from <i>names.txt</i> will be stored in USER_FIRST_LAST_LIST using Get-content .  <br/>
<img src="https://i.imgur.com/RasisCs.png" height="80%" width="80%" alt="Script Breakdown"/>

Now we will encrypt the plaintext password using line 6 and then line 7 automates the step in creating an organizational unit and disabling “protect container from accidental deletion”.  <br/>
<img src="https://i.imgur.com/bokTtxG.png" height="80%" width="80%" alt="Script2"/>

Lines 15 to 24 is a loop which will run for each individual user in the list.  <br/>
<img src="https://i.imgur.com/TGEozlD.png" height="80%" width="80%" alt="Script3"/>

Lines 10 and 11 splits the entire name into two sections called “first” and “last”. Line 12 creates a variable named “username” and concatenates the first character of the first name with entire last name.

For e.g. — the name Dwayne Plumb will become dplumb.

Line 13 will print the text in between the quotations with specific colors.

Lines 15–23 will automate the process to create a new user in active directory which we have done previously by using the GUI.

Now in PowerShell using the cd command , navigate to the directory of your script and then run the script > click “run once”.

Go to Active Directory Users and Computers and Under “Users” you should see all the users that the script created.  <br/>
<img src="https://i.imgur.com/BHa1BNU.png" height="80%" width="80%" alt="AD Users"/>

Step 10: <b>Install Windows 10 Enterprise VM</b>

Minimize the domain controller and go back to your original machine go to VirtualBox > New and set the following parameters:

If unspecified the continue with default values. <br/>
<img src="https://i.imgur.com/qCLKgsl.png" height="80%" width="80%" alt="WIN 10 VM"/>

Go to System > Processor.
If you have the capacity then increase the amount of cores used.

Go to Network > Adapter 1 and set the following parameters:

Now we are done with configuring the settings , Double click the VM to start it.

Click on the browse icon and select the Windows 10 ISO file.

Highlight your Windows 10 ISO and click Choose > Start.

Now continue with the Windows 10 operating system setup/installation.

Select “Custom Installation”

Continue the installation process by clicking next.

When prompted click on “Domain join” and then create your credentials.

Disable all privacy setting options and click accept.

Once your operating system is done installing and you have access to your system, we need to check whether the internet is working.

Go to Start > CMD and type the following command:

Ipconfig to see stats of the networking configuration. Ipv4 and default gateway should already be specified.

Now let’s change hostname and connect to the domain.  <br/>
<img src="https://i.imgur.com/hGMgZD0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

After you click OK it will prompt you to login, use the domain admin credentials you created in Step 6a and then allow it to restart now.

Go to back to the Domain Controller > Server Manager > Tools > DHCP > IPv4 > Scope > Address Leases and check whether your client lease is showing up.

Go to Active Directory Users and Computers > Joshsdomain.com > Computers  <br/>
<img src="https://i.imgur.com/u3suRBQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

You should be able to see your client computer.

Go back to your client machine/Windows 10 machine and log in with the “Other User” option. Use the credentials you created from the PowerShell script with default password as “Password1”.

For instance one of the name is “Dwayne Plumb” so at the login screen for username would be dplumb and the password would be Password1.

<li>Lab purposes Password1 was set to make things easier but in real-time complex passwords are a necessity to security.</li>
Once successful of logging in user go to cmd prompt and type whoami  <br/>
<img src="https://i.imgur.com/6Nyzjlg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<b>Conclusion:</b> We are now complete with our network and have created a mini-corporate environment with all the users in the PowerShell script list as users who can log in from their machine into the corporation domain and connect to the network.

It is like how a university or school lab is set up with each student having their own set of credentials and the ability to connect to the domain.  <br/>

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
