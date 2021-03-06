# Cloud-Sec-Deploy
Cloud Security Deployment

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![](Images/Network-Drawing.png)
[Network-Drawing](https://github.com/TB-UofT/Cloud-Sec-Work/blob/38ea4ecc6b594419c9d8ade2d54305d240fb5857/Images/Network-Drawing.png)



These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select individual playbook files below may be used to install only certain pieces of it, such as Filebeat.

  - [DVWA](Files/DVWA-deploy-playbook.yml)
  - [ELK](Files/ELK-deploy-playbook.yml)
  - [Filebeat](Files/filebeat-deploy-playbook.yml)
  - [Metricbeat](https://github.com/TB-UofT/Cloud-Sec-Work/blob/496f5607430b7714d72be19debfeb9e10361020a/Files/metricbeat-deploy-playbook.yml)

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
- Load balancers restrict the incoming ports allowed as well as provide access to a backend pool of machines for high availability <!-- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_ --> 
- The Jumpbox is secured via key based authentication and connections restricted to specific IP addresses.  This secured box allows administrative access to the rest of the internal network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file and system metrics.
- Filebeat watches for the changes in the files in the locations that we specify or the log files and then collects and send the data to logstash/elasticsearch
- Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.
<!-- _Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_. -->

| Name    |  Function  | IP Address | Operating System |
|---------|:----------:|------------|:----------------:|
| JumpBox |   Gateway  | 10.0.0.5   |       Linux      |
|   web1  |    DVWA    | 10.0.0.4   |       Linux      |
|   web2  |    DVWA    | 10.0.0.6   |       Linux      |
|   web3  |    DVWA    | 10.0.0.7   |       Linux      |
|   ELK1  | ELK/Kibana | 10.0.0.7   |       Linux      |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 107.190.58.20

Machines within the network can only be accessed by the Jumpbox via it's Docker container.
- Jumpbox with IP of 52.170.152.100 is allowed to access the ELK1 Machine.

A summary of the access policies in place can be found in the table below.

|    Name    | Publicly Accessible | Allowed IP Addresses |
|:----------:|:-------------------:|:--------------------:|
|   Jumpbox  |         Yes         |     107.190.58.20    |
|    ELK1    |          No         |       10.0.0.5       |
| Web1..Web3 |          No         |       10.0.0.5       |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because:
<!-- _TODO: What is the main advantage of automating configuration with Ansible?_ -->
- Once a playbook has been written, it can be edited and deployed easily many times over, which saves valuable administrative time and effort.

The playbook implements the following tasks:
<!-- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._ -->
- Install Docker.io
- Install pip
- Install docker python module
- Install a docker ELK container
- Run command to increase virtual memory

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![ELK-container](Images/ELK-container.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.4
- 10.0.0.6

We have installed the following Beats on these machines:

- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat: log events
- Metricbeat: metrics and system statistics

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-deploy-playbook.yml and metricbeat-deploy-playbook.yml files to /etc/ansible/roles.
- Update /etc/ansible/hosts to include the ip address of the machine under webservers
- Run the playbook, and navigate to <IP.Address.OfYour.server:5601> to check that the installation worked as expected.

<!-- _TODO: Answer the following questions to fill in the blanks:_ -->
- Copy file [ELK-deploy-playbook](Files/elk-deploy-playbook.yml) to your ansible directory.  Run it with 'ansible-playbook elk-deploy-playbook.yml'
- The Hosts file located in /etc/ansible.  Editing this file will determine which machines are included in deployments <!-- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ -->
- To check if the ELK server is running, go to https://<IP.OF.YOUR.SERVER>:5601/app/kibana <!--_Which URL do you navigate to in order to check that the ELK server is running? -->

<!-- _As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._ -->

### To obtain and run this playbook, clone this repository, copy the files to the appropriate locations, and edit them to suit your needs.  Prerequisite is having a machine already set up and configured with ansible.

```
apt-get update && apt-get install git
git clone https://github.com/TB-UofT/Cloud-Sec-Work/
```

- Move to the directory you just cloned and copy the files to the appropriate location where you installed ansible.
- Edit the configuration files for the programs you wish to use as appropriate.
- Run the playbooks with:

```
ansible-playbook name-of-playbook.yml
```
