# Docker in Azure

## Installation of Azure CLI 
1. Windows: https://aka.ms/installazurecliwindows
2. Linux: https://docs.microsoft.com/pl-pl/cli/azure/install-azure-cli-apt?view=azure-cli-latest
3. macOS: https://docs.microsoft.com/pl-pl/cli/azure/install-azure-cli-macos?view=azure-cli-latest

## Setting up Virtual Machine
1. Log in through Azure CLI:
```
az login
```
2. Create Resource Group where our resources will be deployed and managed.
```
az group create --name myrg --location eastus
```
3. Create Virtual Machine. We are installing Ubuntu LTS on Standard_DS2_v2 type of VM.
```
az vm create --resource-group myrg --name myvm --image UbuntuLTS --admin-username student --admin-password 'P@ssw0rd1234' --size Standard_DS2_v2
```
* For checking different available images you can use:
```
az vm image list --output table
```
* For checking available different configuration of VM you can use:
```
az vm list-sizes --location eastus --output table
```

## Docker installation on Virtual Machine
1. Install Putty: https://the.earth.li/~sgtatham/putty/latest/w32/putty-0.70-installer.msi
2. Check public IP address your Virtual Machine:
```
az vm list-ip-addresses -g myrg -n myvm --output table
```
2. Login via SSH using Putty.
3. Install Docker according to the documentation for Ubuntu: https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-using-the-repository
