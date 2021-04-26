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


## First Run

The first time the sever was spun  up, an AWS EC2 Ubuntu Bionic Instance was used.

The plan for the future is to likely write a script to automate the set up for the future, but for this machine, the following steps were taking for setting up the VM, after creeating an ssh connection with the VM:
 - Downloaded and installed Docker Engine using ssh (Not something to do for production due the risks of running a foreign script on your computer/server)

 - Downloaded and installed Docker-Compose (version 3.0+ for bionic build)

 - Created a portainer instance to help manage the containers

 - Create a user-defined network for docker

 - Copy & Paste the docker-compose.yml using nano (In the future, include a script to curl from GitHub)

 - Spin up docker-compose

From here,  the AWS Security Group's firewall rules were edited to only allow access to port 80, 443, and 22 (for http, https, and ssh rescpectively).

About a year ago, 'retanatech.com' domain name was purchased. 'retanatech.com' will be used for this VM instance. 

AWS allows users to reserve "Elastic IPs". This will allow the EC2 instance to be shutdown and started up again, while maintaining the same IP. Without it, the EC2 instance receives a new Public IP address each time its spun up.

'retanatech.com' was set to point to the Elastic IP

By putting "retanatech.com:81" into the address bar, the Nginx Proxy Manager (NPM) web interface can be reached. For the first time being accessed, it will request an admin username and passwork be added.

After creating credentials, this first proxy to set up was to point to NPM itself. The subdomain 'npm.retanatech.com' was set to point to 'npm_app_1:81'. The name 'npm_app_1' is able to be used as a hostname within the docker bridge docker, which is pretty convenient.

Next, a proxy was added the portainer page. 'portainer.retanatech.com' was set to point to 'portainer:9000'. Prior to this proxy set up, to access the page, port 9000 was left open on the VM's security group rules (port 9000 on docker host work forward to port 9000 in portainer container). Now, with the proxy set up, port 9000 can be closed on the host, and Nginx can send requests within it's localhost, making the communication more secure.

To up the security of the communication, a SSL certification was added for SSL encryption, using NPM's Let's Encrypt integrated capabilities. Route 53 was used for issuing the cert, and only was cert was used; it was assigned to the wildcard "*.retanatech.com" so that any site going through proxy will require a SSL handshake to open a connection.