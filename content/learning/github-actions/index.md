---
title: "Github Actions"
date: 2022-05-11T15:46:05-05:00
draft: false
weight: 115
hidden: false
---

## Description

I wanted to learn a bit more about CI/CD and landed on working through Github Actions so that I could incorporate it into this project. 

The reason I decided on Github actions was simply because of the seamless integration within github. I plan on working through more ci/cd tools in the future but this was a good start and learning experience for me.

What I wanted to accomplish:
1. Perform action on merge into master branch
1. Have the action complete the following tasks:
	- Checkout master branch
	- Install framework on runner
	- Build project
	- Secure copy files to server

Requirements:
- Server hostname or ip address of production server
- Username to login to server
- ssh port (22)
- Secret Key
- Target directory on server

All of the above information is stored inside of the project repository secrets. This allows you to use them as environment variables within the yml file that performs the action.

## Github Action .yml file for project:

```yml
## Name of action
name: Deploy Master on Merge

## When to perform the action
on: 
  push:
    branches:
      - master

## job content
jobs:
  dependencies_checkout_build_deliver:
    name: Install Hugo, Checkout Source Code, Build Artifacts & Deliver
## type of OS for runner
    runs-on: ubuntu-latest
    steps:
## checkout from master
      - name: Check out repository code
        uses: actions/checkout@master
        with:
          submodules: true
          fetch-depth: 0
## Install hugo on runner
      - name: Install Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: '0.93.0'
## build project on runner
      - name: Build
        run: hugo --minify --gc
## deliver build artifacts to prod server
      - name: Deliver
        uses: appleboy/scp-action@master
        with:
          host: ${{ secrets.HOST }}
          username: ${{ secrets.USERNAME }}
          port: ${{ secrets.PORT }}
          key: ${{ secrets.KEY }}
          source: "public/*"
          target: ${{ secrets.PATH }}
```

With a bit of research I was able to utilize some actions created by `peaceiris` and `appleboy`.

One complication throughout the process was the following error:

{{% notice warning "error" %}}
error copy file to dest: ***, error message: ssh: handshake failed: ssh: unable to authenticate, attempted methods [none publickey], no supported methods remain
{{% /notice %}}

## Troubleshooting

1. Double check private key was copied correctly to secret field
1. Changing private key from OPENSSH to RSA
1. Specify that the key is created as a .pem file with a length of 4098 (similar to that of action repo)

Fortunately I was able to troubleshoot with a co-worker that had a similar tech-stack project. I noticed that the production server they were using was Ubuntu 20.04 while I was using the newest Ubuntu 22.04 Jammy LTS. 

After changing the version of my server from 22.04 to 20.04 the issue was resolved and the action fired off without problems.

Overall this was an excellent learning experience and a good foot forward towards further automation.
