# BitWarden-Nginx-Docker-Compose


## Purpose
Security is an increasingly significant issue over the internet, which only got push forward by the effects of Covid pushes many work forces to remote operations. 

It is important to manage various passwords for the various personal accounts most people create to have access to a plethora of online application. There are services that help manage your passwords over a cloud network. This means you're trusting this service to hold and protect your password. Also, these servcies aren't free for a full line of features.

If these site have a breach, your data will be exposed, which is less than favorable outcome. For this reason, I've decided to go through the process of setting up a bitwarden_rs server on a Cloud VM.

This project is both to solve my password management for free, but also to learn how to host a service like this in a secure manner.

## Tools

- Docker
- Docker-Compose
- [Nginx Proxy Manager](https://nginxproxymanager.com/)
- [BitWardenRS/Server](https://hub.docker.com/r/bitwardenrs/server)
- AWS EC2 Ubuntu Bionic Instance



The first time the sever was spun  up, an AWS EC2 Ubuntu Bionic Instance was used.

The plan for the future is to likely write a script to automate the set up for the future, but for this machine, the following steps were taking for setting up the VM, after creeating an ssh connection with the VM:
 - Downloaded and installed Docker Engine using ssh (Not something to do for production due the risks of running a foreign script on your computer/server)

 - Downloaded and installed Docker-Compose (version 3.0+ for bionic build)

 - Created a portainer instance to help manage the containers

 - Copy & Paste the docker-compose.yml using nano (In the future, include a script to curl from GitHub)

 - Spin up docker-compose

From here,  the AWS Security Group's firewall rules were edited to only allow access to port 80, 443, and 22 (for http, https, and ssh rescpectively).

About a year ago, 'retanatech.com' domain name was purchased. 'retanatech.com' will be used for this VM instance. 

AWS allows users to reserve "Elastic IPs". This will allow the EC2 instance to be shutdown and started up again, while maintaining the same IP. Without it, the EC2 instance receives a new Public IP address each time its spun up.

'retanatech.com' was set to point to the Elastic IP