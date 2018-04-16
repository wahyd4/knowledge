# AWS
- EC2
- EC2 container
- Cloudfront
- S3
- RDS

# CI
- Jenkins
- Gitlab CI
- Travis

# Linux
- ssh
- IP table
- Cron job
- ps aux
- tail
- nohup
- df -h
- free
- Tips
	- Change timezone
		- TZ=Asia/Shanghai;ln -snf /usr/share/zoneinfo/$TZ /etc/localtime
	- Check release
		- cat /etc/*-release
- Packages
	- htop
		- like top, but more
	- mosh
		- auto reconnect ssh

# Everything is code
- Infrastructure as code
- CI config as code
- Dockerfile

# CD
![OSI Models](https://raw.githubusercontent.com/wahyd4/knowledge-mind-mapping/master/assets/images/iac.png)
## Capistrano
## Ansible
## Puppet
## Terraform

Terraform use a declarative language to describe the current state of infrastructure, and there is no server side agent installed.

### Basic steps
```bash
# go to the folder which stores the environment credentials
terraform init # Initialize a new or existing Terraform working directory by creating initial files, loading any remote state, downloading modules, etc.
terraform get # Downloads and installs modules that defined by configuration files
terraform plan # Kind of try run, you will what kind of changes you will have
terraform apply # Apply changes to cluster
```

# HA High Availability
- LB - haproxy
- Keepalived -- vrrp
	- Nginx + Keepalived
- Heartbeat

# Network
- IP
	- Private IP Addresses
		- 10.0.0.0 – 10.255.255.255
		- 172.16.0.0 – 172.31.255.255
		- 192.168.0.0 – 192.168.255.255

## OSI Model( 7 layers network)

![OSI Models](https://raw.githubusercontent.com/wahyd4/knowledge-mind-mapping/master/assets/images/osi-model.png)
# tools
- git
	- cherrypick
	- rebase
	- commit
	- checkout
		- checkout -b br com
	- push
		- --tags
			- push tags
		- —all
			- push all branchs
		- -f
			- force push
	- branch -d xx
		- delete a local branch
	- remote
		- show xxx
			- show info of a remote branch
		- add xxx
			- add a remote repo
	- branch
		- list all the branchs
	- mv Rename/move files and folder with git history records

      e.g. git mv -k ./a/b ./c/d   option `k` would avoid the "can not move directory into itself" error.
- oh-my-zsh
- IDE/tools
	- Intellij
	- vscode