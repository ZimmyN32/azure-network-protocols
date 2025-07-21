<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create a resource group in Azure
- Create a Windows virtual machine
- Create a Linux virtual machine
- Ensure both VMs are in the same Virtual Network / Subnet
- Observe ICMP traffic
  - If using Mac, install Microsoft Remote Desktop
  - Use Remote Desktop to connect to your Windows 10 Virtual Machine
  - Within your Windows 10 Virtual Machine, Install Wireshark
  - Open Wireshark and start packet capture
  - Within Wireshark, filter for ICMP traffic only
  - Retrieve the private IP address of the Ubuntu VM (linux-vm) and attempt to ping it from within the Windows 10 VM
  - From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark
- Configuring a Firewall
  - Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM
    - Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic
    - Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity
    - Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is
    - Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)
    - Stop the ping activity

- Observe SSH traffic
  - Log back into the windows-vm
  - Back in Wireshark, start a packet capture up\
  - Filter for SSH traffic only
  - From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)
  - Open PowerShell, and type: ssh labuser@<private IP address>
    - Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark
    - Exit the SSH connection by typing ‘exit’ and pressing [Enter]
- Observe DHCP Traffic
  - Back in Wireshark, filter for DHCP traffic only
  - From your Windows 10 VM, attempt to issue your VM a new IP address from the command line
    - Open PowerShell as admin and run: ipconfig /renew
    - Observe the DHCP traffic appearing in WireShark
- Observe DNS Traffic
  - Back in Wireshark, filter for DNS traffic only
  - From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are
    - Observe the DNS traffic being show in WireShark
- Observe RDP Traffic
  - Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)
  - Observe the immediate non-stop spam of traffic


<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/lCHhrPS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here is a screenshot of the SSH traffic as well as the command-line interface
</p>
<br />

<p>
<img src="https://i.imgur.com/aGYUSpr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here is a screenshot of the RDP activity. You can't tell because its a screenshot but non-stop spamming is occuring. This is because the RDP is constantly showing you a live stream from one computer to another; therefor traffic is always being transmitted.
</p>
<br />
