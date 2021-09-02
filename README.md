# GT_Project_1
Creation of Azure cloud network with 2 VNets, 2 security groups, a jumpbox, a load balancer, 2 web servers, and an ELK Server. Creation of ELK stack providing network monitoring for web servers.

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

""Images/ELK"": Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the /etc/ansible file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._ NEED TO FIND should be = /etc/ansible "This might be in /etc/ansible/roles or /etc/ansible/folders or something"
  - put all playbook files here

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

| Name     | Function   | IP Address | Operating System |
|----------|------------|------------|------------------|
| Jump Box | Gateway    | 10.0.0.1   | Linux            |
| Web1     | Webserver  |            | Linux            |
| Web2     | Webserver  |            | Linux            |
| ELK-VM   | ELK Server |            | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Home Network IP address

Machines within the network can only be accessed by the Jump-Box-Provisioner
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_
""Jump-Box-Provisioner: <ip address> via SSH port 22. MAKE SURE TO PUT IP ADDRESSES NEXT TO THESE NAMES""

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes/No              | 10.0.0.1 10.0.0.2    |
|          |                     |                      |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because Ansible is able to easily deploy multitier apps by creating what is known as ansible playbooks which allow you to apply these playbooks to VMs. These ansible playbooks will configure the VM based on what is specified in the ansible playbook. The main advantage is that you can re-use these ansible playbooks in order to configure VMs in the future with ease.

The playbook implements the following tasks: CHECK WHAT THE INSTALL-ELK.YML - _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._ = just check install-elk elk installation playbook and write down what it does below
- Create a Filebeat and Metricbeat configuration file.
- Create an Ansible playbook that copies this configuration file to the DVWA VMs and then installs Filebeat and installs Metricbeat. 
- Create a Playbook also installs docker.io, python3-pip, downloads and launches a docker elk container, increases the system memory, and exposes specific ports.
- Run the install-elk.yml, filebeat-playbook.yml, and metricbeat-playbook.yml to install items listed above..
- Confirm that the ELK Stack is receiving logs for Filebeat and Metricbeat.""
- ... DOUBLE CHECK ALL OF THIS

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
""10.0.0.4 
10.0.0.5
10.1.0.4""

We have installed the following Beats on these machines:
- Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
- Metricbeat will monitor your specified machines by collecting metrics from the operating system and services running on that machine such as CPU usage, memory, file system, disk IO, network IO statistics, and statistics on processes running on your system""
Filebeat will monitor your specified machines by collecting logs from the machine such as audit logs, deprecation logs, and server logs.


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the roles folder to /etc/ansible/roles.
- Update the hosts file to include your Webserver IP's and ELKServer IP's. Be sure to specify the correct host in your ansible playbook. For me, it would we webservers.
- Run the playbook, and navigate to HTTP://<ELKServer_Public_IP>:5601 to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
