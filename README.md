<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDP, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used</h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>Objectives</h2>

- Create VMs (Windows) (Ubuntu/Linux) through Microsoft Azure
- Install Wireshark on windows VM to get a visual representation on the network trafficking going on between VMs
- Inspect traffic of protocols (SSH, RDP, DNS, HTTP/s, ICMP)

<h2>Demonstration</h2>

<p>In this demonstration I show how I setup VMs using Microsoft Azure and installing Wireshark on a VM to inspect the traffic going on in networking protocols, giving a simple explanation of each protocol and how they work.</p>

[Microsoft Azure](https://portal.azure.com) is where the VMs are created and where they're stored via cloud.
<p align="center"> <img src="https://user-images.githubusercontent.com/125783560/230516013-55b3ee5b-a281-4506-9b38-2fd7178a638d.png" height="30%" width="30%"/>

<img src="https://user-images.githubusercontent.com/125783560/230515360-a42ed1fe-0850-405c-85f3-ba67a3af39e0.png">

<p>The virtual Machine creation page as shown is where I choose which subscription the VM would be a part of.. What storage group it will be in.. The name of my VM.. Location of where the VM will be at in the cloud.. The type of operating system.. And essentially how strong the computer is, as well as user and password for login. I created a Windows 10 VM and a linux VM or more specifically an Ubuntu VM on the same network of which will be used to show SSH network traffic.</p>

<img src="https://user-images.githubusercontent.com/125783560/230518324-f57cf7eb-891b-4d6a-92dc-b0e89838d4f3.png" height="80%" width="80%"/>

<p>I then RDP'd to the Windows VM using Remote Desktop Connection (included in most windows 10 versions), connecting to the public IP address of the VM and using the user login I setup back in Azure.</p>

<img src="https://user-images.githubusercontent.com/125783560/230519442-fcafd3e5-da12-46cf-99bd-39a5c11062fe.png" height="100%" width="100%"/>

After the login, I went ahead and installed [Wireshark](https://www.wireshark.org) which is the network protocol analyzer that I will be using to view the network traffic protocols SSH, RDP, DNS, HTTP/S, and ICMP.

<img src="https://user-images.githubusercontent.com/125783560/230534132-b2c5c9ab-a5a7-45b2-98be-44453e6a0ec3.gif" height="20%" width="20%"/>
<img src="https://user-images.githubusercontent.com/125783560/230523340-f22cc204-ea0c-4f10-854f-250084f9f2bf.gif" height="100%" width="100%"/>

<p>Once the app launched, I went ahead and entered "tcp.port == 3389" in the display filter bar and started capturing packets which will allow me to view the RDP network traffic that as you can see is currently active. This is because I am currently using the Windows app "Remote Desktop Connection" which sends RDP packets via TCP (Transmission Control Protocol) between my computer and the VM to allow me to control the VM through my personal computer.</p>

<img src="https://user-images.githubusercontent.com/125783560/230536452-d2e25d4e-937d-4a80-9ed6-e2999b64ae6c.gif" height="100%" width="100%"/>

<p>If I were to show you HTTP traffic on Wireshark it would be very lively since HTTP or HyperText Transfer Protocol is what is used to make the internet work.. HTTPS on the other hand is a more secured connection to websites, so if no browser activity is happening on your desktop PC then there is no HTTPS traffic until you'd browse the internet shown above.</p>
