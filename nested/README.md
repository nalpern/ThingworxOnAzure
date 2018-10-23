# This is for running a nested template locally
You need to sign in once and set your subscription once.

# Login, set subscription and resource parameters
```
az login
az account set -s REPLACE_ME
resourceGroup="ThingworxOnAzure"
location="eastus"
az group create --name $resourceGroup --location $location
```

## Test NSG Template
You can run each of the below blocks from your local development machine
```
today=`date +%Y-%m-%d-%H-%M-%S`
deploymentName="MyDeployment-$today"
az group deployment create \
  --name                 $deploymentName \
  --resource-group       $resourceGroup \
  --template-file        azuredeploy.nsg.json \
  --parameters           @local.parameters.nsg.json

today=`date +%Y-%m-%d-%H-%M-%S`
deploymentName="MyDeployment-$today"
az group deployment create \
  --name                 $deploymentName \
  --resource-group       $resourceGroup \
  --template-file        azuredeploy.vnet.json \
  --parameters           @local.parameters.vnet.json

today=`date +%Y-%m-%d-%H-%M-%S`
deploymentName="MyDeployment-$today"
az group deployment create \
  --name                 $deploymentName \
  --resource-group       $resourceGroup \
  --template-file        azuredeploy.subnet.json \
  --parameters           @local.parameters.subnet.json    

today=`date +%Y-%m-%d-%H-%M-%S`
deploymentName="MyDeployment-$today"
az group deployment create \
  --name                 $deploymentName \
  --resource-group       $resourceGroup \
  --template-file        azuredeploy.storage.json \
  --parameters           @local.parameters.storage.json    
```