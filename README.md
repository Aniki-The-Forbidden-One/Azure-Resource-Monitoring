# Azure Resource Monitoring
This project demonstrates the configuration of a secure virtual network environment on Microsoft Azure, designed to allow only HTTPS traffic and provide comprehensive monitoring and alerting. The goal was to create a robust, secure setup while implementing key skills from the AZ-104 certification.

<h2>Project Overview</h2>
Objective: Deploy a secure Azure Virtual Network and Virtual Machine with enforced HTTPS access, storage monitoring, and alert configurations.
Technologies: Azure Virtual Network (VNet), Network Security Groups (NSG), Virtual Machines (VM), Storage Account, Azure Monitor, and Alert Rules.
Outcome: A fully monitored virtual network and VM, with alert rules and diagnostic settings to proactively manage and secure the environment.
Deployment Steps:

1. Set up the Virtual Network and Network Security Group
Create a Virtual Network (VNet) in your resource group.
Add a Network Security Group (NSG) to allow only HTTPS traffic:
Configure an Inbound Rule for port 443 (HTTPS).
Add a Deny All rule for other traffic.

2. Deploy a Virtual Machine and Configure Monitoring
Deploy a Virtual Machine (VM) within the VNet.
Enable Monitoring and Insights on the VM.
Configure alerts for:
CPU Utilization: Alert when usage exceeds a threshold (e.g., 80%).
VM Avaliability: Alert when the Avaliability for the VM is down.

3. Configure Storage Account with Diagnostic Logging
Create a Storage Account within the resource group.
Enable Monitoring and Diagnostics:
Track metrics like total storage used and transactions.
Configure alert rules to notify on anomalies or specific thresholds.

4. Testing the Alerts
CPU Alert: Simulate high CPU usage to trigger the alert via powershell.
Storage Alert: Adjust storage account usage to test alert rules.

<h2>Azure Resource Monitoring and Alerting System project</h2>

Project Overview:
The goal is to create an automated resource monitoring system that includes virtual machines (VMs), 
network security configurations, storage accounts, and alerts to notify you of issues or usage spikes.

We will start this Project off by setting up a Virtual Network:

<img width="1384" height="529" alt="image" src="https://github.com/user-attachments/assets/05ef90bf-0028-4698-8b75-4f6773cd4d66" />

Next we'll add a subnet:

<img width="1509" height="224" alt="image" src="https://github.com/user-attachments/assets/aa2c054a-f2be-4924-8fbd-4f8a62616221" />

The VNET will be created in a resource group with the following Address spaces, VNET: 10.0.0.0/16 (65,536 addresses) Subnet: default (10.0.0.0/24) (256 addresses)

The next step is to set up a Network Security Group (NSG) and associate it with the VNET we just made.
I will then set up rules to restrict access to the group, for this project we'll set it up so only port 443 (HTTPS) can access the NSG.
I will set up an inbound security rule for this with the piority set to 100.
The next step is to set up another inbound security rule to deny all other ports and we will set the piority to 200.
This will allows Port 443 (HTTPS) only as it has higher piority.

<img width="1706" height="706" alt="image" src="https://github.com/user-attachments/assets/94634069-229c-4867-b32e-b34537c74af7" />

The next step of this project is to deploy a VM and set it up for monitoring.
To save on operational costs I will be using no avaliability options, Standard_B1s which is afforable and is eligible with free services.
We will also be using Standard SSD OS disk type with local reduntant storage and with the smallest size to save on costs.
Finally to help save on operational costs, I will enable automatic shutdown at 7pm everynight. 
For networking, we will be using the virtual network and subnet we created earlier.
For the monitoring we will be setting up default alert rules to a personal email address. I will also be setting up boot diagnostics with a managed storage account.

<img width="1406" height="633" alt="image" src="https://github.com/user-attachments/assets/53c44f83-d9cc-4ef4-92bd-fb9968d6c037" />

<img width="1434" height="542" alt="image" src="https://github.com/user-attachments/assets/c1ce1b45-2cab-4a42-8b1f-ec2a2dbac9f6" />

The next step to this project is to set up a storage account and container to store the data.
The storage account will be made in the same resource group and region as the VM.
I'll be saving costs by using standard performance and setting the redundancy to locally redundant storage (LRS).
The access tier will be set to hot as it will be the most cost effective for this project.
I'll have soft delete for blob data and containers (7 days) as a recovery option incase of acidental deletions. 

<img width="1369" height="786" alt="image" src="https://github.com/user-attachments/assets/2c4a2441-cbd3-4fc2-8667-ecc0c9c8ba95" />

Finally we shall enable logs to be stored from the VM to the container.

<img width="1483" height="194" alt="image" src="https://github.com/user-attachments/assets/7dfece76-22e0-478d-aaf1-5f66c2991ac1" />

Next i'll be configuring monitoring and alerts for the VM.
First I'll create a action group which will send me a email to my personal email address to alert me when the conditions on my rules are met.

<img width="785" height="472" alt="image" src="https://github.com/user-attachments/assets/395a280e-300c-4d13-be9b-4b98a0dae938" />

I'll be setting up an alert rule for CPU % usage when above 80% which will be evaluated every 5 minutes, the severity level will be set to "warning".

<img width="634" height="760" alt="image" src="https://github.com/user-attachments/assets/1bcf413f-2b34-4409-820f-430cf0aa85bd" />

Finally to make sure that the alert is working, i'll be testing it by connecting to the VM via remote desktop protocol (RDP).
In order to do this, I must first create RPD access temporarily as only HTTPS is allowed at this moment of time. the piority will be set to 150.

<img width="1699" height="650" alt="image" src="https://github.com/user-attachments/assets/754b0340-5d3c-4155-868e-8e2b72082330" />

Now that we have created the RPD access, we can now log on to test the rule.

<img width="1460" height="613" alt="image" src="https://github.com/user-attachments/assets/3650944e-2c14-4acb-b3da-c58ae6b4ec64" />

Now that we are logged on, i'll use powershell to perform a stress test and wait for the email to alert me of CPU usage.

<img width="991" height="738" alt="image" src="https://github.com/user-attachments/assets/488d0911-4bac-4230-9a04-53d433fbd875" />

Now we check our e-mail after being notified that the rule's condition has been met.

<img width="498" height="728" alt="image" src="https://github.com/user-attachments/assets/5d711ea8-48fd-4bb7-a0e9-3f650bf74790" />

The Project is now complete, the following Azure services used in this project: 
Virtual Network, Network Security Groups, Virtual Machine, and Storage Account.

Key features:
List the specific configurations, like HTTPS-only traffic enforcement, alert rules for CPU usage, storage monitoring, scripts and ARM templates for deployment.


