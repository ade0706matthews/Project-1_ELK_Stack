## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
## Links to Project Images
# Topology 
![Diagram](https://github.com/ade0706matthews/Project-1_ELK_Stack/tree/master/Diagrams)

# Project screenshots (Google Drive) 
![Project_screenshot] https://github.com/ade0706matthews/Project-1_ELK_Stack/tree/master/Ansible


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the __install-elk.yml__ file may be used to install only certain pieces of it, such as Filebeat.


- Description of the Topology
- Access Policies
- ELK Configuration
- Beats in use: Filebeat and metricbeat
- Machines Being Monitored: Web-1 and Web-2
- How to Use the Ansible Build
# 
### Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
# 
### Load Balancer
Load balancing ensures that the application will be highly __distributed and resilient__, in addition to restricting __unwanted traffic__ to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?
    __Specifically, load balancers distributes traffic and mitigates against Denial of Service attack__
    __The Jump-Box controls access to other virtual machines that are not exposed to the internet and reduces risk of having the network breached__

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files and system logs.
- What does Filebeat watch for?_
__Filebeat monitors the log files or locations that you specify and collects log events.__

- _TODO: What does Metricbeat record?_
__Metricbeat periodically collect metrics from the operating system and from services running on the server.__

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name                | Function    | IP Address | Operating System   |
|---------------------|-------------|------------|--------------------|
| Jump-Box-Provisioner| Gateway     | 10.0.0.4   | Linux Ubuntu 18.04 |
| Web-1               | Web App     | 10.0.0.5   | Linux Ubuntu 18.04 |
| Web-2               | Web App     | 10.0.0.6   | Linux Ubuntu 18.04 |
| Elk-VM              | Log Server  | 10.1.0.4   | Linux Ubuntu 18.04 |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the __Jump-Box-Provisioner__ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:  
- __The whitelisted IP addresses are my personal home IP: 98.197.135.197__


Machines within the network can only be accessed by Jump-Box via SSH
- Which machine did you allow to access your ELK VM? What was its IP address?_
- __Jump-Box=Provisioner: 104.43.170.0 (public), 10.0.0.4 (private) via SSH__

The Load Balancer allows traffic from ther internet via port 80
A summary of the access policies in place can be found in the table below.

| Name           | Publicly Accessible | Allowed IP Addresses   |
|----------------|---------------------|------------------------|
| Jump Box       | Yes                 | Home IP: 98.197.135.197|         
|  Web-1         | No                  | 10.0.0.5               |
|  Web-2         | No                  | 10.0.0.6               |
| Load Balancers | Yes                 | 40.83.17.93            |
| ELK-VM         | Yes                 | Home IP: 98.197.135.197|

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. 
__No configuration was performed manually, which is advantageous because the Jump-Box could be used to install and configure the machine__
- _What is the main advantage of automating configuration with Ansible? The main advantage is that you can use commands to provision from a playbook
__Instead of ssh'ing into all the different VMs, you can just use the jump box to install and configure all the machines__


The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- __Install docker.io__
- __Install python-pip__
- __Install docker__
- __sysctl module to expand/use more memory__
- __Download and launch the docker container ELK__

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![DockerPS](https://github.com/ade0706matthews/Project-1_ELK_Stack/blob/master/Ansible/ps_docker_1.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
  - __Web-1: 10.0.0.5__
  - __Web-1: 10.0.0.6__

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
  - __Filebeat__
  - __Metricbeat__

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
  - __Filebeat is used for collecting and shipping audit log files, which tracks for example, opening a file, and starting or killing a process. These logs can be used to monitor servers/systems for suspicious activity.__
  - __Metricbeat  collects and reports various system-level metrics for various systems and platforms.__

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the __filebeat-config__ file to __/etc/ansible/__ directory of the control node machine on which ansible container in running.
- Update the __host line within the config file__ to include __ELK-server private IP__
- Run the __playbook__, and navigate to __Kibana filebeat page__ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? __filebeat.yml__ 
- Where do you copy it? File was copied to __/etc/filebeat/filebeat.yml__ 
- _Which file do you update to make Ansible run the playbook on a specific machine? __Configuration file__ How do I specify which machine to install the ELK server on versus which to install Filebeat on? __the machine IPs are edited in the host file__
- _Which URL do you navigate to in order to check that the ELK server is running?
  - __http://[Elk_IP]:5601/app/kibana__

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.
 - __ssh azadmin@104.43.170.0__
 - __ssh-keygen__
 - __curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > filebeat-configuration.yml__
 - __curl https://gist.githubusercontent.com/slape/58541585cc1886d2e26cd8be557ce04c/raw/0ce2c7e744c54513616966affb5e9d96f5e12f73/metricbeat > metricbeat-config.yml__
 - __sudo su__
 - __Docker start flamboyant_clarke__
 - __Docker attach flamboyant_clarke__
 - __nano filebeat-configuration.yml__
 - __nano metricbeat-config.yml__
 - __nano install-elk.yml__
 - __nano filebeat-playbook.yml__
 - __nano metricbeat.yml__
 - __ansible-playbook install-elk.yml__
 - __ansible-playbook filebeat.yml__
 - __ansible-playbook metricbeat.yml__
