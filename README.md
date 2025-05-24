# Simple-pfSense-set-up

## Objective
The primary focus of this project was to gain basic familiarity of another firewall software in a virtualized environment. After pfSense set-up was complete, simple firewall rules were created on my own and experimented with to primarily learn rule components, rule ordering and processing.

Sources used for this set-up: [MyDFIR on YouTube](https://www.youtube.com/watch?v=IymmPht-dAQ), [Arcy Caparros](https://arcy24.medium.com/setting-home-lab-via-pfsense-part-1-5dffd73d6871), [Joshua Greene](https://drive.google.com/file/d/1bYiYn-L6si4Q27qhIIxpfigM0Ax9PofH/view), [ToTatCa on YouTube](https://www.youtube.com/watch?v=phwrzv8KlUE&t=624s)

### Skills Learned
- Installing and setting up pfSense
- Configuring NICs on VirtualBox (VB) and assigning interfaces within pfSense
- Creating simple firewall rules and seeing effects after editing 

### Tools Used
- pfSense as the open source firewall
- VirtualBox as the hypervisor 
- Simple CMD commands

### Takeaways
This project made me realize that setting up the environment can feel more complicated than configuring the software. Multiple sources are listed because the LAN IP in the pfSense shell did not match the default gateway in the Windows machine. All sources contributed in getting familiar with setting up pfSense. Rules creation at the end was a trial and error process on my own to see how they effect pings from the Windows virtual machine to the default gateway which is also the pfSense LAN IP address. Biggest takeaway is managing firewalls at an enterprise setting sounds very complicated and intricate. 

### Steps

Download pfSense iso on host machine at https://www.pfsense.org/download/ > purchase Netgate Installer with the image you want > verify SHA256 checksum > extract file > Create new Virtual Machine (VM) in VB.
<p align="center">
Purchase Netgate installer: <br/>
<img src="https://i.imgur.com/hGZkg7E.png" height="30%" width="30%" alt="pfSense Steps"/>
<br />
Download selected iso image: <br/>
<img src="https://i.imgur.com/o9fltTc.png" height="30%" width="30%" alt="pfSense Steps"/>
<br />
Verify SHA256 checksum - checksum matches: <br/>
<img src="https://i.imgur.com/JjnG0So.png" height="30%" width="30%" alt="pfSense Steps"/>
<br />
Extract file: <br/>
<img src="https://i.imgur.com/7jKMCYC.png" height="30%" width="30%" alt="pfSense Steps"/>
<br />
Create new VM in VB: <br/>
<img src="https://i.imgur.com/JKCPtsB.png" height="30%" width="30%" alt="pfSense Steps"/>
<br />

Need to add a network adapter for firewall machine in VB, Tools > Network > Properties > Create new network named pfsense in NAT Networks > assign 192.168.50.0 and enable DHCP > Apply. 
<p align="center">
VB Tools > Network: <br/>
<img src="https://i.imgur.com/7ite07E.png" height="30%" width="30%" alt="pfSense Steps"/>
<br />
Create a new NAT network: <br/>
<img src="https://i.imgur.com/VcrYL2b.png" height="30%" width="30%" alt="pfSense Steps"/>
<br />
Assign an IP address and enable DHCP: <br/>
<img src="https://i.imgur.com/cYhM4mW.png" height="30%" width="30%" alt="pfSense Steps"/>
<br />

Firewall typically uses two interfaces, one for WAN and one for LAN. A type two hypervisor like VB only has one physical NIC card so this set-up will have a WAN private IP instead of a normal public IP. 
In the pfSense VM settings > Network > Adapter 1 = Bridged adapter > Adapter 2 = NAT Network created earlier > OK. 
Bridged adapter means the pfSense VM will obtain the same IP on the same network as the host machine
<p align="center">
pfSense VM adapter 1 & 2 configurations: <br/>
<img src="https://i.imgur.com/Kaum6mh.png" height="30%" width="30%" alt="pfSense Steps"/>
<br />

Install pfSense by starting the pfSense VM in VB > Accept terms & conditions > Install pfSense. 
<p align="center">
Install pfSense: <br/>
<img src="https://i.imgur.com/CXzW0CJ.png" height="40%" width="40%" alt="pfSense Steps"/>
<br />

Select and assign the WAN & LAN interfaces in pfSense. The WAN interface is the bridged adapter with the correspoding MAC address. LAN interface is the pfSense NAT network with the corresponding MAC address.
<p align="center">
WAN interface = le0 = network adapter 1 = bridged adapter. Leave network operation mode default: <br/>
<img src="https://i.imgur.com/fClSo4f.png" height="30%" width="30%" alt="pfSense Steps"/>
<br />
LAN interface = le1 = network adapter 2 = NAT network. Leave network operation mode default: <br/>
<img src="https://i.imgur.com/GTx8hc0.png" height="30%" width="30%" alt="pfSense Steps"/>
<br />
