---
title: "Github Actions"
date: 2022-05-11T15:46:05-05:00
draft: false
weight: 115
hidden: true
---

## Description

I wanted to learn a bit more about CI/CD and landed on working through Github Actions so that I could incorporate it into this project. The reason I decided on Github actions was simply because of the seamless integration within github. I plan on working through more ci/cd tools in the future but this was a good start and learning experience for me.

What I wanted to accomplish:
1. Perform action on merge into master branch
1. Have the action complete the following tasks:
	- Checkout master branch
	- Install framework on runner
	- Build project
	- Secure copy files to server

Requirements:
- Server hostname or ip address
- Username to login to server
- ssh port (22)
- Secret Key
- Target directory on server

All of the above information is stored inside of the github project repos action secrets. This allows you to use them as environment variables within the yml file that performs the action.

```yml
name: Deploy Master on Merge

on: 
  push:
    branches:
      - master

jobs:
  dependencies_checkout_build_deliver:
    name: Install Hugo, Checkout Source Code, Build Artifacts & Deliver
    runs-on: ubuntu-latest
    steps:
      - name: Check out repository code
        uses: actions/checkout@master
        with:
          submodules: true
          fetch-depth: 0

      - name: Install Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: '0.93.0'

      - name: Build
        run: hugo --minify --gc

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

With a bit of research I was able to utilize some marketplace features created by `peaceiris` and `appleboy`.

One issue that was quite troublesome throughout this entire process was being prevented from secure copying to server due to an invalid or unrecognized [public key]. 
