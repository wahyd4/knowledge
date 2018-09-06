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

# Everything is code
- Infrastructure as code
- CI config as code
- Dockerfile

# CD
![OSI Models](https://raw.githubusercontent.com/wahyd4/knowledge-mind-mapping/master/assets/images/iac.png)

## Automation tools

### Capistrano
A ruby tool for deploy applications
### Chef

#### What is chef

Chef enables you to manage and scale cloud infrastructure with no downtime or interruptions. Freely move applications and configurations from one cloud to another. Chef is integrated with all major cloud providers including Amazon EC2, VMWare, IBM Smartcloud, Rackspace, OpenStack, Windows Azure, HP Cloud, Google Compute Engine, Joyent Cloud and others.

Chef running a `chef-client` on each node to be a runner to install applications on remote server. The client can use both `pull` and `push` modes to to communication.

More:
* Chef vs ansible: <https://www.chef.io/ansible/>
### Ansible

#### What is Ansible
Ansible is an IT automation tool. It can configure systems, deploy software, and orchestrate more advanced IT tasks such as continuous deployments or zero downtime rolling updates. Ansible’s goals are foremost those of simplicity and maximum ease of use.

Ansible uses `SSH` to execute commands on remote server and use `RabbitMQ` at the transport level by `push` updates

### Puppet

Is also a configuration management tool for servers and designed to install and manage software on existing servers.

### Packer

Packer is a tool to allows you build a machine image which contains all preinstalled and configged applications.

### Terraform

#### What is Terraform
Terraform use a declarative language to describe the current state of infrastructure, and there is no server side agent installed.

Terraform is more about declare the resources/services requirements, rather than install softwares and libraries on remote server.


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
## git
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
## oh-my-zsh
## IDE/tools
	- Intellij
	- vscode

## Security

#
