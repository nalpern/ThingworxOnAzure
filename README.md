# ThingworxOnAzure
ARM template

## How to run
* Download azuredeploy.parameters.json
* Make your edits
* Click the Deploy to Azure button
* Click "Edit Parameters" and upload your azuredeploy.parameters.json


## Actions
<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2Fkwhitehall%2FThingworxOnAzure%2Fmaster%2Fazuredeploy.json" target="_blank"><img src="http://armviz.io/visualizebutton.png"/></a>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fkwhitehall%2FThingworxOnAzure%2Fmaster%2Fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/> 
</a>

## Overview of Templates
The below diagram shows the layout of the templates.  The templates have been nested such that each nested template can be tested independently and then linked in the master template.  The master template will pass the parameters to each linked template and reference an dependencies between the linked templates.

![alt tag](https://raw.githubusercontent.com/kwhitehall/ThingworxOnAzure/master/ARM-Architecture.png)

### Specific template notes
*  The VM template has the most complex set of parameters
   *  The availabilitySet parameter can be set to an empty string will specifics no availibility set for the VM.
   *  The publicIPAddress parameter can be set to true or false which determines if the NIC card is assigned a public IP address.  Conditions are used in the ARM template to achive this.
   *  The VM template uses just a single parameter file which is shared between the NIC, Public IPs and the VMs.  This simplified some testing.
*  The VNET template does a loop to create each subnet.  The subnets cannot be placed in a seperate linked template since when you run the ARM template a second time it will fail.  The VNET will attempt to remove all the subnets when the subnets are in a seperate template.


## To Run via command line
```
# Login
az login

# Select Subscription
az account set -s REPLACE_ME

# Script parameters
resourceGroup="ThingworxOnAzure"
location="eastus"
today=`date +%Y-%m-%d-%H-%M-%S`
deploymentName="MyDeployment-$today"

# Create resource group
az group create \
  --name        $resourceGroup \
  --location    $location

# Deploy the ARM template
az group deployment create \
  --name                 $deploymentName \
  --resource-group       $resourceGroup \
  --template-file        azuredeploy.json \
  --parameters           @azuredeploy.parameters.json \
  --mode                 Incremental

# Clean up resource group
az group delete --name $resourceGroup
```
