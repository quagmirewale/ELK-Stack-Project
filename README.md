## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Note: use this Diagram to understand Network Flow[Diagram of Cloud Design](Images/ELK_Stack_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

Note: These are all of the .yml configuration files that are needed to configure the environement:
[Playbook Files](Playbook_Files/filebeat-config.yml)
[Playbook Files](Playbook_Files/filebeat-playbook.yml)
[Playbook Files](Playbook_Files/install-elk.yml)
[Playbook Files](Playbook_Files/metricbeat.yml)
[Playbook Files](Playbook_Files/pentest.yml)
[Playbook Files](Playbook_files/metricbeat-playbook.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly avaliable, in addition to restricting Denial of Service attacks to the network.
- Load balancers are able to distribute traffic flow across an enterprise. Also it has the possibility of DDOS attacks by shifting attack traffic to a public cloud provider. The advantage of a jumpbox allows for access to your network while segregating the rest of the vm's from the public internet.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files systemand system metrics.
- Filebeat monitors the log files or locations that you specify, collects log events, and fowards them for indexing. It monitors for any type of configuraiton or modification changes.
- Merticbeat takes the metrics and statistics that it collects and ships them to the output that you specify.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator (https://www.tablesgenerator.com/markdown_tables) add/remove values from the table]_.

| Name          | Function      | Public IP Address | Private IP Address | Operating System |
|---------------|---------------|-------------------|--------------------|------------------|
| Jump-Box      | Gateway       | 52.249.176.236    | 10.0.0.4           | Linux            |
| ELK VM        | ELK Server    | 13.65.169.37      | 10.1.0.4           | Linux            |
| Web-App 1     | DVWA          | 52.188.13.180     | 10.0.0.5           | Linux            |
| Web-App 2     | DVWA          | 52.188.13.180     | 10.0.0.6           | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
76.97.34.60

Machines within the network can only be accessed by the Jump-Box.
The ELK VM can be accessed by the Jump-Box which has an IP Address of 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Address |
|-----------|---------------------|--------------------|
| Jump-Box  |         Yes         | 76.97.34.60        |
| ELK VM    |          No         | 10.0.0.4           |
| Web-App 1 |          No         | 10.0.0.4           |
| Web-App 2 |          No         | 10.0.0.4           |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
-_The main advantage of using Ansible is the automatic configuration which takes aways human error. This also allows for quick configuration of multiple machines or instances._

The playbook implements the following tasks:

- Installs Docker
- Installs Python3
- Increases Memory
- Downloads and launches docker elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Path with docker ps output iamage](Images/docker_ps_out.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _10.0.0.5 and 10.0.0.6_

We have installed the following Beats on these machines:
- _FileBeat and Metric Beat_

These Beats allow us to collect the following information from each machine:
- Filebeat monitors the log files or locations that you specify, collects log events, and fowards them for indexing. It monitors for any type of configuraiton or modification changes. For exmaple if the etc/passwd file has been change there will be a notification sent
- Merticbeat takes the metrics and statistics that it collects and ships them to the output that you specify. For example if a system is being overworked there will be a graphic metric for you to be able to see.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to the ansible container etc/ansible.
- Update the ansible.cfg file to include elk vm. Update Hosts file to include ELK username
- Run the playbook, and navigate to ELK VM to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_ 
- _The playbook are copied to the ansible container and they are as followed:
        [Playbook Files](Playbook_Files/filebeat-config.yml) : Configures Filebeat
        [Playbook Files](Playbook_Files/filebeat-playbook.yml) : Installs Filebeat through ansible
        [Playbook Files](Playbook_Files/install-elk.yml): Installs ELk        
        [Playbook Files](Playbook_Files/metricbeat.yml): Configures Metricbeat
        [Playbook Files](Playbook_Files/pentest.yml): Installs DWVA
        [Playbook Files](Playbook_files/metricbeat-playbook.yml): Installs Metricbeat
        
- _ You must update the ansible.cfg and hosts files in order to specify which playbook in ran on which machine.
ansible.cfg: on line 105 you must add the different remote users that you are using
For example: (remote_user = ansible)
hosts: starting on line 21 is where you update the hosts with there correlating IP Address
For example: [elk]
                      10.1.0.4 ansible_python_interpreter=/usr/bin/python3
- _Which URL do you navigate to in order to check that the ELK server is running?
In order to check to see if your ELK server is running navigate to following IP address (http://ELK-Public-IP-Address:5601/)from the authorized IP Address

To download any of these files copy the following commands within your terminal window:
curl https://raw.githubusercontent.com/quagmirewale/ELK-Stack-Project/Playbook-Files/filebeat-config.yml > filebeat-config.yml
curl https://raw.githubusercontent.com/quagmirewale/ELK-Stack-Project/Playbook-Files/filebeat-playbook.yml > filebeat-playbook.yml
curl https://raw.githubusercontent.com/quagmirewale/ELK-Stack-Project/Playbook-Files/install-elk.yml > install-elk.yml
curl https://raw.githubusercontent.com/quagmirewale/ELK-Stack-Project/Playbook-Files/metricbeat-playbook.yml > metricbeat-playbook.yml
curl https://raw.githubusercontent.com/quagmirewale/ELK-Stack-Project/Playbook-Files/metricbeat.yml > metricbeat.yml
curl https://raw.githubusercontent.com/quagmirewale/ELK-Stack-Project/Playbook-Files/pentest.yml > pentest.yml
