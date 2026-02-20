# SSH HRADENING AND SYSTEM MONITORING ON UBUNTU WEB SERVERS IN AZURE & AWS
This documentation details the hardening of Ubuntu-based EC2 web servers through SSH security measures and the implementation of continuous system monitoring after VPC setup. It demonstrates best practices for securing remote access, managing user permissions, and leveraging monitoring tools to track system performance and detect potential security threats, ensuring a robust and resilient cloud infrastructure on both AWS and Azure platforms.

<p align="center"> <img width="800" height="567" alt="vpc-Page-7 drawio" src="https://github.com/user-attachments/assets/865b3e2b-4cc5-4ecf-ac31-b1c1dd27c59f" />


## Table Of Contents
1. Introduction
2. Prerequisites and Services Used
3. AWS VPC Configuration
4. Azure Virtual Machine Configuration
5. SSH Hardening
6. Datadog Installation and Configuration
7. Errors and Troubleshooting
8. Conclusion



## Introduction
In modern cloud environments, securing server access and maintaining real-time visibility into system performance are critical for robust and resilient infrastructure. This project focuses on SSH hardening for Ubuntu-based web servers deployed on both AWS and Azure, ensuring secure remote access through best practices ensuring reliable connectivity. Datadog monitoring was also implemented to provide continuous oversight of system metrics, logs, and performance indicators. By integrating monitoring agents with these servers, the project demonstrates proactive detection of anomalies, resource optimization, and rapid response to potential security threats. 
Together, SSH hardening and Datadog monitoring establish a layered security and observability framework, showcasing best practices for cloud server protection, operational reliability, and proactive infrastructure management.

## Prerequisites and Services Used
1. Access to AWS console dashboard with an active subscription
2. Access to Azure portal dashboard with an active subscription
3. Designated Availabiltity Zone
4. Amazon Virtual Private Cloud
5. Azure Virtual Machine
6. EC2 Instance
7. Virtual Network
8. Ubuntu OS
9. Mobaxtern
10. Datadog Monitoring Agent

## AWS VPC Configuration
Configured a Virtual Private Cloud (VPC) in AWS, including subnet segmentation, route tables, security groups, and NACLs. Launched an Ubuntu EC2 instance in a public subnet and applied best practices for network segmentation, controlled internet access, and layered security.
Full Implementation here: https://github.com/Midas1045/AWS-Vpc/tree/main

## Azure Virtual Machine Configuration
Provisioned Ubuntu-based Virtual Machines on Microsoft Azure, including the setup of networking, storage, and security settings. Configured basic VM properties and ensured connectivity within the virtual network. 
Full Implemetation here: https://github.com/Midas1045/WebPage-Hosting/blob/main/README.md#creation-of-the-azure-virtual-machine

## SSH Hardening Configuration for AWS and Azure Web Servers
This stage was done to improve the security of our Ubuntu web servers where the default SSH port was changed from 22 to 2500. This simple adjustment helps reduce exposure to common automated attacks while maintaining reliable remote access, forming the foundation for a more secure server environment.

* After configuring the Amazon and Azure servers and launching the instances, I accessed both via SSH on the default port 22 using MobaXterm, with the server public IPs, downloaded key pairs, and assigned usernames.
* The next step involved updating the instances to ensure they had the latest packages and security patches. This was done using the following commands "sudo apt update" and "sudo    apt upgrade". These commands refreshed the package lists and applied all available upgrades, preparing the servers for further configuration and hardening.
* Following the upgrade, navigate to the home directory using "cd /" and use "ll" to list the contents of the directory.
* Access the SSH configuration directory by using the command "cd /etc/ssh" and use "ll" to list the contents of the directory.
* To edit the OpenSSH configuration file, use the command "sudo nano sshd_config" to access and modify it.
* Before editing sshd_config, ensure that the NACLs and subnet inbound rules for the instances allow traffic on the new SSH port (e.g., 2500). This prevents lockout after changing    the SSH port. Same applies to the security group for Azure.
* On the sshd_config file, use the arrow keys to navigate to the line showing the default port number. Then uncomment the line by removing the #. Change the port from 22 to 2500.     Optionally, add a comment noting the default port for reference. This updates the SSH service to listen on the new port while keeping a record of the original setting.
* Restart the SSH service to apply the configuration changes by using the following commands "sudo systemctl daemon-reload" and "sudo systemctl restart ssh". These commands reload    the systemd manager configuration and restart the SSH service, ensuring the server begins listening on the newly configured port.
* To verify that the SSH service is running and listening on the updated port, check its status using "sudo systemctl status ssh". This confirms the SSH service is active and helps   validate that the new port configuration has been applied successfully.
* Proceed to remove the default port 22 inbound rules for nacls and security for AWS and change by editing for Azure.
<p align="center"> <img width="800" height="585" alt="Screenshot 2026-02-20 143417" src="https://github.com/user-attachments/assets/64024b50-0d94-485f-adde-c6b5374d667e" />

## Datadog Installation and Configuration






