## The Problem 

The Nautilus DevOps team is presently immersed in data migrations, transferring data from on-premise storage systems to Azure Blob containers. They have recently received some data that they intend to copy to one of the Blob containers.

A Blob container named datacenter-blob-12082 already exists in the East US region under the storage account datacenterst21861. Copy the file /tmp/datacenter.txt to the Blob container datacenter-blob-12082.

## The Solution

In this issue some of the information is already provided to you but if it wasnt, you could have obtained it with
```az storage account list | grep name``` and ```aaz storage container list --account-name datacenterst21861 | grep name``` respectivly 

You can also run ```cat /tmp/datacenter.txt``` just to ensure the file is there. It says it is, but check everything. 

Once you've done all your checks you just need to upload it with the blow command. 
```az storage blob upload --account-name datacenterst21861 --container-name datacenter-blob-12082 -f /tmp/datacenter.txt```

You can then verify in the CLI with 
```az storage blob list --container-name devops-blob-29500 --account-name devopsst11565``` and it will be the value against "name:" so you could also pipe a grep on the end like this ```az storage blob list --container-name devops-blob-29500 --account-name devopsst11565 | grep "name"*``` and you will see your file listed if it's there. Alternativly, check it in the console, but thats no fun is it :smile:

## Thought and takeaways
That was good. I've been really busy the last couple of days so I'm playing catchup with a few days of challenges. Azure storage is such a key and fundamental skill. I look forward to the next few days of labs. Time for tea. 
