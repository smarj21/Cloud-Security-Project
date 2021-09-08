# Cloud-Security-Project
Repository containing files related to my Cloud Security and Elk Deployment project 

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[[Images/Network-Diagram.png]]

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml and configuration file may be used to install only certain pieces of it, such as Filebeat.

  - Ansible Configuration 
  - Ansible ELK Installation
  - FileBeat Playbook
  - Metricbeat Playbook

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting unwanted traffic to the network.

- What aspect of security do load balancers protect?
  
Load balancers assist in defending organisations against DDOS attacks. They also assist in protecting availability and web traffic.

- What is the advantage of a jump box?

Advantages of a jump box include, improved security, ease of automation, and access control


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- Filebeat monitors log files and collects data about the file system and forwards them onto Logstash or ElasticSearch for indexing
- Metricbeat collects machine metrics such as CPU usage and uptime and sends them to a specified output (LogStash, ElasticSearch) 

The configuration details of each machine may be found below.


| Name          | Function      | IP Address   | Operating System |
|---------------|---------------|--------------|------------------|    
| Jump Box      | Gateway       | 10.1.0.4     | Linux            |
| Web-1         | Web Server    | 10.1.0.5     | Linux            |  
| Web-2         | Web Server    | 10.1.0.7     | Linux            |      
| ELK           | Elk Server    | 10.0.0.4     | Linux            |     
| Load Balancer | Load Balancer | 20.92.75.120 | Linux            |



### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the ELK Server machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Workstation Public IP through port TCP 5601

Machines within the network can only be accessed by Workstation and Jumpbox Provsioner

- Jumpbox Provisioner IP: 10.1.0.4 via SSH port 22

A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible ? | Allowed IP Addresses                           |
|---------------|-----------------------|------------------------------------------------|
| Jump Box      | No                    | WorkStation IP                                 |
| Web-1         | No                    | 10.1.0.4                                       |
| Web-2         | No                    | 10.1.0.4                                       |
| Elk           | No                    | Workstation Public IP using TCP:5601, 10.1.0.4 |
| Load Balancer | No                    | Workstation Public IP using HTTP:80            |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows the ability to install a variety of apps on multiple machines and easily configure machines through the use of playbooks, thus saving critical time. 

The playbook implements the following tasks:

- Specify a group of machines
- Increase system memory
- Install Docker, Python and docker.io
- Launch and expose container to ports 5601,9200 and 5044


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[[Images/Docker-Ps.png]]

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.1.0.5 
- Web-2 10.1.0.7

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat monitors audit logs, depreciation logs, gc logs, server logs and slow logs.  
- Metricbeat collects metrics and system statistics. For example, you can monitor system CPU, memory and load.


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Ansible ELK Installation file to /etc/ansible
- Update the hosts file to include the ELK and web server IP Addresses
- Run the playbook, and navigate to http://[your.ELK-VM.External.IP]:5601/app/kibana to check that the installation worked as expected.


### Useful Commands

| COMMAND                | PURPOSE            |
|------------------------|--------------------|   
| ansible-playbook       | Run the Playbook   |                   
| ssh-keygen             | Generate Keygen    |
| sudo docker start      | Start the container|
| sudo docker attach     | SSH into Ansible   |                                 
| systemctl status docker| Status of Docker   |
