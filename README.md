<h2> Active Directory Home Lab</h2>

<h2>Summary</h2>
I learned a great deal from doing this lab. I enjoyed seeing how active directory and the domain controller worked together to create a network. I first created a VM and installed Windows Server 2019 and used Server Manager which offers many different tools and services to implement small and large enterprise networks together. Creating and provisioning to deprovisioning active directory accounts to administering and securing the small enterprise network. As well as configuring dhcp and dns services alike. I also created NAT/RAT so that internal network could communicate over the network/internet. I used a power shell script located on github to create a list of users to be created inside Active Directory. vs making them one by one. I proceeded to create another VM with a client to connect to the domain controller. At the login screen any user with a user name and password can login with their credentials. Here is a quick overview on how I created this small enterprise environment.



<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Diskpart</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)

<h2>Program walk-through:</h2>

<p align="center">
Launch the utility: <br/>
<img src="https://imgur.com/66ef7ae5-bc33-4201-9f41-dfef0282e03e" height="80%" width="80%" alt="Network Topology Steps"/>
<br />
<br />
Select the disk:  <br/>
<img src="https://i.imgur.com/tcTyMUE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Enter the number of passes: <br/>
<img src="https://i.imgur.com/nCIbXbg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Confirm your selection:  <br/>
<img src="https://i.imgur.com/cdFHBiU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Wait for process to complete (may take some time):  <br/>
<img src="https://i.imgur.com/JL945Ga.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Sanitization complete:  <br/>
<img src="https://i.imgur.com/K71yaM2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
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
