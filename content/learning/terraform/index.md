---
title: "Terraform"
date: 2022-05-11T15:46:05-05:00
draft: false
weight: 105
---

## Description

In preparation to teach the upcoming Linux course for a group of learners we discovered that anyone using a machine with M1 ARM chip would not be capable of using VirtualBox. VirtualBox only supports 64bit and 86 bit architechture.

One of the workarounds we landed on was to build a golden image for a Ubuntu 22.04 OS. Since there is thechance that this will be needed often for multiple students in the future I wanted to begin automating the process of creating multiple ec2 instances and dive into some IaC. 

## Terraform Installation for Ubuntu 22.04 (My Personal Machine)

Resources Used: [Terraform Docs](https://www.terraform.io/)

```bash
sudo apt update && sudo apt install -y gnupg software-properties-common curl
```

```bash
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
```

```bash
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
```

```bash
sudo apt update && sudo apt install terraform
```

## Verify Installation

```bash
terraform -help
```

## Start and Destroy Nginx server per tutorial

```bash
mkdir terraform-container
```

```bash
cd terraform-container
```

### Create new file called `main.tf` and add the following code:

```terraform
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 2.13.0"
    }
  }
}

provider "docker" {}

resource "docker_image" "nginx" {
  name         = "nginx:latest"
  keep_locally = false
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "tutorial"
  ports {
    internal = 80
    external = 8000
  }
}
```

initialize project with `terraform init`

```bash
terraform init
```

```bash
terraform apply
```

### Validation

Check localhost:8000 in your browser to verify the nginx server is up and running


## Remove Container and Shutdown Nginx Server
```bash
terraform destroy
```




