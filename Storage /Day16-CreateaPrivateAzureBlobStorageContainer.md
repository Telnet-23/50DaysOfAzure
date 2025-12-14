## The Problem 
As part of the data migration process, the Nautilus DevOps team is actively creating several storage containers on Azure. They plan to utilize private Blob containers to store the relevant data. Given the ongoing migration of other infrastructure to Azure, it is logical to consolidate data storage within the Azure environment as well.

Create a new storage account named xfusionst24523 and a private Blob container named xfusion-blob-30992 within the storage account.


## The Solution

First of all I confirmed there was a resource group just incase I had to create one 
```az group list```

Then I made the storage account as requested
```az storage account create --name xfusionst24523 --resource-group kml_rg_main-c33e09db91814446```

Then I created the private blob container in the storage account as the problem requested
```az storage container create --name xfusion-blob-30992 --account-name xfusionst24523 --public-access off```

## Thought and takeaways

Nice simple one that.I did misread the question and assumed the storage account was already made so trying to make the container failed. I then ran ```az storage account list``` which told me (along with the error trying to make the container) that the account didnt exist. Always check and dont rush in :smile: Time for tea. 
