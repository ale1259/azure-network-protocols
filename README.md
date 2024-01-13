<p align="center">

<img src="https://i.imgur.com/FwHLpH8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>  
  
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

- Part 2 Observe ICMP(Internet Control Message Protocol) Traffic:

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

- Part 3 Observe SSH(Secure Shell) Traffic:

  -Back in Wireshark, filter for SSH traffic only

  -From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address). Just use the commmand SSH and the IP address, type yes+ Enter and type the password, note that is not visible so type it correctly, you got 3 attempts until it close the connection, but you can try again from the beginning
  
   <img src="https://i.imgur.com/VTm22fE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

  -You will see traffic on Wireshark by now

   <img src="https://i.imgur.com/JWJfH86.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

 -Type commands ( pwd, ls -lasth, touch, etc) into the linux SSH connection and observe SSH traffic spam in WireShark

  -Exit the SSH connection by typing ‘exit’ and pressing [Enter]

- Part 4 Observe DHCP(Dynamic Host Configuration Protocol) Traffic:

  -Back in Wireshark, filter for DHCP traffic only

  -From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)

  -Observe the DHCP traffic appearing in WireShark

   <img src="https://i.imgur.com/hvgqy1R.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
 
   <img src="https://i.imgur.com/5kulx6W.png)" height="80%" width="80%" alt="Disk Sanitization Steps"/>

  

- Part 5 Observe DNS(Domain Name System) Traffic:

   -Back in Wireshark, filter for DNS traffic only,this time let's try another way instead of DNS on the bar type udp.port==53

  -From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are

  -Observe the DNS traffic being show in WireShark
  
    <img src="https://i.imgur.com/Ou1hBlD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

    <img src="https://i.imgur.com/5kulx6W.png)" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Part 6 Observe RDP(Remote Desktop Protocol) Traffic:

   -Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)
   
   -Observe the immediate non-stop spam of traffic? Why do you think it’s non-stop spamming vs only showing traffic when you do an activity?

  
   -Answer: because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefore traffic is always being transmitted

<img src="https://i.imgur.com/FwHLpH8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

