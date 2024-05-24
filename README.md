<h1>Active Directory Lab w/ VM</h1>
In this lab I'm going to very comprehensively document how I created an AD home lab environment using Oracle Virtual Box. Configuring and running this lab definitely helped develop my understanding of how AD and windows networking works, being able to run through it several times by memory and getting a good baseline for further experimentation.
<br />


<h2>Languages and Utilities Used</h2>

- <b>Oracle Virtual Box</b>
- <b>PowerShell</b>
  
<h2>Environments Used </h2>

- <b>Windows Server 2019</b>
- <b>Windows 11 Pro</b>

<h2>Program walk-through:</h2>

<p align="center">
<img src="https://imgur.com/Vv1IP1M.png" height="80%" width="80%" alt="Network Diagram"/>
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
Next service we need to install is RAS/NAT so our future Win11 client can access the internet through the DC while being nested in this private virtual network: Add roles and features>Next x3>:Remote Access>Next x3>Routing>Add Features>Next x3>Install: <br/>
<img src="https://imgur.com/agj2eVV.png" height="80%" width="80%" alt="Next service we need to install is RAS/NAT"/>
<br />
</p>

<p align="center">
Tools>Routing and Remote Access>DC(local)>Configure and Enable Routing and Remote Access>Next>NAT (typically have to redo this step tree to see the Network Interfaces for some reason)>select _INTERNET_>Finish: <br/>
<img src="https://imgur.com/EBpM2AE.png" height="80%" width="80%" alt="Now we can login using our admin account under MYDOMAIN"/>
<br />
</p>

<p align="center">
Next service is DHCP: Add roles and features>Next x3>DHCP server>Add Features>Next x3>Install. Tools>DHCP>dc.mydomain.com>IPv4>New Scope>172.16.0.100-200 for name>172.16.0.100, 172.16.0.200, length of mask is 24 = 255.255.255.0>Next>no exclusions for setup so Next>:8 days>Next>172.160.0.1 (DC's IP with NAT configured) and Add (important step, easily missed), Next x4>Finish>dc.mydomain.com>Authorize>IPv4/IPv6 is green which means DHCP is fully set up!: <br/>
<img src="https://imgur.com/5HdLgjl.png" height="80%" width="80%" alt="Next service is DHCP"/>
<br />
</p>

<p align="center">
To make a configuration that allows us to browse the internet from our DC (only in lab setting for ease of access, big no-no in production environments): Configure this local server>:"On" hypertext next to Internet Explorer Enhanced Security Config>Off and Off: <br/>
<img src="https://imgur.com/BaXAwz2.png" height="80%" width="80%" alt="To make a configuration that allows us to browse the internet"/>
<br />
</p>

<p align="center">
Creating 1000 users using a Powershell script sourced online (I'll learn powershell after Python at some point for some basic scripting and admin tools):Start>Windows PowerShell ISE>More>Run as admin>insert script>write "Set-ExecutionPolicy Unrestricted" to allow for script to run on server>Yes to All>write "cd:\users\a-zprater\desktop\AD_PS-master" to change the pulled directory from sys32 to our admin user's desktop where the files sit>Play: <br/>
<img src="https://imgur.com/nUYw17G.png" height="80%" width="80%" alt="Creating 1000 users"/>
<br />
</p>

<p align="center">
Time to create the Client1 VM hosted on Win11 Pro, using an internal NIC as our only network connection for this machine (run through setup same as Server 2019): <br/>
<img src="https://imgur.com/mfuQfeU.png" height="80%" width="80%" alt="After starting VM, running through custom install"/>
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
