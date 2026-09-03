Day 02 — Services & Tags

🔹 Ansible — Install & Enable Nginx
- name: Install and start Nginx on Pathnex
  hosts: all
  become: yes

  tasks:
    - name: Install nginx
      yum:
        name: nginx
        state: present

    - name: Enable nginx
      service:
        name: nginx
        state: started
        enabled: yes


🔹 Terraform — EC2 with Tags (r5.2xlarge)
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "PathnexEC2" {
  ami           = "ami-0abcd1234abcd1234"
  instance_type = "r5.2xlarge"

  tags = {
    Name        = "Pathnex-Server"
    Environment = "Training"
    Owner       = "PathnexStudent"
  }
}


# Kubernetes — Deployment with 2 Replicas
apiVersion: apps/v1
kind: Deployment
metadata:
  name: pathnex-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: pathnex-app
  template:
    metadata:
      labels:
        app: pathnex-app
    spec:
      containers:
        - name: app
          image: nginx
          ports:
            - containerPort: 80


🔹 Shell Script — Disk Usage
#!/bin/bash
df -h

🔹 Docker
# Docker Images & Containers
docker pull ubuntu
docker images
docker ps -a

# Docker File
FROM ubuntu:22.04
RUN apt update
CMD ["echo", "Hello Pathnex"]