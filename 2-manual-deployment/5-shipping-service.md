# Shipping service (Java application)

Shipping service is responsible for finding the distance of the package to be shipped and calculate the price based on that.

## Launch an EC2 instance for shipping service with a Security Group

1. Launch an EC2 instance:
    create a security group with inbound rules to allow ssh access and catalogue application.
    launch VM with the security group.

2. Set hostname (Optional):
    hostnamectl set-hostname shipping

3. Update the packages:
    sudo dnf update -y

## Install Applications and Dependencies

1. Install maven:
    dnf install maven -y

As per the standard process, we always run the applications as a normal user. So, create an user and switch to user

1. Create user roboshop:
    useradd roboshop

2. Change the working directory to user's home:
    cd ~

3. Download the application code:
    curl -s -L -o /tmp/shipping.zip <https://github.com/rshaik4devops/shipping/archive/main.zip>

4. Unzip:
    unzip /tmp/shipping.zip

5. Rename:
    mv shipping-main shipping

6. Change working directory to shipping:
    cd shipping

7. Make artifact:
    mvn clean package

8. Move and rename the jar file:
    mv target/shipping-1.0.jar shipping.jar

## Configuration

1. Move the 'systemd.service' file to '/etc/systemd/system/shipping.service'
    mv systemd.service /etc/systemd/system/shipping.service

2. Update the configuration file with CART_ENDPOINT and DB_HOST details:

3. systemctl daemon-reload
4. systemctl enable shipping
5. systemctl start shipping
