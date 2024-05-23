<h1>Active Directory Lab w/ VM</h1>

 ### [YouTube Demonstration](https://youtu.be/)

<h2>Description</h2>
In this lab I'm going to very briefly document how I created an AD home lab Environment using Oracle Virtual Box. Configuring and running this lab definitely helped develop my understanding of how AD and windows networking works, being able to run through it several times by memory and getting a good baseline for further experimentation.
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
<img src="https://imgur.com/rFKla5h.png" height="80%" width="80%" alt="Creating a network adapter for the internal network"/>
<br />
</p>

<p align="center">
After starting VM, running through custom install: <br/>
<img src="https://imgur.com/dgY2dt8.png" height="80%" width="80%" alt="Creating a network adapter for the internal network"/>
<br />
</p>

<p align="center">
Figuring out which connection is the VM intranet and external internet (external has proper IP addressing from my router): <br/>
<img src="https://imgur.com/zjQM3R9.png" height="80%" width="80%" alt="Creating a network adapter for the internal network"/>
<br />
</p>

<p align="center">
Figuring out which NIC is which (external internet has IP addressing from my router, whereas internal cannot find DHCP yet which means its assigned an autoconfig IP: <br/>
<img src="https://imgur.com/zjQM3R9.png" height="80%" width="80%" alt="Creating a network adapter for the internal network"/>
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
