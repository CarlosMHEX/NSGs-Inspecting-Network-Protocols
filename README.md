<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDP, DHCP, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used</h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>Objectives</h2>

- Create VMs (Windows) (Ubuntu/Linux) through Microsoft Azure
- Install Wireshark on windows VM to get a visual representation on the network trafficking going on between VMs
- Inspect traffic of protocols (SSH, RDP, DHCP, DNS, HTTP/s, ICMP)
- A bit of Network Security Group explaining and fiddling

<h2>Demonstration</h2>

<p>In this demonstration I show how I setup VMs using Microsoft Azure and installing Wireshark on a VM to inspect the traffic going on in networking protocols, giving a simple explanation of each protocol and how they work.</p>

[Microsoft Azure](https://portal.azure.com) is where the VMs are created and where they're stored via cloud.
<p align="center"> <img src="https://user-images.githubusercontent.com/125783560/230516013-55b3ee5b-a281-4506-9b38-2fd7178a638d.png" height="30%" width="30%"/>
</p>

<img src="https://user-images.githubusercontent.com/125783560/230515360-a42ed1fe-0850-405c-85f3-ba67a3af39e0.png">

<p>The virtual Machine creation page as shown is where I choose which subscription the VM would be a part of.. What storage group it will be in.. The name of my VM.. Location of where the VM will be at in the cloud.. The type of operating system.. And essentially how strong the computer is, as well as user and password for login. If you don't have any storage in Microsoft Azure then it will automatically create one for your VMs and their NSGs to be stored in. I created a Windows 10 VM and a linux VM or more specifically an Ubuntu VM on the same network of which will be used to show SSH network traffic.</p>

<img src="https://user-images.githubusercontent.com/125783560/230518324-f57cf7eb-891b-4d6a-92dc-b0e89838d4f3.png" height="80%" width="80%"/>

<p>I then RDP'd to the Windows VM using Remote Desktop Connection (included in most windows 10 versions), connecting to the public IP address of the VM and using the user login I setup back in Azure.</p>

<img src="https://user-images.githubusercontent.com/125783560/230519442-fcafd3e5-da12-46cf-99bd-39a5c11062fe.png">

After the login, I went ahead and installed [Wireshark](https://www.wireshark.org) which is the network protocol analyzer that I will be using to view the network traffic protocols SSH, RDP, DNS, HTTP/S, and ICMP.

<p align="center">
  <strong>Remote Desktop Protocol (RDP)</strong>
</p>
<p align="center"> <img src="https://user-images.githubusercontent.com/125783560/230541191-a0ec1196-f68f-42a6-881b-7f19e2802ce1.gif" height="20%" width="20%"/>
</p>
<img src="https://user-images.githubusercontent.com/125783560/230523340-f22cc204-ea0c-4f10-854f-250084f9f2bf.gif">

<p>Once the app launched, I went ahead and entered "tcp.port == 3389" in the display filter bar and started capturing packets which will allow me to view the RDP network traffic that as you can see is active. This is because I am currently using the Windows app "Remote Desktop Connection" which sends RDP packets via TCP (Transmission Control Protocol) between my computer and the VM to allow me to control the VM through my personal computer.</p>

<p align="center">
  <strong>Hypertext Transfer Protocol Secure (HTTP/S)</strong>
</p>
<img src="https://user-images.githubusercontent.com/125783560/230536452-d2e25d4e-937d-4a80-9ed6-e2999b64ae6c.gif">

<p>If I were to show you HTTP traffic on Wireshark it would be very lively since HTTP or HyperText Transfer Protocol is what is used to make the internet work.. HTTPS on the other hand is a more secured connection to websites, so if no browser activity is happening on your desktop PC then there is no HTTPS traffic until you'd browse the internet shown above.</p>

<p align="center">
  <strong>Domain Name System (DNS)</strong>
</p>
<img src="https://user-images.githubusercontent.com/125783560/230643410-c6b172fc-c041-420f-9d70-f69c3fa54d50.gif">

You can think of DNS as a way to convert website names such as `www.google.com` into a bunch of 1's and 0's that the computer can read... As you can see there is very much no traffic until I either start browsing the web which will cause DNS to start asking around for IP address to certain websites I browse to or as I show here the command `nslookup www.google.com` I use in Command Prompt to find out the IP address of the google website.

<p align="center">
  <strong>Dynamic Host Configuration Protocol (DHCP)</strong>
</p>
<img src="https://user-images.githubusercontent.com/125783560/230646935-65f0d0f2-6f34-4b0f-bef1-583b4988e56d.gif">

DHCP is the protocol that gives your network devices IP addresses as identification, think of it as your address to your home. Using Command Prompt, I will input the command `ipconfig /renew` which will ask the VM's router to basically refresh it's IP, causing DHCP traffic.

<p align="center">
  <strong>Secure Shell (SSH)</strong>
</p>
<img src="https://user-images.githubusercontent.com/125783560/230651644-7acde18e-aadb-4732-ab90-0cdc6a21a924.gif">

SSH is mostly used to configure devices over the network that don't have a display. I will connect to my Ubuntu VM using the command `ssh Hexyhex@10.0.0.5` (Hexyhex being the name of the user and the 10.0.0.5 being the private IP address of the VM) on Command Prompt which will start sending SSH packets over the two VMs to allow control similar to how I am using RDP to control VMs to give these demonstrations.

<p align="center">
  <strong>Internet Control Message Protocol (ICMP)</strong>
</p>
<img src="https://user-images.githubusercontent.com/125783560/230655639-0ef4d5e2-1925-47dc-afb3-4906c38b0148.gif">

<p>Now to inspect ICMP traffic with these 2 VMs, we will need the Ubuntu NSG to allow ICMP traffic to flow.. ICMP traffic is allowed by default, but I closed off any ICMP traffic by putting a security rule in Ubuntu's NSG to deny ICMP for this demonstration.. Seen above is ICMP traffic being caused by an infinite ping I inputted using Command Prompt, unable to ping my Ubuntu VM successfully.</p>

<img src="https://user-images.githubusercontent.com/125783560/230657611-7a5bd3f9-ade7-457e-82c3-be6bd03b5e9c.png">

<p>Going into Azure and into Ubuntu's NSG inbound rules I added a rule that allows for ICMP to flow.. The deny rule and allow rule are both present, but since I have the rule to allow at a higher priority than the one to deny, it allows the ICMP traffic to flow, hence there is a successful ping to the Ubuntu VM shown below.</p>

<img src="https://user-images.githubusercontent.com/125783560/230657034-734570db-2641-4aac-98b5-3f3c393f135c.gif">
  
