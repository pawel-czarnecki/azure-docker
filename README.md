# Docker in Azure

## Installation of Azure CLI 
1. Windows: https://aka.ms/installazurecliwindows
2. Linux: https://docs.microsoft.com/pl-pl/cli/azure/install-azure-cli-apt?view=azure-cli-latest
3. macOS: https://docs.microsoft.com/pl-pl/cli/azure/install-azure-cli-macos?view=azure-cli-latest

## Setting up Virtual Machine
1. Log in through Azure CLI.
```
az login
```
2. Create Resource Group where our resources will be deployed and managed.
```
az group create --name myrg --location eastus
```
3. Create Virtual Machine. We are installing Ubuntu LTS on Standard_DS2_v2 type of VM.
```
az vm create --resource-group myrg --name myvm --image UbuntuLTS --admin-username user --admin-password 'H4$$sło' --size Standard_DS2_v2
```
* For checking different available images do.
```
az vm image list --output table
```
* For checking different configuration of Virtual Machine do.
```
az vm list-sizes --location eastus --output table
```

## Docker installation on Virtual Machine
1. Install Putty: https://the.earth.li/~sgtatham/putty/latest/w32/putty-0.70-installer.msi
2. Check public IP address your Virtual Machine.
```
az vm list-ip-addresses -g myrg -n myvm --output table
```
2. Login via SSH using Putty.
3. Install Docker according to the documentation for Ubuntu: https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-using-the-repository

## Run linux in container
1. Get from the docker repository lightweight linux distribution.
```
docker pull alpine
```
2. Check all images pulled from repository.
```
docker image ls
```
3. Run and go into linux container.
```
docker run -it alpine /bin/sh
```
4. View all directories.
```
ls -l
```

## Create python application in container
1. Pull application from repository.
```
git clone https://github.com/pawel-czarnecki/azure-docker.git
```
2. Create Dockerfile for creating application image
```
# Install the latest python version from the repository
FROM python

# Create appication directory
WORKDIR /app

# Move all application files to docker directory
COPY app /app

# Install all dependencies
RUN pip install -r requirements.txt

# Listen network port
EXPOSE 8080

# Execute the command when running image
CMD [ "python", "api.py" ]
```
3. Make image based on Dockerfile. Name of its is python-api.
```
sudo docker build -t python-api .
```
4. Check if the image has been created.
```
docker image ls
```
5. Run application container in detached mode.
```
docker run --rm -d -p 8080:8080 python-api
```
6. Check running containers.
```
docker container ls
or
docker ps
```
7. Run application in webbrowser.
```
<your-public-ip-address>:8080
```
8. Go into application container.
```
docker exec -it <id-or-container-name> bash
```
9. Stop container.
```
docker stop <id-or-container-name>
```

## Other usefull commands
1. Removing container.
```
docker rm <id-or-container-name>
```
2. Removing image.
```
docker rmi <id-or-image-name>
```
