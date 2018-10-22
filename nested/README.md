# This is for running a nested template locally
You must az login, set your subscription and script parameters from the README.md

## Script parameters
```
resourceGroup="ThingworxOnAzure"
location="eastus"
today=`date +%Y-%m-%d-%H-%M-%S`
deploymentName="MyDeployment-$today"
```

## Test NSG Template
```
az group deployment create \
  --name                 $deploymentName \
  --resource-group       $resourceGroup \
  --template-file        azuredeploy.nsg.json \
  --parameters           @local.parameters.nsg.json

az group deployment create \
  --name                 $deploymentName \
  --resource-group       $resourceGroup \
  --template-file        azuredeploy.vnet.json \
  --parameters           @local.parameters.vnet.json

az group deployment create \
  --name                 $deploymentName \
  --resource-group       $resourceGroup \
  --template-file        azuredeploy.subnet.json \
  --parameters           @local.parameters.subnet.json    
```