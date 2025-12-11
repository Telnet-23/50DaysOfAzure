## The Problem 

The Nautilus DevOps team is presently immersed in data migrations, transferring data from on-premise storage systems to Azure Blob containers. They have recently received some data that they intend to copy to one of the Blob containers.

A Blob container named datacenter-blob-12082 already exists in the East US region under the storage account datacenterst21861. Copy the file /tmp/datacenter.txt to the Blob container datacenter-blob-12082.

## The Solution

```az storage container list --account-name datacenterst21861```

```az copy "/tmp/datacenter.txt" "https://account.blob.core.windows.net/datacenter-blob-12082" --recursive=true```
