# frontend service: (nginx application)

## Launch an EC2 instance with a Security Group

1. launch an EC2 instance:
    create a security group with inbound rules to allow ssh access and public traffic.
    launch VM with the security group.
2. set hostname (Optional):
    hostnamectl set-hostname frontend
3. update the packages:
    sudo dnf update -y

## Install the application (nginx) and start it

1. install nginx:
    dnf install nginx -y
2. enable nginx:
    systemctl enable nginx
3. start nginx:
    systemctl start nginx
4. verify the application in browser:
    http://<ec2-ip>:80

## clean nginx server's public folder

1. change the working directory to nginx server's public folder:
    cd /usr/share/nginx/html
2. remove any previous files of root directory:
    rm -rf *

## Download the application content and move content to the nginx's public directory

1. download the frontend application content from repository:
   curl -s -L -o /tmp/frontend.zip "<https://github.com/rshaik4devops/frontend/archive/main.zip>"

2. unzip downloaded zip file in root directory:
   unzip /tmp/frontend.zip

3. cd /tmp

4. move all files of the unzipped folder to server's root directory:
   mv frontend-main /usr/share/nginx/html

5. cd /usr/share/nginx/html

6. Move any files within the directories of the unzipped folder to server's root directory:
   mv static /usr/share/nginx/html

## update/move the nginx configuration file and restart nginx to load new configuration

1. update configuration file:
   vi /usr/share/nginx/html/localhost.conf

2. move configuration file to:
   mv localhost.conf /etc/nginx/default.d/roboshop.conf

3. restart nginx:
   systemctl restart nginx

4. clean up: remove empty folders (unzipped folder & static folder & any unnecessary files):
   rm -rf /tmp/frontend.zip
   cd /usr/share/nginx/html
   rm README.md
