## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(/Images/net_diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.
	[install-elk.yml](Ansible/install-elk.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network.
	Load balancers allow for high availability because they protect the system from DDoS and other attacks.
	A Jump Box allows for managing the security of machines externally, hardening the overall system.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files on the machine and metrics:

	Filebeat - retrieves data about the file system.
	Metricbeat - retrieves machine metrics, such as uptime.

The configuration details of each machine may be found below.


| Name     | Function   | IP Address | Operating System |
|----------|------------|------------|------------------|
| Jump Box | Gateway    | 10.0.0.1   | Linux            |
| Web-1    | Web Server | 10.0.0.2   | Linux            |
| Web-2    | Web Server | 10.0.0.3   | Linux            |
| ELK      | Monitor    | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
	104.43.53.101

Machines within the network can only be accessed by each other (not externally).
	Jump Box connects to ELK via IP 10.0.0.1

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 104.43.53.101        |
| Web-1    | No                  | Virtual Network      |
| Web-2    | No                  | Virtual Network      |
| ELK      | No                  | Virtual Network      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows for accelerated automation.

The playbook implements the following tasks:
	Install docker.io
	Install pip3
	Install Docker python module
	Increase virtual memory
	Download and launch a docker

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Alt text](Images/docker-ps.png?raw=true)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

	Web-1: 10.0.0.2
	Web-2: 10.0.0.3

We have installed the following Beats on these machines:

	Filebeats
	Metricbeats

These Beats allow us to collect the following information from each machine:

	Filebeat - data about the file system
	Metricbeat - machine metrics

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
1. Copy the playbook file to Ansible Control Node.
2. Update the hosts.txt file to include webserver and elk
3. Run the playbook, and navigate to Kibana to check that the installation worked as expected.

FAQ:

The playbook file is filebeat-playbook.yml, copy it to /etc/ansible so it's available for use.

Update the hosts.txt file to deermine which machines it will work with. The hosts.txt file should have the following format:
```
[webservers]
10.0.0.0
10.0.0.1

[elk]
10.0.0.2
EOF
```

To check if ELK server is running, go to: http://[Host IP]/app/kibana#/home