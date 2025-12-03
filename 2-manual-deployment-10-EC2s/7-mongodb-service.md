# Install database service (MongoDB application)

## Launch an EC2 instance with a Security Group

1. launch an EC2 instance:
    create a security group with inbound rules to allow ssh access and catalogue application.
    launch VM with the security group.

2. set hostname (Optional):
    hostnamectl set-hostname mongodb

3. update the packages:
    sudo dnf update -y

### Setup MongoDB repository

1. create a repository file named 'mongodb-org-7.0.repo':
    sudo vi /etc/yum.repos.d/mongodb-org-7.0.repo

2. repository content:

[mongodb-org-7.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/amazon/2023/mongodb-org/7.0/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-7.0.asc

### Install Mongo , mongosh & Start Service

1. Install MongoDB:
    dnf install -y mongodb-org

2. Enable MongoDB:
    systemctl enable mongod

3. Start MongoDB:
    systemctl start mongod

4. Remove any dependencies related to mogosh:
    rpm -e --nodeps mongodb-mongosh

5. Install mogosh:
    dnf install mongodb-mongosh-shared-openssl3.x86_64 -y

### configuration

1. Update ip address from '127.0.0.1' to '0.0.0.0' in mongo configuration file '/etc/mongod.conf'. Otherwise, it will work with loopback ip and listen on same host:
    sudo vi /etc/mongod.conf

2. Restart mongodb to load the new configuration change:
    systemctl restart mongod

### Download the application content and load to the database

1. Download database schema (data/content):
    curl -s -L -o /tmp/mongodb.zip <https://github.com/rshaik4devops/mongodb/archive/main.zip>

2. Change working directory to downloaded location:
    cd /tmp

3. Unzip downloaded zip file:
    unzip mongodb.zip

4. Change working directory to unarchived directory:
    cd mongodb-main

5. load catalogue & user schema:
    mongosh < catalogue.js
    mongosh < users.js
