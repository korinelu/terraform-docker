🛠 Task 3: Infrastructure as Code (IaC) with Terraform
🎯 Objective
Provision a local Docker container using Terraform.

✅ Steps Performed
Created Terraform Project


mkdir terraform-docker


cd terraform-docker


Created main.tf Configuration

Used Docker provider to pull nginx:latest image.

Created a container named nginx_terraform with port mapping 8080:80.


terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 3.0.2"
    }
  }
}

provider "docker" {
  host = "npipe:////./pipe/docker_engine"  # For Windows + Docker Desktop
}

resource "docker_image" "nginx" {
  name         = "nginx:latest"
  keep_locally = false
}

resource "docker_container" "nginx_container" {
  name  = "nginx_terraform"
  image = docker_image.nginx.name
  ports {
    internal = 80
    external = 8080
  }
}
Initialized Terraform


terraform init
Planned Infrastructure Changes


terraform plan
Applied Configuration


terraform apply
Confirmed by visiting: http://localhost:8080 in browser.

Saw the default nginx welcome page ✅

(Optional) Checked Terraform State


terraform state list
(Optional) Destroyed the Infrastructure


terraform destroy
📦 Outcome
Successfully provisioned a Docker container using Terraform.

Demonstrated key Terraform commands: init, plan, apply, destroy.

Understood basic IaC concepts with local Docker environment.

