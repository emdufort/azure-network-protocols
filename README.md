![image](https://github.com/emdufort/azure-network-protocols/assets/153258619/36922c7b-60c8-426c-8d82-f6130b980df5)


Part 1 (Create our Resources)
Create a Resource Group
Create a Windows 10 Virtual Machine (VM)

![image](https://github.com/emdufort/azure-network-protocols/assets/153258619/a8bd0624-cf21-486f-bfe0-263aa996c330)

While creating the VM, select the previously created Resource Group

![image](https://github.com/emdufort/azure-network-protocols/assets/153258619/fc7e17b3-179b-4726-8b65-f991ecff79d9)


While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet

![image](https://github.com/emdufort/azure-network-protocols/assets/153258619/d2c49216-f126-4742-94ff-a06056f3245a)

Create a Linux (Ubuntu) VM

![image](https://github.com/emdufort/azure-network-protocols/assets/153258619/ad891759-b6b0-42cd-8853-89affeb7a944)



While create the VM, select the previously created Resource Group and Vnet
Observe Your Virtual Network within Network Watcher

Part 2 (Observe ICMP Traffic)
Use Remote Desktop to connect to your Windows 10 Virtual Machine

![image](https://github.com/emdufort/azure-network-protocols/assets/153258619/25ab3a85-22ac-40c9-b756-a13b1f9ef4a9)


Within your Windows 10 Virtual Machine, Install Wireshark

![image](https://github.com/emdufort/azure-network-protocols/assets/153258619/9fa41fb6-a7fd-4c7b-925a-38af0bfe6420)

![image](https://github.com/emdufort/azure-network-protocols/assets/153258619/e9ac0aa5-9b82-463a-9f45-16e7190cc863)

![image](https://github.com/emdufort/azure-network-protocols/assets/153258619/b0cf90c8-ffbe-453e-a4b6-dd33dd9163b0)

Open Wireshark and filter for ICMP traffic only
Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM
Observe ping requests and replies within WireShark

![image](https://github.com/emdufort/azure-network-protocols/assets/153258619/4fe95981-5a4c-4e03-a3c8-06302fb79a52)

![image](https://github.com/emdufort/azure-network-protocols/assets/153258619/ffa5ba4e-bd9e-43e3-8600-d7dda5fb9e47)

From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark

![image](https://github.com/emdufort/azure-network-protocols/assets/153258619/90bf2c86-fc55-4eb0-a68e-9330b8037d41)

![image](https://github.com/emdufort/azure-network-protocols/assets/153258619/7b6a6505-5149-4d6e-a4bc-728879402814)


Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM
![image](https://github.com/emdufort/azure-network-protocols/assets/153258619/22490767-038c-4c5c-8d2f-aaecc44de694)

![image](https://github.com/emdufort/azure-network-protocols/assets/153258619/637f146c-e01e-4264-83af-5a9a7ce5eaf5)

Create a firewall in Azure
1. open Azure and in the search type Network Security groups

2. Select VM2-NSG, then select "inbound security rules"

![image](https://github.com/emdufort/azure-network-protocols/assets/153258619/c03299e0-d440-4042-beee-9aba9320e365)

3. Change settings to deny ping

4. ![image](https://github.com/emdufort/azure-network-protocols/assets/153258619/cc441120-4699-46cb-b8e1-e750365efad9)

5. press add, you will see on wire shark that its sya request

6. ![image](https://github.com/emdufort/azure-network-protocols/assets/153258619/a10d2fb2-e407-4955-bf32-7b097a8a0813)


7. ![image](https://github.com/emdufort/azure-network-protocols/assets/153258619/2dea39fc-5e55-4199-9fe6-04f5a9c0d990)

Switching back to allow ping






Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic
Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity
Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using
Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)
Stop the ping activity

Part 2 (Observe SSH Traffic)
Back in Wireshark, filter for SSH traffic only
From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)
Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark
Exit the SSH connection by typing ‘exit’ and pressing [Enter]

Part 2 (Observe DHCP Traffic)
Back in Wireshark, filter for DHCP traffic only
From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)
Observe the DHCP traffic appearing in WireShark

Part 2 (Observe DNS Traffic)
Back in Wireshark, filter for DNS traffic only
From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are
Observe the DNS traffic being show in WireShark

Part 2 (Observe RDP Traffic)
Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)
Oserve the immediate non-stop spam of traffic? Why do you think it’s non-stop spamming vs only showing traffic when you do an activity?
Answer: because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted

Lab Cleanup (DON’T FORGET THIS)
Close your Remote Desktop connection
Delete the Resource Group(s) created at the beginning of this lab
Verify Resource Group Deletion
