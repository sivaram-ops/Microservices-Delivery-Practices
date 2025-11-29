# Redis service (Redis application)

## Launch an EC2 instance for Redis application and setup Security Group

1. Launch an EC2 instance:
    create a security group with inbound rules to allow ssh access and catalogue application.
    launch VM with the security group.

2. Set hostname (Optional):
    hostnamectl set-hostname redis

3. Update the packages:
    sudo dnf update -y

## About Redis

Redis is 'in-memory data storage' and can be accessed using API.

## To Install Redis on AWS

1. Find avaialbel redis package on aws:
    dnf list | grep "redis"

2. Install the found version:
    dnf install redis6 -y

3. Enable redis6:
    systemctl enable redis6

4. Start the redis:
    systemctl start redis6

## Service configuration

1. Set protected-mode to 'no' in configuration file:
    sudo vi /etc/systemd/system/redis6.service'
    Set the protected-mode no

2. Update the bind ip from 'loopback ip' to 'redis private ip'.
    (multiuser.target.wants --> update 127.0.0.1 to 0.0.0.0)
    Set bind ip from 127.0.0.1 to 0.0.0.0

3. Restart redis after the configuration file change:
    systemctl restart redis6
