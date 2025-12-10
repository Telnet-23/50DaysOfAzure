## The Problem
As part of the data migration process, the Nautilus DevOps team is actively creating several storage containers on Azure. They plan to utilize public Blob containers to store the relevant data. Given the ongoing migration of other infrastructure to Azure, it is logical to consolidate data storage within the Azure environment as well.

Create a new storage account named nautilusst21842 and a public Blob container named nautilus-blob-19525 within the storage account. Make sure anonymous read access for containers and blobs is enabled.

## The Solution
- Reference Docs: https://learn.microsoft.com/en-us/azure/storage/blobs/anonymous-read-access-configure?tabs=azure-cli

As always, search for the resource group name and make a note with 
```az group list```

Then create the storage account
```az storage account create --name nautilusst21842 --resource-group kml_rg_main-1e3a8b50aff84395 --allow-blob-public-access true```

Now, this command, I did a lot of backward and forward with to decide what parameter to use on the end, ```--public-access blob``` or what I've placed below. I decided on below as it closer refeltcs what is being asked in the question.
```az storage container create --name nautilus-blob-19525 --account-name nautilusst21842 --public-access blob```

## Note. 
This failed. Not entirely sure why yet so I'll work it out and update the doc :)
