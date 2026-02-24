# Azure Resource Monitoring
This project demonstrates the configuration of a secure virtual network environment on Microsoft Azure, designed to allow only HTTPS traffic and provide comprehensive monitoring and alerting. The goal was to create a robust, secure setup while implementing key skills from the AZ-104 certification.

Project Overview
Objective: Deploy a secure Azure Virtual Network and Virtual Machine with enforced HTTPS access, storage monitoring, and alert configurations.
Technologies: Azure Virtual Network (VNet), Network Security Groups (NSG), Virtual Machines (VM), Storage Account, Azure Monitor, and Alert Rules.
Outcome: A fully monitored virtual network and VM, with alert rules and diagnostic settings to proactively manage and secure the environment.
Deployment Steps:

<h2>Set up the Virtual Network and Network Security Group</h2>
Create a Virtual Network (VNet) in your resource group.
Add a Network Security Group (NSG) to allow only HTTPS traffic:
Configure an Inbound Rule for port 443 (HTTPS).
Add a Deny All rule for other traffic.

<h2>Deploy a Virtual Machine and Configure Monitoring</h2>
Deploy a Virtual Machine (VM) within the VNet.
Enable Monitoring and Insights on the VM.
Configure alerts for:
CPU Utilization: Alert when usage exceeds a threshold (e.g., 80%).
VM Avaliability: Alert when the Avaliability for the VM is down.

<h2>Configure Storage Account with Diagnostic Logging</h2>
Create a Storage Account within the resource group.
Enable Monitoring and Diagnostics:
Track metrics like total storage used and transactions.
Configure alert rules to notify on anomalies or specific thresholds.

<h2>Testing the Alerts</h2>
CPU Alert: Simulate high CPU usage to trigger the alert via powershell.
Storage Alert: Adjust storage account usage to test alert rules.
