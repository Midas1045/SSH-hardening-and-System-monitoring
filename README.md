# SSH HARDENING AND SYSTEM MONITORING ON UBUNTU WEB SERVERS IN AZURE & AWS
This documentation details the hardening of Ubuntu-based EC2 web servers through SSH security measures and the implementation of continuous system monitoring after VPC setup. It demonstrates best practices for securing remote access, managing user permissions, and leveraging monitoring tools to track system performance and detect potential security threats, ensuring a robust and resilient cloud infrastructure on both AWS and Azure platforms.

<p align="center"> <img width="800" height="567" alt="vpc-Page-7 drawio" src="https://github.com/user-attachments/assets/865b3e2b-4cc5-4ecf-ac31-b1c1dd27c59f" />


## Table Of Contents
1. [Introduction](#introduction)
2. [Prerequisites and Services Used](#prerequisites-and-services-used)
3. [AWS VPC Configuration](#aws-vpc-configuration)
4. [Azure Virtual Machine Configuration](#azure-virtual-machine-configuration)
5. [SSH Hardening](#ssh-hardening)
6. [Datadog Installation and Configuration](#datadog-installation-and-configuration)
7. [Errors and Troubleshooting](#errors-and-troubleshooting)
8. [Conclusion](#conclusion)



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

<p align="center"> <img width="800" height="543" alt="Screenshot 2026-02-20 154558" src="https://github.com/user-attachments/assets/c47a6b73-47f5-45c9-a5e3-c1feb650384e" />

## Azure Virtual Machine Configuration
Provisioned Ubuntu-based Virtual Machines on Microsoft Azure, including the setup of networking, storage, and security settings. Configured basic VM properties and ensured connectivity within the virtual network. 
Full Implemetation here: https://github.com/Midas1045/WebPage-Hosting/blob/main/README.md#creation-of-the-azure-virtual-machine

<p align="center"> <img width="800" height="450" alt="Screenshot 2026-02-20 154530" src="https://github.com/user-attachments/assets/f8a1cbb5-d7ca-4bbd-af98-12f3d2bdd5ed" />

## SSH Hardening Configuration for AWS and Azure Web Servers
This stage was done to improve the security of our Ubuntu web servers where the default SSH port was changed from 22 to 2500. This simple adjustment helps reduce exposure to common automated attacks while maintaining reliable remote access, forming the foundation for a more secure server environment.

* After configuring the Amazon and Azure servers and launching the instances, I accessed both via SSH on the default port 22 using MobaXterm, with the server public IPs, downloaded   key pairs, and assigned usernames.
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
This stage shows how Datadog monitoring was set up to enable real-time tracking of system performance, resource usage, and logs.
* Go to https://www.datadoghq.com/# and create an account. After mail verification, the dashboard can now be accessible.
* Install the datadog agent by selecting the intended platform (LINUX).
* Infrastructure metrics, like CPU and Memory usage, are collected by default. To enable additional data collection, toggle on the options for app performance monitoring and log      collection.
* Specify the type of environment (development, production and staging).
* Copy the Datadog Agent installation command and run it in the server’s Linux environment for AWS and Azure.This contains an API key that can also be used for multiple servers.      After installation, start the agent service using "sudo systemctl start datadog-agent". This initializes the Datadog Agent and enables the collection of system metrics and logs     from the server.
* Check the status of the datadog agent using "sudo systemctl status datadog-agent". This confirms the agent is running and actively collecting system metrics.

<p align="center"> <img width="800" height="402" alt="Screenshot 2026-02-20 154057" src="https://github.com/user-attachments/assets/0b987fee-4486-4a6a-80d5-015715ec05b4" />

* Return to the Datadog website and navigate to the Infrastructure Dashboard to observe real-time monitoring of logs, system performance, and other key metrics. If additional         servers are available, navigate to the View Host List tab to view them.

<p align="center"> <img width="1352" height="266" alt="Screenshot 2026-02-20 162724" src="https://github.com/user-attachments/assets/1adab709-461a-4762-84b4-e7c44a23bbc7" />

You can watch the video here [Datadog System Monitoring](https://youtu.be/RUPv7jKEkZg)

## Errors and Troubleshooting




## Conclusion
This project demonstrates the successful implementation of SSH hardening and system monitoring on cloud-based Ubuntu servers. Updating the default SSH port enhances access security by reducing exposure to automated attacks, while the integration of monitoring tools enables real-time visibility into system performance, logs, and overall server health. Together, these measures confirm secure remote connectivity, improved operational awareness, and a stronger foundation for maintaining reliable and resilient cloud infrastructure.







