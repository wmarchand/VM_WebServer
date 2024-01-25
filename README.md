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

<h2>Pre-Project Set-Up</h2>
 - Sign up for a free Azure Account or use an exsisting account <br/>
 - Login to the Azure Portal
 <br />
 <br />
 <p align="center">
 Login to portal.azure.com: <br/>
 <img src="https://i.imgur.com/TUzFP8L.png"/>

<h2>Program walk-through:</h2>

<h3> 1) Create a Resource Group</h3>

<br />
<p align="center">
There are multiple ways to get to the start of creating a Resource Group. For this lab, I clicked on the Resource Group button on the home page of the Azure Portal. <br/>
<img src="https://i.imgur.com/a26tkVw.png"/>
<br />
<br />
Click the Create button in the top left corner of the Resource Group page.  <br/>
<img src="https://i.imgur.com/SAoaUFU.png"/>
<br />
<br />
Choose the name of your Resource Group and the Region. I chose RG-UCS-Nextcloud, RG for Resource Group, UCS for the US South Central Region, and Nextcloud because we are creating a Nextcloud server. The naming convention is up to you, but I recommend whatever you decide just be consistent.  <br/>
<img src="https://i.imgur.com/SAoaUFU.png"/>
<br />
<br />
Click on the Review + create button on the previous page and then on the create button as shown here. Both buttons are located at the bottom left of the page.  <br/>
<img src="https://i.imgur.com/SAoaUFU.png"/>
<br />
<br />
Once the Resource Group is finished being created, click on the go to resource group button at the top right of the page. Congratulations, you have just created your first Resource Group!!!  <br/>
<img src="https://i.imgur.com/SAoaUFU.png"/>
<br />
<br />


<!--
  <br/>
<img src="https://i.imgur.com/SAoaUFU.png"/>
<br />
<br />

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
