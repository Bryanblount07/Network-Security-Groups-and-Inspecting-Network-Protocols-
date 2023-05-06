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

- Create VM's
- Install Wireshark
- Re-Enable ICMP Traffic
- Use SSH

<h2>Actions and Observations</h2>

<p>
<img src="https://imgur.com/pjqCVFO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
First we need to create a Resource group & 2 VM's. Make sure to put them in the same resoure group. 1 with windows 10 & another with Ubuntu. After I create the VM's make sure you go to the "Network Watcher" to make sure they're in the same network.
</p>
<br />

<p>
<img src="https://imgur.com/jkh3qj2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now we have to go to our start menu on your own computer and bring up remote desktop. Copy your IP address from your VM-1 and paste it in the remote desktop. Then put in the user name & password you created when creating the VM"s.
</p>
<br />

<p>
<img src="https://imgur.com/Ioawzaa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Inside your VM bring open up microsoft edge and type in google. Then type in "Download wireshark" Click it then click on installer 64 bit for your windows or mac. Next everything and install. Then open it up.
</p>
<br />

<p>
<img src="https://imgur.com/lENlipV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click on the shark icon to start capturing packets. This will capture live packets. Click on the search within the wireshark and type ICMP (to filter) & press enter. There should be no traffic coming through now.
</p>
<br />

<p>
<img src="https://imgur.com/UEIATli.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now we have to open up powershell and we're going to ping the private ip address in VM 2. 
</p>
<br />

<p>
<img src="https://imgur.com/dkpL3wB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now we're going to block ICMP traffic on VM 2 firewall. Go to your VM 2 network security group (NSG). So now we can block ping coming from VM 1. Edit the Inbound rules. Create another rule. After it should be denying ping. Then go back and allow it to allow pings again.  
</p>
<br />

<p>
<img src="https://imgur.com/pff3var.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now we're going filter SSH traffic in Wireshark. So we're going to connect VM 1 into VM 2 via wireshark. So go into wireshark in your VM 1 & bring up command prompt. type in ssh & your user name @ VM 2 private ip address. EX: ssh labuser@10.0.0.4. After looking through that type exit to go back to your regular VM.
</p>
<br />

<p>
<img src="https://imgur.com/NnnK3cL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now we're going to vie some DHCP traffic. in your filter in wireshark type DHCP. Then go back to your cmd prompt and type ipconfig /renew. It should disconnect then reconnect.
</p>
<br />

<p>
<img src="https://imgur.com/cTaltGX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go back to wireshark & filter for DNS so we can see if we can get the IPv4 & IPv6 addresses. In your cmd prompt us nslookup google.com
</p>
<br />

<p>
<img src="https://imgur.com/qKFuu6w.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lastly were going to observe RDP. In your wireshark filter type (tcp.port==3389) and just observe the traffic.
</p>
<br /> 
