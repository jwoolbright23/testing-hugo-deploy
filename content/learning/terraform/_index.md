---
title: "Terraform"
date: 2022-05-11T15:46:05-05:00
draft: false
weight: 105
---
## Description

In preparation to teach the upcoming Linux course for a group of learners we discovered that anyone using a machine with M1 ARM chip would not be capable of using VirtualBox.

One of the workarounds we landed on was to build a golden image for a Ubuntu 22.04 OS. Since there is thechance that this will be needed often for multiple students in the future I wanted to begin automating the process of creating multiple ec2 instances and dive into some IaC. 


{{% children %}}
