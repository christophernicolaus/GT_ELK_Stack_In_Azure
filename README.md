# GT_Project_1
Creation of Azure cloud network with 2 VNets, 2 security groups, a jumpbox, a load balancer, 2 web servers, and an ELK Server. Creation of ELK stack providing network monitoring for web servers.

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

File Path: Diagrams/Full_Network_Diagram.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the /etc/ansible file may be used to install only certain pieces of it, such as Filebeat.

https://github.com/christophernicolaus/GT_Project_1/blob/6cba558b0139b048278b969726ebcd7dac551be1/Ansible/ansible_config.yml
https://github.com/christophernicolaus/GT_Project_1/blob/6cba558b0139b048278b969726ebcd7dac551be1/Ansible/ansible_elk.yml
https://github.com/christophernicolaus/GT_Project_1/blob/6cba558b0139b048278b969726ebcd7dac551be1/Ansible/filebeat-playbook.yml
https://github.com/christophernicolaus/GT_Project_1/blob/6cba558b0139b048278b969726ebcd7dac551be1/Ansible/install-elk.yml
https://github.com/christophernicolaus/GT_Project_1/blob/6cba558b0139b048278b969726ebcd7dac551be1/Ansible/metricbeat-playbook.yml
https://github.com/christophernicolaus/GT_Project_1/blob/6cba558b0139b048278b969726ebcd7dac551be1/Linux/ansible.cfg.yml
https://github.com/christophernicolaus/GT_Project_1/blob/6cba558b0139b048278b969726ebcd7dac551be1/Linux/filebeat-config.yml
https://github.com/christophernicolaus/GT_Project_1/blob/6cba558b0139b048278b969726ebcd7dac551be1/Linux/hosts
https://github.com/christophernicolaus/GT_Project_1/blob/6cba558b0139b048278b969726ebcd7dac551be1/Linux/metricbeat-config.yml

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
- Load balancers protect against Distributed Denial-of-Service attacks (DDoS attacks). The advantage of a jumpbox is that you can control all traffic by forcing the traffic into one central point, i.e. the jumpbox.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function   | IP Address    | Operating System |
|----------|------------|---------------|------------------|
| Jump Box | Gateway    | 23.96.107.167 | Linux            |
| Web1     | Webserver  | 10.0.0.5      | Linux            |
| Web2     | Webserver  | 10.0.0.6      | Linux            |
| ELK-VM   | ELK Server | 10.1.0.4      | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Home Network IP address

Machines within the network can only be accessed by the Jump-Box-Provisioner
- Jump-Box-Provisioner: 23.96.107.167 via SSH port 22. Private IP: 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Accessible | Allowed IP Addresses                                  |
|----------------------|---------------------|-------------------------------------------------------|
| Jump-Box-Provisioner | Yes                 | Home Network IP Address                               |
| Web1                 | No                  | Jump-Box: 23.96.107.167 LB: 20.106.163.202            |
| Web2                 | No                  | Jump-Box: 23.96.107.167 LB: 20.106.163.202            |
| ELK-VM               | No                  | Jump-Box: 23.96.107.167 Web1: 10.0.0.5 Web2: 10.0.0.6 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because Ansible is able to easily deploy multitier apps by creating what is known as ansible playbooks which allow you to apply these playbooks to VMs. These ansible playbooks will configure the VM based on what is specified in the ansible playbook. The main advantage is that you can re-use these ansible playbooks in order to configure VMs in the future with ease.

The playbook implements the following tasks:
- Increase Memory/Use More Memory
- Install docker.io
- Install python3-pip
- Install docker
- Download and launch ELK Container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

Diagrams/Day_1_Part_4_Project_1_Screenshot_ChristopherNicolaus.PNG

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
10.0.0.4: Web1
10.0.0.5: Web2
10.1.0.4: ELK-VM

We have installed the following Beats on these machines:
- Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
- Metricbeat will monitor your specified machines by collecting metrics from the operating system and services running on that machine such as CPU usage, memory, file system, disk IO, network IO statistics, and statistics on processes running on your system
- Filebeat will monitor your specified machines by collecting logs from the machine such as audit logs, deprecation logs, and server logs.


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml to /etc/ansible/install-elk.yml
- Update the hosts file to include your Webserver IP's and ELKServer IP's. Be sure to specify the correct host in your ansible playbook.
- Run the playbook, and navigate to HTTP://<ELKServer_Public_IP>:5601 to check that the installation worked as expected.

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

### Commands the user will need to run
- Put install-elk.yml under /etc/ansible
- Edit the hosts file in /etc/ansible and include the correct IP address with ansible_python_interpreter=/usr/bin/python3 under the correct []
- Run install-elk.yml by typing command: ansible-playbook install-elk.yml
- Now visit  HTTP://<ELKServer_Public_IP>:5601
- Now run the filebeat-playbook.yml and metricbeat-playbook.yml in the /etc/ansible folder by using ansible-playbook filebeat-playbook.yml and ansible-playbook metricbeat-playbook.yml
