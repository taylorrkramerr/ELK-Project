# ELK-Project
Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.

These files have been tested and used to generate a live ELK deployment on Azure. 
They can be used to either recreate the entire deployment pictured above. 
Alternatively, select portions of the __.yml___ file may be used to install only certain pieces of it, such as Filebeat.
The ansible playbooks elk.yml and the filebeat-playbook.yml will be needed in order to create the ELK-server.
This document contains the following details:
Description of the Topology
Access Policies 
ELK Configuration
Beats in Use
Machines Being Monitored
How to Use the Ansible Build
Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly available , in addition to restricting access to the network.
Load Balancers fall under the availability aspect when talking about the CIA triad. 
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system flow or traffic .
Filebeat watches for logs and log files and their location and tracks log events.
Metricbeat records statistical data from services running on the server being used.
The configuration details of each machine may be found below. Note: Use the Markdown Table Generator to add/remove values from the table.
Name
Function
IP Address
Operating System
Jump Box
Gateway
10.1.0.4/
20.120.97.42
Linux 
Web-1
Ubuntu
10.1.0.5/
13.68.203.126
Linux
Web-2
Ubuntu
10.1.0.6/
13.68.203.126
Linux
ELK-S
Ubuntu
10.0.0.4/
20.122.106.37
Linux 

Access Policies
The machines on the internal network are not exposed to the public Internet.
Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
ssh sysadmin@20.120.97.42
Machines within the network can only be accessed by SSH.
 My Jumpbox had access to my ELK server . JumpBox IPs private : 10.1.0.4 public: 20.120.97.43 
A summary of the access policies in place can be found in the table below.
Name
Publicly Accessible
Allowed IP Addresses
Jump Box
Yes (SSH)
20.120.97.42
Web 1
Yes (HTTP)
10.1.0.5
Web 2

Elk-S
Yes(HTTP)

Yes(HTTP)
10.1.0.6

10.0.0.4 & personal

Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
The main advantage of automating configuration through ansible is how easy it can be and how efficient it is. You are able to configure multiple playbooks for multiple machines with a few single commands after using the original configuration .

The playbook implements the following tasks:
Installs docker.io - It references the IP address listed under [elk] in ansible's hosts file 
Increases virtual memory - A standard container does not have enough virtual memory to run an ELK container. For 3 DVWA machines, the suggested amount is 262144.
Installs python3 -- the Docker module uses python which we had to put on our VM
Installs docker modules
Downloads and launches web container - Downloads and launches the ELK container.
The following screenshot displays the result of running docker ps after successfully configuring the ELK instance.

Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web 1 : 10.1.0.5 
Web 2: 10.1.0.6
Elk_Server: 10.0.0.4 
We have installed the following Beats on these machines:
I successfully installed the Filebeat and Metricbeat onto the machines.
These Beats allow us to collect the following information from each machine:
Filebeat allows us to collect log data from sources like apache and elasticsearch . While metric allows us to use our VM’s to capture CPU usage , and Network ISO . both beats are very valuable to use when collecting data and we saw that when we looked at our logs on Kibana.
Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:
SSH into the control node and follow the steps below:
Copy the YAML file to the Ansible folder .
Update the Config file to include the correct ports and your username 
Run the playbook, and navigate to Kibana to check that the installation worked as expected.
TODO: Answer the following questions to fill in the blanks:
Which file is the playbook? Where do you copy it?
/etc/ansible/files/filebeat-config.yml 
 /etc/filebeat/filebeat.yml
Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
To make the ansible playbook run I had to update the hosts file .
_Which URL do you navigate to in order to check that the ELK server is running?
http://[your_elk_server_ip]:5601/app/kibana

