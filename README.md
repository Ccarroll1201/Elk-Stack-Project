### Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

******DIAGRAM

The following files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select portions of the Ansible Playbook files may be used to install only certain pieces of it, such as Filebeat.

******LINK TO PLAYBOOK FILE

This document contains the following details:
-Description of the Topology
-Access Policies
-ELK Configuration
  - Beats in Use
  - Machines Being Monitored
-How to use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly reliable, in addition to assisting with potential security risks. 
-The off-loading function of a load balancer helps defend the network against distributed denial of service (DDoS) attacks. This is accomplished by shifting attack traffic across multiple servers.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the machines files and system metrics. 
-Filebeat generates and organizes log files to send to Logstash and Elasticsearch.  Specificly, it logs information about the file system, including which files have changed and when. 
-Metricbeat periodically collects metrics form the operating system and from services running on your server.  Metricbeat takes the metrics and statistics collected and sends them to the specified output, such as Elasticsearch or Logstash. 

The configuration details of each machine may be found below.

| Name       	| Function       	| IP Address              	| OS    	|
|------------	|----------------	|-------------------------	|-------	|
| Jump Box   	| Gateway        	| 10.0.0.7 20.88.22.247   	| Linux 	|
| Web-1      	| DVWA Container 	| 10.0.0.5 20.88.5.211    	| Linux 	|
| Web-2      	| DVWA Container 	| 10.0.0.6 20.88.5.211    	| Linux 	|
| ELK Server 	| Config VM      	| 10.1.0.4 40.121.138.127 	| Linux 	|

| Applications Used   |
|-------------------  |
| Docker              |
| Ansible             |
| Filebeat            |
| Metricbeat          |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from my personl machines IP address: 174.20.144.15

Machines within the network (including the ELK server) can only be accessed by the Jump Box (10.0.0.7).

A summary of the access policies in place can be found in the table below.

| Name       	| Publicly Accessible 	| Allowed IP Addresses 	|
|------------	|---------------------	|----------------------	|
| Jump Box   	| No                  	| 174.20.144.15        	|
| Web-1      	| No                  	| 10.0.0.7             	|
| Web-2      	| No                  	| 10.0.0.7             	|
| ELK Server 	| No                  	| 10.0.0.7             	|

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because this process speeds up deployment with automation and allows for quick reproduction of new machines within the network.  Ansible playbooks can be run on a specific machine or large groups of machines within the network.

The playbook implements the following tasks:
-The 'hosts' option specifies that the tasks within the playbook should only be run on the machines in the `elk` group.
-Installs the 'apt' packages: 'docker.io' the Docker engine used for running containers, and 'python3-pip' the package used to install Python software.
-Configures the target VM to use more memory. The ELK container will not run without this setting.
-Downloads the Docker container called 'sebp/elk:761'. 'sebp' is the organization that made the container. 'elk' is the container and '761' is the version.
-Enables the 'docker' service on boot. If the ELK VM is restarted, the docker service will start up automatically.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
*********ADD screenshot


### Target Machines & Beats

The ELK server is configured to monitor the following machines:
-Web-1 (10.0.0.5)
-Web-2 (10.0.0.6)

The following Beats were successfully installed and cofigured:
-Filebeat
-Metricbeat

Filebeat and Metricbeat allow us to collect the following information from each machine:
-Filebeat can send audit logs, depreciation logs, garbage-collection logs, server logs, and slow logs.
*****screenshot
-Metricbeat is used to capture system information and monitor performance.  For example, Metricbeat can be used to monitor and analyze system CPU and memory usage.
*****screenshot

### Using the Playbook
In order to use the playbook, an Ansible control node must already be configured. Assuming such a control node is provisioned: 

SSH into the control node and follow the steps below:
-Navigate to /etc/ansible/playbooks/
-Run the command `curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > filebeat-config.yml`
-Update the hosts file to include the private IP addresses of the ELK and Web servers.  The host names must match in the ansible playbook file for the installation to be directed to the proper machines in the network.
-Run the playbook with the command `ansible-playbook filebeat-playbook.yml` and navigate to Kibana to confirm the installation worked as expected. http://40.121.138.127:5601/app/kibana#/home
-Follow the same steps to configure and install Metricbeat.