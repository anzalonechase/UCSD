# UCSD
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](/c/Users/anzal/Pictures/elk-topology)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._
/etc/ansible/elkstack.yml --this is a playbook despite the name not including "playbook"


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly protected, in addition to restricting traffic to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_
Load balancers protects the system from DDoS attacks by shifting attack traffic--protects layer 4 of osi model
The advantage of a jump box is to give access to the user from a single node that can be secured and monitored as well as protecting the azure VMs from exposure to the public.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- _TODO: What does Filebeat watch for?_::  any information in the file system which has been changed and when it has.
- _TODO: What does Metricbeat record?_::  takes the metrics and statistics that collects and ships them to the output you specify

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name      | Function | IP Address | Operating System |
|-----------|----------|------------|------------------|
| Jump Box  | Gateway  | 10.0.0.7 and dynamic public IP   | Linux            |
| Web1  | Server   | 10.0.0.4   | Linux            |
| Web2  | Server   | 10.0.0.5   | Linux            |
| ELK-server | Server   | 10.1.0.5   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_
Public localhost ip

Machines within the network can only be accessed by Jumpbox.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_
Allowed Localhost to access Elk-server

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Addresses |
|-----------|---------------------|----------------------|
| Jump Box  | Yes                 | Localhost IP              |
| Web1  | No                  | 10.0.0.7            |
| Web2  | No                  | 10.0.0.7            |
| ELK-server | yes                  | Localhost  IP           |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
it was closed off to the public, implementing a layer of security.
- _TODO: What is the main advantage of automating configuration with Ansible?_
1.  you can put commands into multiple servers from a single playbook
2. It is flexible and open-sourced

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Install: docker.io
- Install: python-pip3
- Install: docker
- Command: sysctl -w vm.max_map_count=262144 for memory allocation
- Launch docker container: elk

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](/c/Users/anzal/Pictures/elk-docker.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
Web1 10.0.0.4
Web2 10.0.0.5

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
Filebeat and metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
Filebeat collects the changes done, such as data/log changes
Metric beat collects metrics and statistics exports them to Elasticsearch

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to ansible.
- Update the host file to include webserver machines in this case (the machines you want to configure)
- Run the playbook, and navigate to kibana to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
root@1ab73c19e2d7:/etc/ansible/roles# ls
filebeat-playbook.yml  metricbeat-playbook.yml

- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
edit the /etc/ansible/host file to add Webserver/Elk-server IPs
- _Which URL do you navigate to in order to check that the ELK server is running?
publicip:5601 (Kibana)

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
sudo ansible-playbook /etc/ansible/(desiredPLAYBOOKsetup).yml
			 (Metricbeat-playbook.yml/filebeat-playbook.yml/elkstack.yml)
