# ELK-Stack-Project1
UCI Cybersecurity boot camp ELK Stack project
![TODO: Update the path with the name of your diagram](Photos/Project1_Diagram.PNG) https://github.com/rickchau90/ELK-Stack-Project1/blob/main/Project1_Diagram.PNG


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the __project1-playbook.zip___ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file. https://drive.google.com/drive/folders/1l3takQvVMBe5_HnRiC0JpQBCV1VJ3mvV?usp=sharing
This document contains the following details:
- Description of the Topology- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly ___available__, in addition to restricting __traffic___ to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box? Load balancers ensure that access to servers are protected by managing the amount of traffic going to servers so that one server isn’t overwhelmed by traffic and slowed down.  The advantage of a jumpbox is that administrators can make changes to webservers remotely on another secure domain that doesn’t have open connections to the internet.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- _TODO: What does Filebeat watch for?_ Filebeat collects and watches information on log files including changes made to files and when they were changed. 
- _TODO: What does Metricbeat record?_ Metricbeat records metric data for different services. An example of what Metricbeat might record is how frequently a service is used. 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name       | Function          | IP Address    | Operating System |
|------------|-------------------|---------------|------------------|
| Jumpbox    | Gateway           | 172.31.88.180 | Linux            |
| Webserver1 | Webserver         | 172.31.91.143 | linux            |
| Webserver2 | Webserver         | 172.31.28.86  | linux            |
| ELK server | Packet monitoring | 172.31.17.128 | Ubuntu           |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only  __webserver 1 and 2___ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_ 
ICMP- all IPv4
Port 5044: all IPv4
Port 9200: all IPv4
Port 5601: all IPv4
Port 80: all IPv4
SSH: 172.31.88.180/32, 45.51.19.33/32


Machines within the network can only be accessed by _____.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_ Only the Jumpbox/Ansible server has access to the ELK VM
IP Address: 172.31.88.180
A summary of the access policies in place can be found in the table below.
| Name            | Publicly Accessible | Allowed IP addresses |
|-----------------|---------------------|----------------------|
| Jumpbox/Ansible | no                  | 45.51.19.33          |
| Webserver 1     | yes                 | 172.31.88.180        |
| Webserver 2     | yes                 | 172.31.88.180        |
| ELK Server      | no                  | 172.31.88.180        |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_
The main advantage of automating configuration with Ansible is scalability because automation allows us to efficiently create identical servers to control data traffic.
The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Install these services onto all servers under elk group listed in host file
- install docker.io
- increase virtual memory 
- Install docker python module
- download and launch a docker web container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.


![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png) https://github.com/rickchau90/ELK-Stack-Project1/blob/main/Project1-dockerps%20(2).PNG

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
Webserver 1: 172.31.91.143
Webserver 2: 172.31.28.86

We have installed the following Beats on these machines:
Webserver 1 and Webserver 2
- _TODO: Specify which Beats you successfully installed_
Metricbeat 
filebeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

Metricbeat collects different metrics on services for example Docker metrics fetches metrics from your docker containers. 
Filebeat collects logs from different log files for example Apache logs collects access and error logos created by the apache HTTP server

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy filebeat-playbook.yml and metricbeat-playbook.yml file to _/etc/ansible____.
- Update the __config file___ file to include the ELK server IP address
- Run the playbook, and navigate to the ELK GUI to check that the installation worked as expected. Navigate to system logs and docker container metrics and click on check data to see if the server is working properly

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_ playbook files list out a series of actions whereas configuration files are used to indicate services should be created.
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ update the playbook file to specify which machines to run the playbook on. This is done by changing hosts to match the correct group and remote_user to match the user id of that machine
- _Which URL do you navigate to in order to check that the ELK server is running?
Navigate to your ELK public IP on its open port (in this case port 5601) to see if the the app is running.
_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
