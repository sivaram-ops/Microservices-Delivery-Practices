# User service (NodeJS application)

This Microservice provides user accounts login and registrations functionality in the RoboShop website.

## Launch an EC2 instance for user service with a Security Group

1. Launch an EC2 instance:
    create a security group with inbound rules to allow ssh access and catalogue application.
    launch VM with the security group.

2. Set hostname (Optional):
    hostnamectl set-hostname user

3. Update the packages:
    sudo dnf update -y

## Install Nodejs

1. Install nodejs, make, and gcc-c++:
    dnf install nodejs make gcc-c++ -y

As per OS standards,  all the applications and databases should run by a normal user but not with root user.

1. Create an user called roboshop:
    useradd roboshop

2. Switch to user:
    su - roboshop

## Add the application content

1. Download catalogue application content:
    curl -s -L -o /tmp/user.zip <https://github.com/rshaik4devops/user/archive/main.zip>

2. Change working directory as roboshop user's home:
  cd /home/roboshop

3. Unzip the downloaded zip to current directory:
    unzip /tmp/user.zip

4. Rename the unarchived directory to user:
  mv user-main user

5. Change directory to catalogue:
    cd /home/roboshop/user

6. Install the nodejs packages:
    npm install

7. Switch to root user:
    sudo su -

8. Rename and move configuration file to '/etc/systemd/system/':
    mv systemd.service /etc/systemd/system/user.service

9. Update configuration file to add mongodb service IP:
    (update 'redis-host-ip' and 'mogodb-server-ip':port)
    vi /etc/systemd/system/user.service

10. Reload deamon after the configuration change:
    systemctl daemon-reload

11. Enable catalogue service:
    systemctl enable user

12. Start catalogue service:
    systemctl start user
