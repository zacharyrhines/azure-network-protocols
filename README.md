<p align="center">
  <img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

# Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines

In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups.

## Environments and Technologies Used

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

## Operating Systems Used

- Windows 10 (21H2)
- Ubuntu Server 22.04

## High-Level Steps

1. Create Virtual Machines in Azure.
2. Observe ICMP traffic between Virtual Machines using Wireshark.
3. Configure a Firewall (Network Security Group) and analyze its impact on network traffic.
4. Observe various protocol traffic (SSH, DHCP, DNS, RDP) using Wireshark.

---

## Part 1: Create Virtual Machines

1. Log in to [Azure Portal](https://portal.azure.com/).
2. **Create a Resource Group**:
   - Navigate to "Resource Groups" and click "Create."
   - Provide a name for your Resource Group and select a region.
   - Click "Review + Create," then "Create."
  
<p>
<img width="80%" height="80%" alt="NetworkSec1" src="https://github.com/user-attachments/assets/dfa61f86-decf-4978-b81a-5b4cb2080e86" />
</p>

3. **Create a Windows 10 Virtual Machine**:
   - Navigate to "Virtual Machines" and click "Create."
   - Select the Resource Group you just created.
   - Configure the Virtual Machine:
     - OS: Windows 10
     - Create username and password
     - Head to the Networking section, then create a new virtual network titled "Lab2-vnet"
   - Complete the setup and deploy the VM.
  
<p>
<img width="80%" height="80%" alt="NetworkSec2" src="https://github.com/user-attachments/assets/895db7c7-74b5-4d6d-a69f-87e3c9bc0537" />
</p>

<p>
<img width="80%" height="80%" alt="NetworkSec3" src="https://github.com/user-attachments/assets/c4f34d75-8183-46c0-91f3-53887ad20116" />
</p>

<p>
<img width="80%" height="80%" alt="NetworkSec4" src="https://github.com/user-attachments/assets/2f9d4570-1a54-40ee-ace0-aaa79c8d28fb" />
</p>

<p>
<img width="80%" height="80%" alt="NetworkSec5" src="https://github.com/user-attachments/assets/cd5f1faf-3a20-415a-942b-c3b88210e631" />
</p>

4. **Create a Linux (Ubuntu) Virtual Machine**:
   - Navigate to "Virtual Machines" and click "Create."
   - Select the same Resource Group and Virtual Network used for the Windows 10 VM.
   - Configure the Virtual Machine:
     - OS: Ubuntu Server 22.04
     - Authentication: Username/Password.
   - Ensure both VMs are in the same Virtual Network and Subnet as the Windows 10 VM.
   - Complete the setup and deploy the VM.

<p>
<img width="80%" height="80%" alt="NetworkSec6" src="https://github.com/user-attachments/assets/ef42ad60-49a6-4228-9c25-92121bcb1492" />
</p>

<p>
<img width="80%" height="80%" alt="NetworkSec7" src="https://github.com/user-attachments/assets/c168afc5-f5e1-4626-8a79-f308936f45af" />
</p>

<p>
<img width="80%" height="80%" alt="NetworkSec8" src="https://github.com/user-attachments/assets/0413fe29-b7d3-476a-8ab5-c15f2a25666d" />
</p>

<p>
<img width="80%" height="80%" alt="NetworkSec9" src="https://github.com/user-attachments/assets/e5975805-a9bd-42c3-92bc-ad14e3c8c6fc" />
</p>

---

## Part 2: Observe ICMP Traffic

1. Use [Microsoft Remote Desktop](https://apps.microsoft.com/store) to connect to your Windows 10 Virtual Machine (if on Mac, install the client first).
2. **Install Wireshark** on the Windows 10 VM:
   - Download and install Wireshark from [https://www.wireshark.org/](https://www.wireshark.org/).
3. Open Wireshark and start a packet capture.
4. Filter for ICMP traffic in Wireshark.
5. Retrieve the private IP address of the Ubuntu VM and attempt to ping it from the Windows 10 VM:
   - Open Command Prompt or PowerShell and run: `ping <Ubuntu VM Private IP>`.
   - Observe the ping requests and replies in Wireshark.
6. From the Windows 10 VM, ping a public website (e.g., `www.google.com`) and observe the ICMP traffic in Wireshark.

<p>
<img width="80%" height="80%" alt="NetworkSec10" src="https://github.com/user-attachments/assets/cfae4955-2b53-4516-a7bc-8eec9000fbd9" />
</p>

<p>
<img width="80%" height="80%" alt="NetworkSec11" src="https://github.com/user-attachments/assets/38311543-ae3f-4e0b-b43d-3ce7222ec93f" />
</p>

---

## Part 3: Configure a Firewall (Network Security Group)

### Observe ICMP Traffic with Firewall Changes

1. Initiate a continuous ping from your Windows 10 VM to the Ubuntu VM:
   - Command: `ping <Ubuntu VM Private IP> -t`.
2. Open the Network Security Group associated with the Ubuntu VM.
3. Disable inbound ICMP traffic in the Network Security Group.
4. Observe the ICMP traffic in Wireshark and the command line Ping activity (should stop).
5. Re-enable ICMP traffic in the Network Security Group.
6. Observe the ICMP traffic in Wireshark and the command line Ping activity (should resume).
7. Stop the ping activity.

<p>
<img width="80%" height="80%" alt="NetworkSec12" src="https://github.com/user-attachments/assets/f9d0f622-a135-437d-be84-8e4c0cd4e7d1" />
</p>

<p>
<img width="80%" height="80%" alt="NetworkSec13" src="https://github.com/user-attachments/assets/bb4706dd-8707-460a-b510-b1cd427721cb" />
</p>

<p>
<img width="80%" height="80%" alt="NetworkSec14" src="https://github.com/user-attachments/assets/1e9e9240-e26f-4c0b-8e7f-d140efa1c8a7" />
</p>

<p>
<img width="80%" height="80%" alt="NetworkSec15" src="https://github.com/user-attachments/assets/03f3251e-8941-409e-874a-626a62fa5e8c" />
</p>

<p>
<img width="80%" height="80%" alt="NetworkSec16" src="https://github.com/user-attachments/assets/b42c292d-1b13-4723-b75b-732c98ed3ce3" />
</p>

### Observe SSH Traffic

1. In Wireshark, start a new packet capture and filter for SSH traffic.
2. From the Windows 10 VM, SSH into the Ubuntu VM:
   - Command: `ssh <username>@<Ubuntu VM Private IP>`.
   - Enter the password when prompted.
3. Type commands within the SSH session and observe the SSH traffic in Wireshark.
4. Exit the SSH session: `exit`.

<p>
<img width="80%" height="80%" alt="NetworkSec17" src="https://github.com/user-attachments/assets/8a00a789-81a8-402e-98e1-41656c6ae48a" />
</p>

### Observe DHCP Traffic

1. In Wireshark, filter for DHCP traffic.
2. From the Windows 10 VM, issue a new IP address:
   - Open PowerShell as admin and run: `ipconfig /renew`.
3. Observe the DHCP traffic in Wireshark.

<p>
<img width="80%" height="80%" alt="NetworkSec18" src="https://github.com/user-attachments/assets/7a39e972-3b09-42d8-9c88-94901cd4d1b2" />
</p>

### Observe DNS Traffic

1. In Wireshark, filter for DNS traffic.
2. From the Windows 10 VM, use `nslookup` to find IP addresses for websites:
   - Example: `nslookup google.com`, `nslookup disney.com`.
3. Observe the DNS traffic in Wireshark.

<p>
<img width="80%" height="80%" alt="NetworkSec19" src="https://github.com/user-attachments/assets/ccb09753-b874-4701-bfb5-cc9596734dc6" />
</p>

### Observe RDP Traffic

1. In Wireshark, filter for RDP traffic:
   - Use the filter: `tcp.port == 3389`.
2. Observe the continuous RDP traffic between the Windows 10 VM and your local machine.

<p>
<img width="80%" height="80%" alt="NetworkSec20" src="https://github.com/user-attachments/assets/761707cb-8a67-43fa-822a-f7e65af2e4aa" />
</p>
