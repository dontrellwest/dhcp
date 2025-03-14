<h1>Capturing DHCP Requests and Responses in Wireshark on Azure VMs</h1>
<h2>Objective</h2>

 - In this section, you will capture and analyze DHCP (Dynamic Host Configuration Protocol) traffic between your Windows 10 VM and the Azure network. 
 - You will manually trigger the process of releasing and renewing your VM’s IP address, then observe how DHCP traffic appears in Wireshark.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computers)
- Remote Desktop
- Powershell
- Batch Script Creation
- Command-Line Tools
- Network Protocol DHCP
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 Pro (22H2)
- Ubuntu Server 22.04


<h2>What is DHCP (Dynamic Host Configuration Protocol)?</h2>

DHCP stands for Dynamic Host Configuration Protocol. It’s a network management protocol used to automatically assign IP addresses and other network settings (like the default gateway and DNS servers) to devices on a network. 

Without DHCP, every device (like your VM) would need to be manually configured with an IP address and network settings — which is time-consuming and prone to errors. DHCP automates this process, ensuring that devices can join the network and communicate with each other without manual intervention.

•	The DHCP process involves four steps:
  - 	Discover – The client broadcasts a request for an IP address.  
  - 	Offer – The DHCP server responds with an available IP.  
  - 	Request – The client requests to use the offered IP.  
  - 	Acknowledge – The server confirms and leases the IP to the client.  

Port Numbers:

 - 67 (UDP) – Used by the DHCP server.
 - 68 (UDP) – Used by the DHCP client.

In Wireshark: Filtering for dhcp (or bootp, since DHCP is based on BOOTP) allows you to see devices requesting and receiving IP addresses, which is useful for troubleshooting network connectivity issues.
<br>

<h2>Actions and Observations</h2>
<h3>Step 1 - Filter for DHCP Traffic in Wireshark</h3>

 - [ ] Open Wireshark and start a new packet capture.
 - [ ] In the Wireshark filter bar, type: dhcp 
	 - This will isolate DHCP-related traffic, making it easier to spot DHCP requests and responses during the exercise.


  
<h3>Step 2 - Create a DHCP Batch File</h3>
To simplify the process of releasing and renewing the IP address, you will create a batch script:

 - [ ] Open Notepad (or any text editor).
 - [ ] Type the following commands: 
	
		•	ipconfig /release
		•	ipconfig /renew 

			Explanation
			•	ipconfig /release – Releases the current IP address, effectively telling the 
				DHCP server that you no longer need it.

			•	ipconfig /renew – Requests a new IP address from the DHCP server. 

 - [ ] Save the file as dhcp.bat: 
	 - [ ] In Notepad, choose File > Save As 
	 - [ ] Navigate to the folder: C:\ProgramData 
	 - [ ] In the “Save as type” dropdown, select “All files”
	 - [ ] Save the file as dhcp.bat (not .txt)

<img width="764" alt="Step 6a- DHCP" src="https://github.com/user-attachments/assets/c3d0e483-a171-4183-9166-26c54165152f" />
<img width="764" alt="Step 6b- DHCP" src="https://github.com/user-attachments/assets/6310ce3c-8677-4f3d-abe4-02cac6f9da0b" />

<h3>Step 3 - Execute the Batch File to Request a New IP Address</h3>
Now you will trigger the DHCP process manually: 

 - [ ] Open PowerShell as an administrator.
 - [ ] Change to the ProgramData directory by typing: 

			cd c:/programdata

 - [ ] Verify the script is in place by listing the files, typing: 

		- ls 
 - [ ] Run the script to release and renew the IP address by typing: 
		
		- .\dhcp.bat 
	 - The release command will send a DHCPRELEASE packet to the DHCP server, informing it that the VM is giving up its IP address. 
	 - The renew command will send a DHCPDISCOVER packet to search for available DHCP servers, and the server will respond with a new lease (IP address). 

  
  <img width="1512" alt="Step 6c- DHCP" src="https://github.com/user-attachments/assets/15cf2ca9-a02c-4b3e-904c-ed7edd9a3584" />

<h3>Step 4 - Observe the DHCP Traffic in Wireshark</h3>

 - In Wireshark, you should see the following DHCP packet sequence: 

	- DHCPDISCOVER – The VM broadcasts a request for an available IP address. 
	- DHCPOFFER – The DHCP server offers an IP address. 
	- DHCPREQUEST – The VM requests the offered IP address. 
	- DHCPACK – The server confirms and assigns the IP address to the VM. 

 - This completes the DHCP process and assigns the VM a new IP address.
  
<h2>Summary & Significance</h2>

<h3>What You Did</h3>

 - [ ] Created a batch script to automate the release and renew DHCP commands.
 - [ ] Used PowerShell to execute the script and trigger DHCP traffic.
 - [ ] Captured and analyzed DHCP traffic in Wireshark, including the DORA sequence. 
 - [ ] Verified the DHCP assignment through PowerShell output and Wireshark logs.

<h3>Why This Matters</h3>

 - DHCP is critical for network automation – it reduces the need for manual IP address assignment and ensures consistent network configuration.
 - Understanding DHCP traffic helps with troubleshooting IP conflicts, connectivity issues, and network misconfigurations.
 - Wireshark packet analysis allows you to confirm that the DHCP process is functioning correctly and helps identify if there are problems with DHCP server availability or configuration.
 - By automating the process with a batch file, you gain insight into how to work more efficiently with DHCP in a real-world scenario.

By completing this tutorial, you’ve gained practical experience with managing DHCP in Azure, automating network configuration, and capturing DHCP traffic with Wireshark. 
