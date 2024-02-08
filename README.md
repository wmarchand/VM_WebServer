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

<h3> 3) Protect a subnet using a Network Security Group</h3>
We are not going to better secure our Virtual Network by using a Network Security Group. While on the page of your Resource Group, click the create button.  <br/>
<img src="https://i.imgur.com/ymtGDx4.png"/>
<br />
<br />
Search for Network Security Group in the search bar. Find the result that says Network Security Group and click the create button within the box.  <br/>
<img src="https://i.imgur.com/Mk2a8eX.png"/>
<br />
<br />
We need to make sure we are in the right Resource Group and the correct Region and give our Network Security Group a name using our previous naming convention. Mine will be NSG-USC-NextCloud. Click the Review + create button when finished.  <br/>
<img src="https://i.imgur.com/4cEE0nq.png"/>
<br />
<br />
Once it has passed the Validation, click the create button in the bottom left corner.  <br/>
<img src="https://i.imgur.com/iZuyNPZ.png"/>
<br />
<br />
Congratulations, your Network Security Group has been created! Click on the Go to resource button to configure the rules.  <br/>
<img src="https://i.imgur.com/8XWeniS.png"/>
<br />
<br />
As you can see, Azure has created some default rules for us, these will be sufficient for what we need. Now lets assign these rules to our subnets. Click on our Resource Group to go back to that page.  <br/>
<img src="https://i.imgur.com/VDG2rWv.png"/>
<br />
<br />
Here we can see that our Network Security Group has been created and added to our Resource Group. To assign it to our subnets, we need to go to our Virtual Network by clicking our Virtual Networks name below the Network Security Group.  <br/>
<img src="https://i.imgur.com/7jd9n8B.png"/>
<br />
<br />
Once in your Virtual Network, click on Subnets in the left Hamburger menu. Then click on your subnet and on the right hand side, choose the Network Security Group that we just made. Then click save to finish the set up.  <br/>
<img src="https://i.imgur.com/CFUoh3g.png"/>
<br />
<br />
Lets see how the Network Security Group changed our Network Architecture. In the left hamburger menu, scroll down and select diagram. Here we can see that a Network Security Group has been added in our Virtual Network and connected to our subnet.  <br/>
<img src="https://i.imgur.com/0Gapdhw.png"/>
<br />
<br />

<h3> 4) Deploy Bastion to connect to a Virtual Machine</h3>
We are now going to deploy Bastion to connect to our Virtual Machine. We first need to create a new Subnet for Bastion. Under your Virtual Network, click Subnets in the hamburger menu on the left. Then click the + Subnet button near the top left. Unlike our previous Subnet, the name of the Subnet for Bastion is required, it has to be AzureBastionSubnet. We can keep all the rest of the defualts and click save at the bottom.  <br/>
<img src="https://i.imgur.com/O0haIPI.png"/>
<br />
<br />
We can verify here that our Bastion Subnet was created. We now need to create our Bastion Resource.  <br/>
<img src="https://i.imgur.com/EyhiCLt.png"/>
<br />
<br />
If we go back to the overview of our Resource Group, we can click + Create near the top left.  <br/>
<img src="https://i.imgur.com/mnoQc2s.png"/>
<br />
<br />
Search for Bastion and click the Create button when you find the correct Resource.  <br/>
<img src="https://i.imgur.com/hsagrHr.png"/>
<br />
<br />
You can see here, that our Resource Group was selected for us by default. We need to name our Bastion Resource and this time we can go back to our original naming convention, I chose BASTION-USC-Nextcloud. It gives us a default for the public IP address name, this has nothing to do with our Virtual Machine, so we are going to rename it the same as our Bastion Resource, BASTION-USC-Nextcloud. Then click Revew + create at the bottom left of the page. Then click create again once our Bastion Resource is done verifying. *NOTE* This will take a while to create, longer than anything we have created so far, you can continue the next steps while the Bastion Resource is being created.  <br/>
<img src="https://i.imgur.com/aTLhcpD.png"/>
<br />
<br />
Here we can see our Bastion Resource was created successfully.  <br/>
<img src="https://i.imgur.com/GnM9pHs.png"/>
<br />
<br />

<h3> 5) Create an Ubuntu Server Virtual Machine</h3>
We are now going to get to create our Virtual Machine! Make sure you are on your Resource Group page and click the + Create button.  <br/>
<img src=""/>
<br />
<br />
There might be a selection that comes up for an Ubuntu sever without the need to search for it. If not, search for Ubuntu. There will be multiple verstions of Ubuntu that appear. For this project, we are going to select the Ubuntu Server with the highest version number, in my case that is Ubuntu Server 23.10. Click create.  <br/>
<img src=""/>
<br />
<br />
First, we need to name our Virtual Machine with our same naming convention, mine is VM-USC-Nextcloud.  <br/>
<img src=""/>
<br />
<br />
Next we need to scroll down on the page until we get to the Size, click the see all sizes button to see our options.   <br/>
<img src=""/>
<br />
<br />
Here we can see all of the options we have while configuring a Virtual Machine. We are going to choose a basic one as we using minimal resources using it as a web server. The names of the sizes might change with time, for this project just choose the cheapest option, I chose B2ats_v2. Click on select at the botton left of the page.  <br/>
<img src=""/>
<br />
<br />
We now need to set up our Administrator Account. We are going to be using an SSH public key instead of a password. First we need to set our username, you can choose whatever you want, and then we are going to modify the default key pair name to be more specific, VM-USC-Nextcloud_SSHkey. Sice we are deploying Bastion, that is how we will be connecting to our Virtual Machine so we want to make sure to close all of the ports. Select the None radio button under Public inbound ports. Click the button Next: Disks >  <br/>
<img src=""/>
<br />
<br />
For this project, we are going to keep all of the OS disk defaults, go ahead and click the Next: Networking > button.  <br/>
<img src=""/>
<br />
<br />
We are going to set our own Public IP, so in the drop down box for Public IP, selct none. Since we already made our own Network Security Group, make sure the radio button none is selected for NIC network secruity group. Click Review + create at the bottom left of the page.  <br/>
<img src=""/>
<br />
<br />
  <br/>
<img src=""/>
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
