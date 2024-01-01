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

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Part 1 (Create our Resources):

  -Create a Resource Group, I called it "Networkinglab"

  -Create a Windows 10 Virtual Machine (VM)

  -While creating the VM, select the previously created Resource Group

  -While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet

  -Create a Linux (Ubuntu) VM, in the authentication type choose password
  
  -While create the VM, select the previously created Resource Group("Networkinglab" in my case) and Vnet of the Windows 10 VM

  -Observe Your Virtual Network within your Resource Group

<h2>Actions and Observations</h2>

- Part 2 (Observe ICMP Traffic):

  -Use Remote Desktop to connect to your Windows 10 Virtual Machine

  -Within your Windows 10 Virtual Machine open Microsoft Edge and start without data. Download Wireshark from the website https://www.wireshark.org/download.html the Window x64 version. The installation process is pretty straight forward, just leave everything by default. It will install Ncap 1.78 to complete the installation

  -Open Wireshark and click on the blue dorsal fin to start monitoring traffic. Now you can filter the traffic you like.
  
 <img src="https://i.imgur.com/GcdreV3.png" height="30%" width="30%" alt="Disk Sanitization Steps"/>

  -Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM

   <img src="https://i.imgur.com/JW57nYJ.png" height="30%" width="30%" alt="Disk Sanitization Steps"/>

   -Observe ping requests and replies within WireShark by filtering the traffic as ICMP

   <img src="https://i.imgur.com/PSdqZJt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

  -From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark

  <img src="https://i.imgur.com/fFXTAa7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

  -Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM (ping IP Address -t)

  -Open the Network Security Group your Ubuntu VM is using and go to Inbound security rules and Add a new rule. Just check ICMP and set the priority 200, action deny, the name could be DENY_ALL_ICMP, save the rule

   <img src="https://i.imgur.com/IvNVObW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

  -Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity. As you can see there is just requests and no replies from the Linux VM

  <img src="https://i.imgur.com/cpQN1F1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

  -Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using

  <img src="https://i.imgur.com/LXAGaCj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

  -Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)

  -Stop the ping activity Ctrl+C on the command line

- Part 3 (Observe SSH Traffic):

  -Back in Wireshark, filter for SSH traffic only

  -From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)

  -Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark

  -Exit the SSH connection by typing ‘exit’ and pressing [Enter]

- Step 4

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/LXAGaCj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
