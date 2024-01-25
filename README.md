<h1>Create a Virtual Machine and Deploy a Web Server in Azure</h1>

<h2>Description</h2>
In this Guided Project, you will create a Virtual Machine in Azure to deploy a web server, specifically a Nextcloud server. Instead of using just the presets, you will explore how the basic architecture of Azure works, by creating a Virtual Machine, connecting it to a subnet, protected by inbound and outbound rules thanks to Network Security Groups, in a Virtual Network. You'll also learn how to use Bastion to connect to the machine via SSH, without exposing an external port to the Internet, and then installing a simple Nextcloud server and make the Virtual Machine available to you by opening a public IP and a DNS label.Note: before taking this Guided Project, if you don't have an Azure subscription yet, please create an Azure Free Trial beforehand at https://portal.azure.com. Note: This course works best for learners who are based in the North America region. We’re currently working on providing the same experience in other regions.
<br />

<h2>Project Tasks</h2>

1) Create a Resource Group
2) Create a Virtual Network and a subnet
3) Protect a subnet using a Network Security Group
4) Deploy Bastion to connect to a Virtual Machine
5) Create an Ubuntu Server Virtual Machine
6) Install Nextcloud by connecting via SSH using Bastion
7) Publish an IP
8) Create a DNS label

<h2>Azure Project Architecture</h2>
<img src="https://i.imgur.com/wGSQbAG.png">

<h2>Pre Project Set-UP</h2>
 - Sign up for a free Azure Account or use an exsisting account <br/>
 - Login to the Azure Portal
 <br />
 <br />
 <p align="center">
 Login to portal.azure.com: <br/>
 [<img src="https://i.imgur.com/TUzFP8L.png"/>][login]
 [login]: https://portal.azure.com

<h2>Program walk-through:</h2>

<h3>1) Create a Resource Group</h3>

<p align="center">
Create a Resource Group: <br/>
<img src=""/>
<br />
<br />
Select the disk:  <br/>
<img src=""/>
<br />
<br />
Enter the number of passes: <br/>


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
