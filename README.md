Multi-VM Automated Web Deployment 
This project demonstrates the automation of a multi-server web environment using Vagrant for Infrastructure as Code (IaC) and Bash Scripting for configuration management.

 Architecture
Management Node (scriptbox): CentOS Stream 9 - Used to host scripts and manage the environment.

Web Nodes (web01, web02, web03): Mixed environment (CentOS & Ubuntu) to simulate a real-world heterogeneous data center.

Networking: Private host-only network (192.168.56.0/21).

 Tech Stack
Virtualization: VirtualBox

Orchestration: Vagrant

Scripting: Bash (Shell)

Web Server: Apache (httpd)

Deployment: Automated artifact fetching via wget and unzip.

 How to Run
Clone the repository.

Ensure VirtualBox and Vagrant are installed.

Run vagrant up to provision the VMs.

Access the web server at http://192.168.56.10.

 Challenges & Solutions
1. VirtualBox Host-Only Network Restrictions
Issue: VirtualBox blocked the initial 192.168.10.x range due to security policies on Linux hosts.
Solution: Adjusted the Vagrantfile to use the allowed range (192.168.56.x) and ensured /etc/vbox/networks.conf was configured to permit the traffic.

2. Deployment Script Optimization
Issue: Manual deployment was prone to human error (pathing and permissions).
Solution: Developed websetup.sh to automate:

Installing dependencies (httpd, wget, unzip).

Setting up systemd services.

Deploying web artifacts from a remote ZIP template.

Cleaning up temporary files to maintain a slim OS footprint.

 Bash Script Preview
Bash
# Automated artifact deployment snippet
mkdir -p /tmp/webfiles
cd /tmp/webfiles
wget $URL
unzip $FILE.zip
sudo cp -r $FOLDER/* /var/www/html/
