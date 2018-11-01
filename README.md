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
