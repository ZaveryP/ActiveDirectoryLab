<h1>Active Directory Lab w/ VM</h1>

 ### [YouTube Demonstration](https://youtu.be/)

<h2>Description</h2>
In this lab I'm going to very comprehensively document how I created an AD home lab Environment using Oracle Virtual Box. Configuring and running this lab definitely helped develop my understanding of how AD and windows networking works, being able to run through it several times by memory and getting a good baseline for further experimentation.
<br />


<h2>Languages and Utilities Used</h2>

- <b>Oracle Virtual Box</b>
- <b>PowerShell</b>
  
<h2>Environments Used </h2>

- <b>Windows Server 2019</b>
- <b>Windows 11 Pro</b>

<h2>Program walk-through:</h2>

<p align="center">
First VM is the Domain Controller using Windows Server 2019: <br/>
<img src="https://imgur.com/UjRO69O.png" height="80%" width="80%" alt="First VM is the Domain Controller using Windows Server 2019"/>
<br />
</p>

<p align="center">
Creating a 2nd NIC for the VM intranet, 1st is real internet: <br/>
<img src="https://imgur.com/rFKla5h.png" height="80%" width="80%" alt="Creating a 2nd NIC for the VM intranet, 1st is real internet"/>
<br />
</p>

<p align="center">
After starting VM, running through custom install: <br/>
<img src="https://imgur.com/dgY2dt8.png" height="80%" width="80%" alt="After starting VM, running through custom install"/>
<br />
</p>

<p align="center">
Figuring out which NIC is which (external internet has IP addressing from my router, whereas internal cannot find DHCP yet which means its assigned an autoconfig IP) and renaming properly: <br/>
<img src="https://imgur.com/zjQM3R9.png" height="80%" width="80%" alt="Figuring out which NIC is which (external internet has IP addressing from my router, whereas internal cannot find DHCP yet which means its assigned an autoconfig IP) and renaming properly"/>
<br />
</p>

<p align="center">
Assigning static IP to internal NIC (no default gateway because DC serves *as* the gateway, same for DNS so you use the same IP address or the loopback address of 127.0.0.1. Interesting!): <br/>
<img src="https://imgur.com/CGAdn8E.png" height="80%" width="80%" alt="Assigning static IP to internal NIC (no default gateway because DC serves *as* the gateway, same for DNS so you use the same IP address or the loopback address of 127.0.0.1. Interesting!"/>
<br />
</p>

<p align="center">
First service to install is Active Directory through: "Add roles and features">Next x3>Highlighting Active Directory Domain Services and Add Features>Next x3>Install: <br/>
<img src="https://imgur.com/rHZLzeX.png" height="80%" width="80%" alt="First service to install is Active Directory"/>
<br />
</p>

<p align="center">
After installing AD you have to promote the server to a domain, simple domain name of 'mydomain.com' and Next x4>Install (all passwords in lab are Password1), and after signing out MYDOMAIN is created!: <br/>
<img src="https://imgur.com/waizNij.png" height="80%" width="80%" alt="After installing AD you have to promote the server to a domain"/>
<br />
</p>

<p align="center">
Creating dedicated domain admin account: Start>Windows Admin Tools>AD Users and Computers>mydomain.com>New>Organizational Unit (basically a folder in AD)>Naming the OU _ADMINS then Create new>User, logon name being a-zprater to signify an admin account, then Properties on the new user account>Member Of>Add>Domain Admins, thus creating the admin account: <br/>
<img src="https://imgur.com/vztYVv3.png" height="80%" width="80%" alt="Creating dedicated domain admin account"/>
<br />
</p>

<p align="center">
Now we can login using our admin account under MYDOMAIN: <br/>
<img src="https://imgur.com/4oRW9Wi.png" height="80%" width="80%" alt="Now we can login using our admin account under MYDOMAIN"/>
<br />
</p>

<p align="center">
Next service we need to install is RAS/NAT so our future Win11 client can access the internet through the DC while being nested in this private virtual network: Add roles and features>Next x3>:Remote Access>Next x3>Routing>Add Features>Next x3>Install <br/>
<img src="https://imgur.com/agj2eVV.png" height="80%" width="80%" alt="Now we can login using our admin account under MYDOMAIN"/>
<br />
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
