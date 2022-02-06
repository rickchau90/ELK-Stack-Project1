![project1-diagram](https://user-images.githubusercontent.com/84049611/152666248-184f17ac-dbd8-42b3-84c8-575466d365a4.PNG)
# ELK-Stack-Project1
UCI Cybersecurity boot camp ELK Stack project
(Photos/Project1_Diagram.PNG) https://github.com/rickchau90/ELK-Stack-Project1/blob/main/Project1_Diagram.PNG

These files have been tested and used to generate a live ELK deployment on AWS cloud. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the project1-playbook.zip file may be used to install only certain pieces of it, such as Filebeat.

  - https://drive.google.com/drive/folders/1l3takQvVMBe5_HnRiC0JpQBCV1VJ3mvV?usp=sharing
This document contains the following details:
- Description of the Topology- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to create a load-balanced and monitored HTTPd/Apache2 application server.

Load balancing ensures that the application will be highly available, in addition to maintaining traffic flow going to servers.
Load balancers improve performance by managing traffic flow going into each server to make sure they all receive the same or similar workload. This scenerio is considered an active/active load balancing. The jumpbox server acts as a DMZ (demilitarized zone) which is an intermediary between the public internet and internal network. The jumpbox server makes it possible to make remote changes to the internal network without having to make a direct connection to the internal network via the internet.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the metrics and system logs.
Filebeat collects and watches information on log files including changes made to files and when they were changed. 
Metricbeat records metric data for different services. An example of what Metricbeat might record is how frequently a service is used. 

The configuration details of each machine may be found below.
Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name       | Function          | IP Address    | Operating System |
|------------|-------------------|---------------|------------------|
| Jumpbox    | Gateway           | 172.31.88.180 | Linux            |
| Webserver1 | Webserver         | 172.31.91.143 | linux            |
| Webserver2 | Webserver         | 172.31.28.86  | linux            |
| ELK server | Packet monitoring | 172.31.17.128 | Ubuntu           |


### Access Policies

The ELK server and jumpbox server are on the internal network and are not exposed to the public Internet. For security reasons, connection to these servers are only allowed through SSH. 

Only  webserver 1 and 2 machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

ICMP- all IPv4

Port 5044: all IPv4

Port 9200: all IPv4

Port 5601: all IPv4

Port 80: all IPv4

SSH: 172.31.88.180/32, 45.51.19.33/32

Machines within the network can only be accessed by the ansible server.
The Ansible server allows for remote access to the webservers to make any changes to configuration. 
IP Address: 172.31.88.180
A summary of the access policies in place can be found in the table below.

| Name            | Publicly accessible | Allowed IP addresses |
|-----------------|---------------------|----------------------|
| Jumpbox/Ansible | no                  | 45.51.19.33          |
| Webserver 1     | yes                 | 172.31.88.180        |
| Webserver 2     | yes                 | 172.31.88.180        |
| ELK server      | no                  | 172.31.88.180        |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. 
The main advantage of automating configuration with Ansible is scalability because automation allows us to efficiently create identical servers to control data traffic.
The playbook implements the following tasks:
- Install these services onto all servers under elk group listed in host file
- install docker.io
- increase virtual memory 
- Install docker python module
- download and launch a docker web container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
![Project1-dockerps (2)](https://user-images.githubusercontent.com/84049611/134743990-4a68475b-8107-4b93-bbf3-a48bee2089ec.PNG)
(Images/docker_ps_output.png) https://github.com/rickchau90/ELK-Stack-Project1/blob/main/Project1-dockerps%20(2).PNG

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
List the IP addresses of the machines you are monitoring_
Webserver 1: 172.31.91.143
Webserver 2: 172.31.28.86

We have installed the following Beats on these machines:
Webserver 1 and Webserver 2
Specify which Beats you successfully installed_
Metricbeat 
filebeat

These Beats allow us to collect the following information from each machine:

Metricbeat collects different metrics on services for example Docker metrics fetches metrics from your docker containers. 
Filebeat collects logs from different log files for example Apache logs collects access and error logos created by the apache HTTP server

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy filebeat-playbook.yml and metricbeat-playbook.yml file to _/etc/ansible____.
- Update the __config file___ file to include the ELK server IP address
- Run the playbook, and navigate to the ELK GUI to check that the installation worked as expected. Navigate to system logs and docker container metrics and click on check data to see if the server is working properly

Playbook files list out a series of actions whereas configuration files are used to indicate services should be created. Copy the playbook files into the ansible server because the ansible server also holds all of the configuration files that are used when running a playbook.
In order to make ansible run a playbook on a specific machine, update the playbook file to specify which machines to run the playbook on. This is done by changing hosts to match the correct group and remote_user to match the user id of that machine
Navigate to your ELK public IP on its open port (in this case port 5601) to see if the the app is running.

Some important docker commands

sudo docker start (start the container)

sudo docker attach (connect to the container)

docker container list -a (shows list of containers on the machine)

sudo docker cp KEYFILE.pem <container name>:/destination path (copies key to container to folder destination)
  

Some important ansible commands
  
  ansible -m ping all --key-file KEYFILE.PEM (pings all servers created with KEYFILE.PEM)
  
  ansible-playbook -i hosts PLAYBOOK.YML --key-file KEYFILE.pem (runs playbook file to all servers with KEYFILE.pem)
