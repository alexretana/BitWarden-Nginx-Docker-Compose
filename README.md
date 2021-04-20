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

I'll likely write a script to automate the set up for the future, but for this machine,
I essentially did the following after making an ssh connection to the VM:

 - Downloaded and installed Docker Engine using ssh (Not something to do for production due the risks of running a foreign script on your computer/server)

 - Downloaded and installed Docker-Compose (version 3.0+ for bionic build)

 - I created a portainer instance to help manage the containers

 - Copy & Paste the docker-compose.yml using nano (In the future, include a script to curl from GitHub)

 - Spin up docker-compose

 From here