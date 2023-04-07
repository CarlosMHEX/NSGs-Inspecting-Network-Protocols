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

[Microsoft Azure](https://portal.azure.com) is where the VMs are created and where they're stored via cloud. <img src="https://user-images.githubusercontent.com/125783560/230516013-55b3ee5b-a281-4506-9b38-2fd7178a638d.png" height "50" width "50">


<img src="https://user-images.githubusercontent.com/125783560/230515360-a42ed1fe-0850-405c-85f3-ba67a3af39e0.png">

<p>The virtual Machine creation page as shown is where I choose which subscription the VM would be a part of.. What storage group it will be in.. The name of my VM.. Location of where the VM will be at in the cloud.. The type of operating system.. And essentially how strong the computer is, as well as user and password for login.</p>



