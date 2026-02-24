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

We will start this Project off by setting up a Virtual Network with a Subnet.
The VNET will be created in a resource group with the following Address spaces
VNET:
10.0.0.0/16 (65,536 addresses)
Subnet:
default (10.0.0.0/24) (256 addresses)

The next step is to set up a Network Security Group (NSG) and associate it with the VNET we just made.
I will then set up rules to restrict access to the group, for this project we'll set it up so only port 443 (HTTPS) can access the NSG.
I will set up an inbound security rule for this with the piority set to 100.
The next step is to set up another inbound security rule to deny all other ports and we will set the piority to 200.
This will allows Port 443 (HTTPS) only as it has higher piority.

The next step of this project is to deploy a VM and set it up for monitoring.
To save on operational costs I will be using no avaliability options, Standard_B1s which is afforable and is eligible with free services.
We will also be using Standard SSD OS disk type with local reduntant storage and with the smallest size to save on costs.
Finally to help save on operational costs, I will enable automatic shutdown at 7pm everynight. 
For networking, we will be using the virtual network and subnet we created earlier.
For the monitoring we will be setting up default alert rules to a personal email address. I will also be setting up boot diagnostics with a managed storage account.

The next step to this project is to set up a storage account and container to store the data.
The storage account will be made in the same resource group and region as the VM.
I'll be saving costs by using standard performance and setting the redundancy to locally redundant storage (LRS).
The access tier will be set to hot as it will be the most cost effective for this project.
I'll have soft delete for blob data and containers (7 days) as a recovery option incase of acidental deletions. 
Finally we shall enable logs to be stored from the VM to the container.

Next i'll be configuring monitoring and alerts for the VM.
I'll be setting up alerts for CPU % usage when above 80% which will be evaluated every 5 minutes, the severity level will be set to "warning".
I'll create a action group which will send me a email to my personal email address to alert me this condition is met.
Finally to make sure that the alert is working, i'll be testing it by connecting to the VM via remote desktop protocol (RDP).
In order to do this, I must first create RPD access temporarily as only HTTPS is allowed at this moment of time. the piority will be set to 150.
Once logged on, i'll use powershell to perform a stress test and wait for the email to alert me of CPU usage.

The Project is now complete, the following Azure services used in this project: 
Virtual Network, Network Security Groups, Virtual Machine, and Storage Account.

Key features:
List the specific configurations, like HTTPS-only traffic enforcement, alert rules for CPU usage, storage monitoring, scripts and ARM templates for deployment.
