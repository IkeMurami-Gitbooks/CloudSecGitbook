# Azure Storage BLOB

Хранение больших двоичных файлов

## Python

### Install

```
pip install azure-storage-blob
```

### Example

Используйте следующие классы Python для взаимодействия с ресурсами.

* [BlobServiceClient](https://docs.microsoft.com/ru-ru/python/api/azure-storage-blob/azure.storage.blob.blobserviceclient). Класс `BlobServiceClient` позволяет управлять ресурсами службы хранилища Azure и контейнерами больших двоичных объектов.
* [ContainerClient](https://docs.microsoft.com/ru-ru/python/api/azure-storage-blob/azure.storage.blob.containerclient). Класс `ContainerClient` позволяет управлять контейнерами службы хранилища Azure и содержащимися в них большими двоичными объектами.
* [BlobClient](https://docs.microsoft.com/ru-ru/python/api/azure-storage-blob/azure.storage.blob.blobclient). Класс `BlobClient` позволяет управлять большими двоичными объектами службы хранилища Azure.

```python
import os, uuid
from azure.storage.blob import BlobServiceClient, BlobClient, ContainerClient, __version__


def list_blobs(blob_service_client, container: str):
    container_client = blob_service_client.get_container_client(container)

    print(f"\nListing blobs for container '{container}'...")

    # List the blobs in the container
    blob_list = container_client.list_blobs()
    for blob in blob_list:
        print("\t" + blob.name)

def blob_url():
    blob_client = BlobClient.from_connection_string(
        AZURE_STORAGE_CONNECTION_STRING, container_name="dev", blob_name="test.txt")
    print(blob_client.url)

try:
    print("Azure Blob Storage v" + __version__ + " - Python quickstart sample")

    ACCOUNT_KEY = "ySUF4d***29PA=="
    AZURE_STORAGE_CONNECTION_STRING = "DefaultEndpointsProtocol=https;AccountName=someaccountname;AccountKey=ySUF4d***29PA==;EndpointSuffix=core.windows.net"
    # Quick start code goes here

    # Create the BlobServiceClient object which will be used to create a container client
    blob_service_client = BlobServiceClient.from_connection_string(AZURE_STORAGE_CONNECTION_STRING)

    account_info = blob_service_client.get_account_information()
    print('Using Storage SKU: {}'.format(account_info['sku_name']))
    print('Using Account kind: {}'.format(account_info['account_kind']))
    # print(account_info)

    for container_name in ["dev", "beta", "production"]:
        # enum blobs
        list_blobs(blob_service_client, container_name)

except Exception as ex:
    print('Exception:')
    print(ex)
```

Залить файл:

```python
blob_client = blob_service_client.get_blob_client(container="dev", blob="test.txt")

with open("test2.txt", "rb") as file:
    blob_client.upload_blob(file)
```
