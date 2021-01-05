## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

File path for my topology diagram:

- /Desktop/Images/Elk Project Topology.io

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

- ansible-playbook install_elk.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available and reliable, in addition to restricting inbound access to the network.
- The load balancer ensures that work to process incoming traffic will be shared by both vulnerable web servers. Access controls will ensure that only authorized users — namely, ourselves — will be able to connect in the first place.
- The advantage of a Jump Box is that all traffic is going through a single node(single entry point), so you can focus on securing that one interaction between the routers rather than connections between all the machines in the topology above.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file systems of the VMs on the network and system data.

- Filebeat monitors the log files you specify, collects the log events and forwards them to Elasticsearch or Logstash.
- Metricbeat records the metrics and statistics that it collects and ships them to the output that you specify such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.

| Name     | Function  | IP Address | Operating System |
|----------|-----------|------------|------------------|
| Jump Box | Gateway   | 10.0.0.1   | Linux            |
| Web 1a   | V.M       | 10.0.0.7   | Linux            |
| Web 2a   | V.M       | 10.0.0.8   | Linux            |
| Elk-VM   | Monitoring| 10.1.0.4   | Linux            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

- My localhost IP address

Machines within the network can only be accessed by each other.

- Web 1a(10.0.0.7)and Web 2a(10.0.0.8)VMs can access the Elk VM.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | My Localhost IP      |
| Web 1a   | No                  | 10.0.0.7             |
| Web 2a   | No                  | 10.0.0.8             | 
| Elk-VM   | No                  | 10.1.0.4             |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The main advantage of automating configurations with ansible is speed and efficiency which removes the drudgery from daily tasks and human error.

The playbook implements the following tasks:

- Installs Docker.io
- Install Python3-pip
- Downloads and Launches the docker Elk container
- Installs Docker Python Module
- Instructs to use more memory & Uses virtual memory

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

- /Desktop/Images/docker_ps_output.png


### Target Machines & Beats

This ELK server is configured to monitor the following machines:

- 10.0.0.7
- 10.0.0.8

We have installed the following Beats on these machines:

- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:

- Filebeat: detects changes to the filesystem. Specifically, we use it to collect Apache logs.
- Metricbeat: detects changes in system metrics, such as CPU usage. We use it to detect SSH login attempts, failed sudo escalations, and CPU/RAM statistics.


### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. We use the Jump Box for this purpose. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to the Ansible control node.
- Update the playbook file to include the appropriate targets.
- Run the playbook, and navigate to kibana to check that the installation worked as expected.

- Update the Hosts file inorder to specify which machines to install the ELK server on versus which to install Filebeat on.
- Go to http://10.1.0.4:5601 to check that the Elk server is running.
