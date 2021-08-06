# cloud_security
Project 1 - cloud security
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![image](https://github.com/melvyn10/cloud_security/blob/main/Screenshot%2021-08-05%202536.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select individual file may be used to install only certain pieces of it, such as Filebeat.

 activity3_dvwa.yml - install dvwa contaner
 install-elk.yml - install elk container
 filebeat-playbook.yml - install filebeat service
 metricbeat-playbook.yml - install metricbeat service
 
This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly reliable and scalable, in addition to restricting access to the network.
Load balancers also provide security for the system, keeping the networks protected from the open web and balancing the incoming traffic preventing DDOS attacks, thereby providing a more efficient application. 
The advantage of a jumpbox is to provide a gateway to assess and configure the VMs.  It allows restricted ssh access to the jumpbox while providing a way to utlize ansible to install docker containers.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system performance with the use of Filebeat and Metricbeat. 

The configuration details of each machine may be found below.

| Name     | Function   | Public IP Address | Private IP Address | Operating System |
|----------|------------|-------------------|--------------------|------------------|
| Jump Box | Gateway    | 104.42.170.162    | 10.0.0.1           | Linux            |
| ELK - VM | ELK Server | 52.173.27.56      | 10.0.0.4           | Linux            |
| Web - 1  | WebApp     |       N/A         | 10.1.0.7           | Linux            |
| Web - 2  | WebApp     |       N/A         | 10.1.0.8           | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBoxProvisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

Public IP: My Personal PC Public IP

Machines within the network can only be accessed by JumpBoxProvisioner.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses          |
|----------|---------------------|-------------------------------|
| Jump Box | Yes                 |Personal PC Public IP          |
| ELK - VM | Yes                 |Personal PC Public IP 10.0.0.1 |
| Web - 1  | No                  | 10.1.0.4  10.0.0.1            |
| Web - 2  | No                  | 10.1.0.4  10.0.0.1            |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it ensures consistant, tracable and repeatable deployments - configuration as code.

The elk installation playbook implements the following tasks:
Install docker.io
Install pip
Install docker python module
Download and launch docker web container
Enable docker service on boot

This ELK server is configured to monitor the following machines:
DVMA-VM1
DVMA-VM2

We have installed the following Beats on these machines:
Filebeat
Metricbeat

Filebeat and Metricbeat collects and forwards log data and metrics from the machines it is installed on and sends this information to the ELK stack server for processing. This information can then be viewed through Kibana through customizable charts and tables.

### Using Ansible Build and the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:

Copy the filebeatconfig.yml and metricbeatconfig.yml file to /etc/ansible/files/.

Update the /etc/ansible/host file to include the private IP addresses of the DVWAs

Run the playbook (ansible-playbook filebeatconfig.yml)

Navigate to http://52.173.27.56:5601/app/kibana to validate the information collected are visible through Kibana.
