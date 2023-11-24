# CVAT Installation Manual for Linux

## Introduction
This guide provides step-by-step instructions for installing CVAT (Computer Vision Annotation Tool) on a Linux system. CVAT is a powerful open-source annotation tool for computer vision tasks.

## Prerequisites
Before starting the installation process, ensure that you have the following prerequisites:
- Access to a Linux terminal
- Docker and Docker Compose installed
- Git installed (if not, install using `sudo apt install git`)

## Step - 1 
## Installing Docker and Docker Compose
Follow the commands below to install Docker and Docker Compose on your Linux system. Refer to [Docker documentation](https://docs.docker.com/install/linux/docker-ce/ubuntu/) for additional instructions.

```bash
sudo apt-get update
sudo apt-get --no-install-recommends install -y \
  apt-transport-https \
  ca-certificates \
  curl \
  gnupg-agent \
  software-properties-common
```
## Step - 2
## Add Docker repository and key
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
  "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) \
  stable"
```

## Step - 3
## Install Docker and Docker Compose
```
sudo apt-get update
sudo apt-get --no-install-recommends install -y \
  docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

## Step - 4
## Perform post-installation steps
```
sudo groupadd docker
sudo usermod -aG docker $USER
```
Log out and log back in (or reboot) for changes to take effect

# Step - 5
## Clone CVAT Source Code
Clone the CVAT source code from the GitHub repository using Git:

```bash
git clone https://github.com/opencv/cvat
cd cvat
```

## Step - 6
## Configure CVAT Environment
Set the CVAT_HOST environment variable to enable access over a network:

```bash
export CVAT_HOST=your-ip-address
```

## Step - 7
## Run Docker Containers
Start the CVAT Docker containers. This may take some time to download the required images and create containers:

```bash
docker-compose up -d
```
(Optional) Specify a CVAT version using the CVAT_VERSION environment variable:

```bash
CVAT_VERSION=dev docker-compose up -d
```

For more options, refer to How to pull/build/update CVAT images.

## Step - 8
## Verify Installation
Ensure that the local version of CVAT is working correctly by checking the server logs:

```bash
docker logs cvat_server
```

## Step - 9
## Create Superuser Account
When running the CVAT server for the first time, create a superuser account using the following command:

```bash
docker exec -it cvat_server bash -ic 'python3 ~/manage.py create superuser'
```
Follow the prompts to choose a username and password for the superuser account.

## Step - 10
## Install Google Chrome
CVAT supports only Google Chrome. Install it using the following commands:

```bash
curl https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'
sudo apt-get update
sudo apt-get --no-install-recommends install -y google-chrome-stable
```

## Step - 11
## Access CVAT
Open Google Chrome and navigate to `localhost:8080`. Log in with the superuser credentials created earlier. You can now use CVAT to create annotation tasks. Refer to the [CVAT manual]("https://opencv.github.io/cvat/docs/manual/") for detailed usage instructions.
