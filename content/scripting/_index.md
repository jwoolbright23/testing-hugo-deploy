---
title: "Scripting"
date: 2022-05-11T15:46:05-05:00
draft: false
weight: 100
---

## Bash Scripts

Below I begin to list some scripts that I have written recently for our the Linux Curriculum.

### React Initialization Script:

{{% expand "Click to View Script" %}}
```bash
# install dependencies for React project

wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash

## Install Caddy https://caddyserver.com/docs/install#debian-ubuntu-raspbian

sudo apt install -y curl

sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https

curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo tee /etc/apt/trusted.gpg.d/caddy-stable.asc
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
sudo apt update -y
sudo apt install caddy

## Install nvm

export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"

## install node and npm version 16.3.0 (version project requires)

nvm install 16.3.0
nvm use 16.3.0

## Cloning Existing Project Repository to Machine

git clone https://github.com/LaunchCodeTechnicalTraining/react-tic-tac-toe-tutorial.git /path/to/project/react-tic-tac-toe-tutorial

### Load project dependencies inside of directory

cd /path/to/project/react-tic-tac-toe-tutorial

npm i

## Build dependences / Artifcats

npm run build

## Move artifacts: Create a /website at root of server

sudo mkdir /website

mv /path/to/project/react-tic-tac-toe-tutorial/build /website

## Create a Caddyfile inside of /etc/caddy/Caddyfile and reload

(
cat <<'EOF'
https://localhost {
        root * /website/build
        file_server
}
EOF
) > /etc/caddy/Caddyfile

caddy reload --config /etc/caddy/Caddyfile
```
{{% /expand %}}

### Angular Initialization Script:

{{% expand "Click to View Script" %}}
```bash
## Install dependencies

wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash

#Install curl

sudo apt update
sudo apt install -y curl

#Install caddy

sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo tee /etc/apt/trusted.gpg.d/caddy-stable.asc
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
sudo apt update
sudo apt install caddy

source /home/john/.bashrc

##Install nvm package manager

export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"

## Use Correct Version for Project

nvm install 16.13.0 #installing even number node versions
nvm use 16.13.0 #using even number node versions

## Install Angular CLI

npm install -g @angular/cli

## Clone Existing Project Repository

git clone https://github.com/LaunchCodeTechnicalTraining/angular-tour-of-heroes /home/john/Desktop/angular-tour-of-heroes 

## Moveinto directory and load dependencies

cd /path/to/project/angular-tour-of-heroes

## Load Project dependencies

npm i

## Build dependencies and artifacts

ng build

## Change User Permissions for Website Directory

sudo chmod 777 /website

## Move Build Artifacts

mv /path/to/project/angular-tour-of-heroes/dist/angular-tour-of-heroes /website

## Configure Caddy File and Reload
(
cat <<'EOF'
https://localhost {
	root * /website/angular-tour-of-heroes
	file_server
}
EOF
) > /etc/caddy/Caddyfile

caddy reload --config /etc/caddy/Caddyfile
```
{{% /expand %}}

### Spring Boot Initialization Script:

{{% expand "Click to View Script" %}}
```bash
# Install Dependencies

## openjdk-11-jre (version project uses)

sudo apt install -y openjdk-11-jre

## Install Caddy for Web Server

sudo apt install -y curl

sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https

curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo tee /etc/apt/trusted.gpg.d/caddy-stable.asc
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
sudo apt update -y
sudo apt install caddy

## Clone Existing Project Repository to Machine

git clone https://github.com/LaunchCodeTechnicalTraining/spring-todo-api /path/to/project/spring-todo-api

## Build the project with gradle

/path/to/project/spring-todo-api/gradlew bootJar -p /path/to/project/spring-todo-api/

## Create /website folder in root directory

sudo mkdir -p /website/spring
sudo chown user:user /website
sudo chown user:user /website/spring

## Move .jar file and rename

sudo mv /path/to/project/spring-todo-api/build/libs/todo-0.0.1-SNAPSHOT.jar /website/spring/todo-api.jar

## Running the project jar file with jre in detached mode

java -jar /website/spring/todo-api.jar &

## Configure Caddyfile with Reverse Proxy

(
cat <<'EOF'
http://localhost {
        reverse_proxy 127.0.0.1:8080
}
EOF
) > /etc/caddy/Caddyfile

caddy reload --config /etc/caddy/Caddyfile
```
{{% /expand %}}
