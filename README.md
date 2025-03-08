<h1>Capturing DHCP Requests and Responses in Wireshark on Azure VMs</h1>
Objective: Explain how DHCP (Dynamic Host Configuration Protocol) assigns IP addresses to Azure VMs, capture DHCP request/response traffic in Wireshark, and analyze how VMs obtain their network configurations dynamically.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Powershell
- Various Command-Line Tools
- Network Protocol ICMP
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 Pro (22H2)
- Ubuntu Server 22.04


<h2>Actions and Observations</h2>

<br>

<h3>Step 1 - DHCP (Dynamic Host Configuration Protocol)</h3>
•	DHCP is responsible for automatically assigning IP addresses to devices when they join a network. This prevents IP conflicts and ensures devices can communicate without manual configuration.
<br>
<br>
•	The DHCP process involves four steps:
<br>
  1.	Discover – The client broadcasts a request for an IP address.
<br>
  2.	Offer – The DHCP server responds with an available IP.
<br>
  3.	Request – The client requests to use the offered IP.
<br>
  4.	Acknowledge – The server confirms and leases the IP to the client.
<br>
<br>
•	Port Numbers:
<br>
  •	67 (UDP) – Used by the DHCP server.
<br>
  •	68 (UDP) – Used by the DHCP client.
<br>
<br>
•	In Wireshark: Filtering for dhcp (or bootp, since DHCP is based on BOOTP) allows you to see devices requesting and receiving IP addresses, which is useful for troubleshooting network connectivity issues.
<br>
<img width="764" alt="Step 6a- DHCP" src="https://github.com/user-attachments/assets/c0eb6caf-6bd4-4a0a-9db7-ded146c36ec9" />
<img width="764" alt="Step 6b- DHCP" src="https://github.com/user-attachments/assets/cbe319b1-6f4d-43a8-8e04-d6c4bb58e49e" />
