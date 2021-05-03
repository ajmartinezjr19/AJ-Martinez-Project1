# AJ-Martinez-Project1
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Images/diagram-topology.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml file may be used to install only certain pieces of it, such as Filebeat.

  (Images/install-elk.png)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_
- Loab balancers protect from DDoS attacks by shifting the attacking traffic from the coporate server to a public cloud. An advantage to using a jumpbox is the added layer of security needed to access other servers on the network via ssh key or other means.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- _TODO: What does Filebeat watch for?
- Filebeat watches for changes in the files and logs whats whats changed and when.
- _TODO: What does Metricbeat record?
- Metricbeat collects metrics and statistics from the operating system and ships them to the specified output.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name                 | Function | IP Adress             | Operating System |
|----------------------|----------|-----------------------|------------------|
| Jump Box Provisioner | Gateway  | 20.64.249.41 10.0.0.4 | Linux            |
| Web 1 (DVWA)         | Server   | 10.0.0.7              | Linux            |
| Web 2 (DVWA)         | Server   | 10.0.0.6              | Linux            |
| Elk Server           | Monitor  | 20.64.45.129 10.1.0.4 | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox-provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 73.153.142.138

Machines within the network can only be accessed by ssh connections.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_
- Access to the ELK VM is available through the ansible container on the Jumpbox-Provisioner machine which has a public IP of 20.64.249.41.

A summary of the access policies in place can be found in the table below.

| Name                | Publicly Accessible | Allowed IP Address |
|---------------------|---------------------|--------------------|
| Jumpbox-Provisioner | Yes                 | 73.153.142.138     |
| Web 1               | No                  | 10.0.0.4           |
| Web 2               | No                  | 10.0.0.4           |
| Elk Server          | Yes                 | 10.0.0.4           |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_
- Automating configuration with Ansible helps eliminate time consuing tasks and allows it to be set up in miniutes across multiple servers.

The playbook implements the following tasks:
- Installs Docker to use for creating containers
- Installs python3-pip thats used for managing software packages
- Downloads the Elk Container
- Lists ports that Elk will run on
- Increases available memory

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/docker-ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
- Web 1 10.0.0.7
- Web 2 10.0.0.6

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
- Filebeat checks on the files or locations the user specifies and monitors changes to the log files.
- Metricbeat records metrics and statistics from the servers and operating system which can be used to analyze how much RAm was being used during a specified time.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to /etc/ansible/roles/files.
- Update the filebeat-config.yml file to include the private IP address of the Elk VM - 10.1.0.4.
- Run the playbook, and navigate to http://20.65.45.129:5601/app/kibana to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- filebeat-playbook.yml is the playbook and it is copied to the filebeat directory to run.
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- The Host file must be updated with the new Web VMs IP addresses as well as the Elk-Servers IP address.
- _Which URL do you navigate to in order to check that the ELK server is running?
- http://20.65.45.129:5601/app/kibana
