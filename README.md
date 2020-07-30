# AndrewFin_Bootcamp-Repository
Repository for Coursework related to Cyber-Security Bootcamp
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![](AndrewFin_Bootcamp-Repository/Diagrams/"Week 12 Diagram.png")

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.
- ![](AndrewFin_Bootcamp-Repository/Ansible/Pentest.yml.txt)
- ![](AndrewFin_Bootcamp-Repository/Filebeat/Filebeat-Configuration.yml)
- AndrewFin_Bootcamp-Repository/Filebeat/Filebeatsetup.yml
- AndrewFin_Bootcamp-Repository/Ansible/Hosts.yml.txt
- AndrewFin_Bootcamp-Repository/Elk/Install_Elk.yml.txt
  

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly responsive, in addition to increasing access to the network.
Load Balancing prevents DDoS (Denial of Service) Attacks, by switching traffic from the attacked server to a different sever. 
A Jumpbox Server protects our system by securing VLANS using a firewall. It also has the ability to update and create/recreate operating systems for our Network with ease. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system operating system.
- Filebeat will monitor logs that have been recorded in the servers.
- Metricbeat will monitor metrics and measure statistics from the server periodically and output them into a report. 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  |40.125.67.5 | Linux            |
| Web-01   | Network  | 10.0.0.9   | Linux            |
| Web-02   | Network  | 10.0.0.12  | Linux            |
| Web-03   | Network  | 10.0.0.13  | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBoxProvisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 67.186.247.232

Machines within the network can only be accessed by JumpBoxProvisioner.
- JumpBoxProvisioner AzureUser@40.125.67.54

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| JumpBox  | No                  | 10.0.0.9 10.0.0.12   |
|          |                     |                      |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- You can set up the Elk Container without being inside the Elk Stack. 
- It makes management of the Elk Stack Operating System easier (Easier to update remotely). 
- It also allows us to maximize storage for intallation
- Allows users to install partial packages.
- Reduces the recovery time for the Elk Server 
- Increases ability to create a duplicate

The playbook implements the following tasks:
- Install Docker so that containers can be configured in the Elk Server
- Install Python3 and and install docker within python3
- Increase virtaul memory automatically when Elk is booted
- Download and Launch a docker container for Elk
- Enable the docker container previously created
./Images/Elk-Container-Setup.png

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
./Images/Docker-Containers-in-Elk.png

### Target Machines & Beats

This ELK server is configured to monitor the following machines:
- Web-01 10.0.0.9
- Web-02 10.0.0.12
- Web-03 10.0.0.13

We have installed the following Beats on these machines:
- Filebeat 
- Winlogbeat
- Metricbeat
- Auditbeat

These Beats allow us to collect the following information from each machine:
- These beats allow administrators to monitor the seperate operating systems in the network. It also is useful in monitoring security and unusual activity. 
- Winlogbeat will develop a report based on Windows event logs.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to /etc/ansible.
- Update the filebeat-confiig.yml file to include the IP Address of the Elk Virtual Machine
- Run the playbook, and navigate to http://10.2.0.4:5601/app/kibana to check that the installation worked as expected.

To setup Filebeat:
- Nano /etc/filebeat/filebeat-configuration.yml
- Scroll to output.elasticsearch: and adjust the hosts line to the elk server's IP Address
- Scroll to setup.kibana: and adjust the hosts line to the elk server's IP Address:5601
- Exit and save the configuration file
- Create a new .yml file (example FilebeatInstall.yml)
- After the filebeat playbook is played run ansible-playbook 'name-of-your-file.yml'

