Follow information.

1.	Question
Ans; 
To configure the PPA on your machine and install ansible run these commands:
$ sudo apt-get update
$ sudo apt-get install software-properties-common
$ sudo apt-add-repository --yes --update ppa:ansible/ansible
$ sudo apt-get install ansible

Ssh-keygen


sudo vim /etc/ssh/sshd_config

# Change to no to disable tunnelled clear text passwords
PasswordAuthentication yes

sudo service ssh restart

ssh-copy-id  Ipaddress

/etc/ansible$ sudo vi hosts

/etc/ansible$ sudo vi /etc/hostname

To update hostname
sudo init 6


ansible all -m shell -a 'curl -fsSL https://get.docker.com -o get-docker.sh; sh 


get-docker.sh' -b






2. Question 
Ans: 

1). To install node
ansible localhost -m shell -a 'apt install -y nodejs;apt install -y npm' -b

check node 
nodejs -v

2).To install nvm
 ansible localhost -m shell -a 'curl -sL https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh -o install_nvm.sh;sh install_nvm.sh' -b
next
sudo init 6
nvm --version

3).To install docker
ansible localhost -m shell -a 'curl -fsSL get.docker.com -o get-docker.sh;sh get-docker.sh' -b

4) To install docker compsoe
ansible localhost -m shell -a 'sudo curl -L https://github.com/docker/compose/releases/download/1.18.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose ; sudo chmod +x /usr/local/bin/docker-compose' -b


5). To install openssl
ansible localhost -m shell -a 'apt install openssl' -b 

6). To install git
ansible localhost -m apt -a "name=git state=latest update_cache=yes" -b
   













3. question 
Ans:

Treee
.
├── dockercompose
│   ├── docker-compose.yaml
│   └── webapp
│       ├── Dockerfile
│       └── sample.html
├── get-docker.sh
├── playbook.retry
├── playbook.yaml
└── sample.html


3).

sudo vim playbook.yaml
---
 - name: set of tasks
   hosts: localhost
   become: yes
   connection: local
   gather_facts: no
   tasks:
    - name: docker compose
      file:
       name: ./dockercompose
       state: directory
       mode: 0755
    - name: create webapp dir in dc
      file:
       name: ./dockercompose/webapp
       state: directory
       mode: 0755
    - name: git clone
      git:
       repo: https://github.com/satish916/DevOps-Test.git
       clone: yes
       dest: ./dockercompose/webapp   
    - name: change directory
      shell: cd /home/ubuntu/dockercompose;docker-compose build;docker-compose up -d
...


2)Create Dockerfile In webapp:

$cd dockercompose/webapp

$sudo vim Dockerfile

	FROM ubuntu
	RUN apt-get update \
   	&& apt-get install -y apache2
	COPY sample.html /var/www/html/
	WORKDIR /var/www/html
	CMD ["apachectl", "-D", "FOREGROUND"]
	EXPOSE 80

save&quit

3)create docker-compose.yaml in dockercompose dir:
cd /home/ubuntu/dockercompose
sudo vim docker-compose.yaml

	version: '2'
	services:
 	   web:
                         image: apache
    	        build: ./webapp
    	        container_name: apache_web
   	        restart: always
    	        ports:
      	            - "8080:80"
save&quit










