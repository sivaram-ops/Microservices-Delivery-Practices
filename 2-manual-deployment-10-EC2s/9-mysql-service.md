# MySQL Database as Microservice

## Launch an EC2 instance for shipping service with a Security Group

1. Launch an EC2 instance:
    create a security group with inbound rules to allow ssh access and catalogue application.
    launch VM with the security group.

2. Set hostname (Optional):
    hostnamectl set-hostname mysql

3. Update the packages:
    sudo dnf update -y

## MySQL 5.7 Installation

dnf update -y

1. Setup the necessary repository:
method 1: To install repository package directly with an URL.
rpm -uvh https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm

method 2: To download the repository package:
wget https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
to install the downloaded repository package:
option 1: rpm -uvh mysql57-community-release-el7-11.noarch.rpm (or) yum localinstall mysql57-community-release-el7-11.noarch.rpm -y
option 2: dnf install mysql57-community-release-el7-11.noarch.rpm -y

Previous steps: (commented as not required)
#1. Add the MySQL 5.7's rpm (as the root user):
#A release package that sets up the necessary repositories
#rpm -Uvh <https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm>
#(or)
#wget <https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm>
#yum localinstall mysql57-community-release-el7-11.noarch.rpm -y

2. rpm --import <https://repo.mysql.com/RPM-GPG-KEY-mysql-2022> (optional)
#https://repo.mysql.com/RPM-GPG-KEY-mysq

3. install mysql:
dnf install mysql-community-server -y

4. enable mysql:
    systemctl enable mysqld

5. start mysql:
    systemctl start mysqld
    systemctl status mysqld

6. find the default password in the log, using grep:
    grep temp /var/log/mysqld.log
    grep 'temporary password' /var/log/mysqld.log
output:
2025-10-08T10:07:21.677077Z 1 [Note] A temporary password is generated for root@localhost: wIue5dGPpx&z
2025-10-08T10:07:24.587728Z 0 [Note] InnoDB: Creating shared tablespace for temporary tables

7. To change the default password:
    mysql_secure_installation
    Set new password to: 'RoboShop@1',

8. Launch mysql, to verify the new password:
    mysql -u root -p

9. Run the following SQL command to remove the 'password policy':
    > uninstall plugin validate_password;
    answer 'y' to questions like remove anonymous users, disallow remote root login, remove test database, reload privilege tables.

### Load the application schema to MySQL

1. download the schema from the github repository:
    curl -s -L -o /tmp/mysql.zip <https://github.com/rshaik4devops/mysql/archive/main.zip>

2. change directory to tmp:
    cd /tmp

3. unzip:
    unzip mysql.zip

4. change directory to unzipped folder:
    cd mysql-main

5. Load the schema:
    mysql -u root -p < shipping.sql
    #password: RoboShop@1
