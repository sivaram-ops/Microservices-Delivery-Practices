Welcome to this repository.

This repo is a Full-Stack DevOps Implementation - of an ecommerce website, Roboshop, built with microservices in 3-tier architecure.
This repo presents a complete DevOps lifecycle. from manual deployment on VMs to containerizing and orchestrating with kubernetes.

# About the directories in repo & their contents:
1-microservices-code: The complete source code for the 10 microservices (Node, Python, Java, etc.). 10 subfolders.
2-manual-deployment: Containes Markdown files documenting the configuration steps.
3-ansible-playbooks: The playbooks for deploying each service.
4-dockerfiles: The optimized Dockerfiles and Compose file.
5-k8s-orchestration: K8s YAML files for the application.
6-CI-CD-with-jenkins: Jenkins Files for pipelines etc.
7-Observability: Monotoring and solutions to the chanllenges.
'assets' direcoty: to store images (for markdown files)


This project (Roboshop) is composed of 10 microservices in 3-tire architecture. Each microservice (application) is serving a distinct function and interacting with various data base services (MongoDB, MySQL, Redis, RabbitMQ).

## ⚙️ architecture: 3-tier (frontend, backend, and databases)
![3-tier architecture of roboshop](https://github.com/sivaram-ops/roboshop-3tier-microservices/blob/7199f09afe656dc669505aad935214d5a247a8cb/3-tier-microservices.png)

