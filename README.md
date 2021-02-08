## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Azure Elk Deployment](https://github.com/SolidSol/SolidSol/blob/main/HW12%20Elk%20Project%20Diagram.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the (YAML) file may be used to install only certain pieces of it, such as Filebeat.

  - Ansible Playbooks Elk-Playbook.yml._

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly (dynamic), in addition to restricting (access) to the network.

- A load-balancer has features and policy controls to stop bad traffic from ever reaching the main application, two main examples being (rate limiting) and (URL filtering). Both software and physical Load-balancers work on layers 4-7 of the OSI model (transportation, session application, presentation). Load-balancers protect against threats like (S.Q.L injection) and (Cross-site scripting (XSS)). 

- A Jump Box is a window server that is a bridge between two trusted networks. The Jump Box is in most cases security hardened and is the main entryway to your server group. The Jump Box is usually built in front of other servers to add a security layer preventing all Azure VM's from being exposed to the public. Advantages of using a Jump box, it allows you to focus all the monitoring and logging on that one box and also a jump box allows you to turn ir off to stop all RDP (Remote Desktop Protocal) to everything when you know its not needed. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the (Configuration) and system (Files).

- "Filebeat" watches and monitors the log files or locations that users specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing. Filebeat is a lightweight shipper for forwarding and centralizing log data. Installed as an agent on the server.

- "Metricbeat" kinda like Filebeat, but Metricbeat is a lightweight shipper that periodically collects metrics from the operating system and from services running on the server. It akes the metrics and statistics that it collects and ships them to the output that you specify.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name         | Function  | IP Address | Operating System |
|--------------|-----------|------------|------------------|
| Jump Box     | Gateway   | 10.0.0.1   | Linux            |
| Web-1        | Web server| 10.0.0.5   | Linux            |
| Web-2        | Web server| 10.0.0.6   | Linux            |
| ElkProject1VM| Web Server| 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the (Jump Box) machine can accept connections from the Internet through PORT 22. Access to this machine is only allowed from the following IP addresses: (My IP)
- The 3 machines built within this network can only be accessed by the provisioned Jump box.This particular provisioning allows for only my personl IP to gain access to the ElkProject1VM works off of PORT 5601. Machines outside of this network can only gain access by remote access through said Jump box within the Ansible container.

A summary of the access policies in place can be found in the table below.

| Name         | Publicly Accessible | Allowed IP Addresses | Operating System |
|--------------|---------------------|----------------------|------------------|
| Jump Box     | Yes                 | 10.0.0.1 10.0.0.2    | Linux            | 
| Web-1        | No                  | My ip                | Linux            |
| Web-2        | No                  | My IP                | Linux            |
| ElkProject1VM| SSH-NO /http-yes    | MY Ip                | Linux            |

### Elk Configuration
- I used Ansible to configure and automate the all three of the VM's. No configuration was performed manually, which is advantageous because, Ansible allows for universal changes to be made within any of the VMs associated with the Ansible. This helps with consistency between machines and fluidity with the playbook established.

- One of the main advantages of "Automation" within Ansible is the use of roles. Ansible Roles provide the groundwork or the road map for either fully independent,or interdependent collections of variables, tasks, files, templates and modules. These Roles simplify the writing of complex playbooks. The Rolse themselfs are not the Playbooks, but rather simple functionalities within the playbook. Basically the "legos" to your larger machine.

The playbook implements the following tasks:
- The VMs can be built in 5 steps. 1st)  Install doker.io  2nd.) Install python3-pip 3rd.)Install Docker module E.g.
- Elk Instalation:) Creating a new vNet which we needed to be located in the same (resource group), most of the setting stayed consistant, my focus was on the adding Peering, which established the connection between all vNets. Importan for allowing traffic to pass between said vNets a
- Install Docker): we had to create a playbook that installed Docker and configured the containers, -name: Config elk VM with Docker

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Docker](https://github.com/SolidSol/SolidSol/blob/main/Elk%20Project%231%20docker%20confirm.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
ElkProject1VM   10.1.0.4
JuMpBox  10.0.0.4
Web-1  10.0.0.5
Web-2  10.0.0.6


- List the IP addresses of the machines you are monitoring_

- I successfully installed Filebeat and MetricBeat on my Web-1, Web-2 and ElkProject1VM

- Filebeat watches/monitors log files, log events and locations that users specify,   Example: Inputs and harvesters. While Metricbeat watches for any information in the file system which has been changed/altered and time frame. Takes the statistics

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Edit the /etc/ansible/ansible.cfg command line remote_user=username to refelect the remote account being used to execute playbooks.

- Update the /etc/ansible/host file to the group(s) we want to install packages on. 
- Run the playbook, and navigate to Jump box to check that the installation worked as expected.

- The ansible.cfg file is the playbook
- I updated the (Elk.yml) file to make Ansible run the playbook on a specific machine? To specify which machine to install the ELK server on versus which to install Filebeat on, I used specific IP's of the servers?
 
- In order to check that the my ELK server was running I navigated to http://[ElkProject1VM-ip]:5601/app/kibana
