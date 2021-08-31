# Elk-Stack-Project
The files in this repository were used to configure the network depicted below. 

[Network-Diagram.pdf](https://github.com/G0nkDr0id395/Project_13/files/7080281/Network-Diagram.pdf)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  https://github.com/G0nkDr0id395/Project_13/blob/main/Ansible/ansible_configfile.yml

https://github.com/G0nkDr0id395/Project_13/blob/main/Ansible/filebeat-playbook.yml

https://github.com/G0nkDr0id395/Project_13/blob/main/Ansible/install-elk.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- A load balancer protects availability. The advantage of Jump Box is that it allows remote connections to come through one vm. Remote connections can be monitored to find suspecting behavior

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the configuration and system files.
- Filebeat is used to monitor log files
- Metricbeat is used to collect operating system data from VMs. 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway    | 52.188.113.51 | Linux            |
| Web-1    |   DVWA       |      10.0.0.7      |    Linux         |
| Web-2    |   DVWA       |   10.0.0.6         |    Linux         |
| Web-3    |   DVWA       |    10.0.0.5        |    Linux         |
| Elk-1       |   ELK           |     10.1.0.4       |   Linux          |   

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 73.137.252.24

Machines within the network can only be accessed by Jump Box.
- The Jump Box can access the ELM VM. The Jump Box IP is 52.188.113.51 

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |          Yes             | 73.137.252.24         |
|  Web-1     |         Yes              |  73.137.252.24        |
|  Web-2     |        Yes               |   73.137.252.24       |
|  Web-3     |      Yes                 |   73.137.252.24       |
| ELK -1      |      Yes                  |    73.137.252.24      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
-  The build and deployment is done automatically and efficiently

The playbook implements the following tasks:
- ansible_configfile.yml
- Install Docker
- Install Python
- Installs Docker's Python Module
- Downloads and launches the DVWA Docker container
- Enables the Docker service

- install_elk.yml
- Install Docker
- Install Python
- Install Docker's Python Module
- Increase virtual memory to support the ELK stack
- Increase memory to support the ELK stack
- Download and launch the Docker ELK container

- filebeat_playbook.yml
- Downloads and installs Filebeat
- Enables and congigures the system module
-Configures and launches Filebeat

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://github.com/G0nkDr0id395/Project_13/blob/main/dockerpsimage.pdf

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
-  Web-1: 10.0.0.7
-  Web-2: 10.0.0.6
-  Web-3: 10.0.0.5

We have installed the following Beats on these machines:
-  Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects and ships logs to Filebeat agent
- Metricbeat collects and ships system metrics from operating system and service of VM

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playboook file to Ansible Docker Container.
- Update the Ansible host /etc/ansible/hosts file to include

[webservers]
10.0.0.7 ansible_python_interpreter=/usr/bin/python3
10.0.0.6 ansible_python_interpreter=/usr/bin/python3
10.0.0.5 ansible_python_interpreter=/usr/bin/python3

[elkservers]
10.1.0.4 ansible_python_interpreter=/usr/bin/python3


- Run the playbook, and navigate to Kibana to check that the installation worked as expected.


- The playbook is filebeat-playbook.yml. You copy this to the /etc/ansible/hosts directory. 
- You update the filebeat.yml file. You have to create a new group and add the private IP of Elk-Server to this group. The you assign the private IP of the Elk-Server in two line of the .yml file
- Run the public IP address of 0.0.0.5601

**To run the playbook**
1. Use: "ssh sysadmin@<Jump Box Public IP>"
2. Start Ansible Docker container: "sudo docker start <Ansible Container>
3. Attach shell to container: sudo docker attach <Ansible Container Name>
4. Run the playbooks with the commands:
    - ansible-playbook /etc/ansible/ancible_configfile.yml
    - ansible-playbook /etc/ansible/install-elk.yml
    - ansible-playbook /etc/ansible/roles/filebeat-playbook.yml
5. Navigate to Kibana and verify the installation worked as expected. 
