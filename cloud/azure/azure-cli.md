# Azure CLI

## Init

Генерим конфиг для kubectl (точные коvанды можно взять на портале Azure, так же нужен установленный AzureCLI)

```
az login
az account set --subscription 0c675***8217cf
az aks get-credentials --resource-group example-group --name example-name
```

## Azure Storage Blob

```
# Create a new resource group to hold the storage account -
# if using an existing resource group, skip this step
az group create --name my-resource-group --location westus2

# Create the storage account
az storage account create -n my-storage-account-name -g my-resource-group

```
