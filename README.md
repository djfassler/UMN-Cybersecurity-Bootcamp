# UMN-Cybersecurity-Bootcamp
Compilation of work produced in the UMN Cybersecurity Bootcamp program June - December 2020
The files in this repository were used to configure the network depicted below.
​
https://drive.google.com/file/d/1CPHlxBcG4srzMrEPU_KVp_1ydhyvAzxU/view?usp=sharing
​
These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the pentest.yml file may be used to install only certain pieces of it, such as Filebeat.
​
 Pentest.yml
 ---- 
  name: Config Web VM with Docker  
  hosts: webservers  
  become: true  
  tasks:  
  - name: docker.io    
    apt:      
      update_cache: yes      
      name: docker.io      
      state: present  
  - name: Install pip3    
    apt:      
      name: python3-pip      
      state: present  
  - name: Install Docker python module    
    pip:      
      name: docker      
      state: present  
  - name: download and launch a docker web container    
    docker_container:      
      name: dvwa      
      image: cyberxsecurity/dvwa      
      state: started
      restart_policy: always      
      published_ports: 80:80  
  - name: Enable docker service    
    systemd:      
      name: docker      
      enabled: yes
​
This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build
​
​
### Description of the Topology
​
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
​
Load balancing ensures that the application will be highly available in addition to restricting unauthorized access to the network.
-Load balancers help ensure high availability by preventing one system server from being overloaded with service requests.  Load balancers are configured from the Jump Box Provisioner to the Docker VMs.  Load balancers can also be configured directly from the firewall.  Both configurations ensure accessibility while minimzing intrusion risk to the network.
​
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system statistics.
-Filebeat is a lightweight shipper for forwarding and centralizing log data.  Filebeat monitors specified log files or locations, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
-Metricbeat is a Lightweight shipper for system metrics (statistics) for both the system and services.  

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.
​
| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.10  | Linux            |
| Web-1    | Docker   | 10.0.0.18  | Linux            |
| Web-2    | Docker   | 10.0.0.19  | Linux            |
| Web-3    | Docker   | 10.0.0.5   | Linux            |
​
### Access Policies
​
The machines on the internal network are not exposed to the public Internet. 
​
Only the Jump Box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 73.94.14.170
Machines within the network can only be accessed by other VMs on the network configured for access.  .
-Access from the Jump Box Provisioner (10.0.0.10) and the stoic_elion anisble container access to the Elk-Server (10.1.0.4) can be established by secure shell.
​
A summary of the access policies in place can be found in the table below.
​
| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 10.0.0.10            |
| Web-1    | No                  | 10.0.0.18            |
| Web-2    | No                  | 10.0.0.19            |
| Web-3    | No                  | 10.0.0.5             |
| ELK      | Yes                 | 10.1.0.4             |
​
### Elk Configuration
​
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The main advantage of automating ansible configuration is that you can configure multiple individual containers with a single configuration action.
​
The playbook implements the following tasks:
- Configure ELK VM with Docker - User=Sysadmin
- Configure Elk VM With Docker - Install Docker.io
- Configure ELK VM with Docker - Install Pip3, Use Pip3
- Configure ELK VM with Docker - Sysctl, use more memory
- Configure ELK VM with Docker - Use docker container, download and launch docker elk container
- ...
​
The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
​
![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)
​
### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.18
- 10.0.0.19
​
We have installed the following Beats on these machines:
- Web-3 VM (10.0.0.5) - Kibana, Elasitisearch 
​
These Beats allow us to collect the following information from each machine:
- Filebeats collects log files from the server
- 
​
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 
​
SSH into the control node and follow the steps below:
- Copy the hosts file to Elk-Server (10.1.0.5).
- Update the hosts file to include Elk Server
- Run the playbook, and navigate to ____ to check that the installation worked as expected.
​
- The Ansible playbook is pentest.yml found in JumpBoxSysadmin@Jump-Box-Provisioner:/etc/ansible/pentest.yml
- The updated file to make Ansible run the playbook on specific machines is the Hosts file.   Under ELk the host would specific 10.1.0.4 and Filebeat is installed on 10.0.0.5
- Testing the accessiblitly of the ELK server is 52.165.238.25
​
_
