# Payment service (Python Application)

This service is responsible for payments in RoboShop e-commerce app. While creating Ec2 instance please select Devops-Practice AMI From Communicty AMIS.


## Launch an EC2 instance for payment service with a Security Group

1. Launch an EC2 instance:
    create a security group with inbound rules to allow ssh access and catalogue application.
    launch VM with the security group.

2. Set hostname (Optional):
    hostnamectl set-hostname payment

3. Update the packages:
    sudo dnf update -y


## Install Applications and Dependencies

1. Install python36, gcc, python3-devel: 
    dnf install python3 gcc python3-devel -y

2. Create an user (roboshop) to run the payment application:  
    useradd roboshop
    (no need to switch user for now. we will add this user to payment.ini file)

3. Change working directory to user home:
    cd /home/roboshop

4. Download payment application content:
    curl -L -s -o payment.zip "https://github.com/rshaik4devops/payment/archive/main.zip"

5. Unzip: 
    unzip /tmp/payment.zip

6. Rename the unarchived directory: 
    mv payment-main payment

7. Change working directory to renamed folder:
    cd /home/roboshop/payment 

8. Install dependencies as specified in the requirements file,using pip3.6
    pip install -r requirements.txt (# run as root)

#running pip as root is not ideal. switch to user.

9. Update the user and group id in payment.ini file. (id details can be found using id user command):
    vi payment.ini


## configuration:

1. Move the 'systemd.service' file to '/etc/systemd/system/payment.service'
    mv systemd.service /etc/systemd/system/payment.service

2. Update the '/etc/systemd/system/payment.service' configuration file:

3. systemctl daemon-reload

4. systemctl enable payment

5. systemctl start payment
