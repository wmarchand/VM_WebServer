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
<img src="https://i.imgur.com/xSsZQ9K.png"/>
<br />
<br />
Click on the Review + create button on the previous page and then on the create button as shown here. Both buttons are located at the bottom left of the page.  <br/>
<img src="https://i.imgur.com/KdkT8Wc.png"/>
<br />
<br />
Once the Resource Group is finished being created, click on the go to resource group button at the top right of the page. Congratulations, you have just created your first Resource Group!!!  <br/>
<img src="https://i.imgur.com/MFWeGwD.png"/>
<br />
<br />

<h3> 2) Create a Virtual Network and a subnet</h3>
While in your Resource Group that was just created, click the create button.  <br/>
<img src="https://i.imgur.com/7xHDgOW.png"/>
<br />
<br />
Then search for Virtual Network in the search bar. Find the result that says Virtual Network and click create.  <br/>
<img src="https://i.imgur.com/sexs5LU.png"/>
<br />
<br />
Here you will be able to choose which Resource Group you would like the Virtual Network in. Choose the Resource Group that we just created, in my case it is RG-USC-Nextcloud. Next, name the Virtual Network and keep consistent to the naming convention that you chose before. Mine is named VNET-USC-Nextcloud. Keep in mind, the Virtual Network needs to be in the same Region as Resource Group. Click next at the bottom of the page until you get the the IP Addresses tab.  <br/>
<img src="https://i.imgur.com/WtPGhea.png"/>
<br />
<br />
The Virtual Network is populated with a default IP address space. We are going to assign our own IP so click the Delete Address Space button.  <br/>
<img src="https://i.imgur.com/Dx0nPJP.png"/>
<br />
<br />
It will then give you an error message saying You must add at least one address space to the virtual network. Click the Add IPv4 address space button.  <br/>
<img src="https://i.imgur.com/DD6WNNt.png"/>
<br />
<br />
After creating a new IPv4 Address Space, we need to assign our IP Address range. Here I chose 172.10.0.0/16. We also want to create a Subnet, click the Add a subnet button within the Address Space. In the Add a subnet sheet, we need to name the subnet. Again, keep to the chosen naming convention, SNET-USC-Nextcloud. Choose the IPv4 address range, the Starting address and the Size. The IPv4 Address range is the range we just created in the address space, the starting address can be the first IPv4 address in that address range, and for the size I chose /24, which will give me 256 IP addresses but Azure uses 5 address so only 251 usable IPv4 addresses. Click Add at the bottom of the Add a subnet sheet. After you have chosen your Address range and subnet, click the Review + create button at the bottom left of the page.  <br/>
<img src="https://i.imgur.com/nlJdAT9.png"/>
<br />
<br />
After the Virtual Network finishes validating, click the create button at the bottom of the page.  <br/>
<img src="https://i.imgur.com/fITWtW8.png"/>
<br />
<br />
Once the Virtual Network has been created, you will be able to see the network under your Resource Group.  <br/>
<img src="https://i.imgur.com/1vlt17L.png"/>
<br />
<br />
If you click on our Virtual Network that we just made, you will be able to verify the Address space at the top right of the page. In the hamburger menue on the left, you can also click on Address space or Subnets if you want to verify the addresses.  <br/>
<img src="https://i.imgur.com/N0RjNS2.png"/>
<br />
<br />
Scroll down in the hamburger menue and click on the Diagram button. Here we can see the topology of our Virtual Network so far. We can the subnet we created within the Virtual Network we created.  <br/>
<img src="https://i.imgur.com/5vQVvsJ.png"/>
<br />
<br />

<!--
  <br/>
<img src=""/>
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
