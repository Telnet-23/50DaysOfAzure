## The Problem

The Nautilus DevOps team is currently engaged in a cleanup process, focusing on removing unnecessary data and services from their Azure environment. As part of the migration process, several resources were created for one-time use only, necessitating a cleanup effort to optimize their Azure environment.

A private blob container named datacenter-blob-17996 already exists in the East US region under storage account datacenterst27578.

1. Copy the contents of datacenter-blob-17996 blob container to the /opt directory on the azure-client host (the landing host once you load this lab).

2. Delete the blob container datacenter-blob-17996 from the storage account.

## The Solution

Verify the required information first, despite the task giving you some info, you should also check it as if you were told nothing. Fist get the storage account.
```az storage account list | grep name```

Then get a list of the storage containers under that storage account. 
```az storage container list --account-name datacenterst27578```

Then get the name of the blob in the container. 
```az storage blob list --container-name datacenter-blob-17996 --account-name datacenterst27578 | grep "name"*```

Once you know all of that, you can move your blob to the specified local path.
```az storage blob download -f /opt/datacenter.txt --container-name datacenter-blob-17996 --name datacenter.txt --account-name datacenterst27578```

Confirm the data have moved to the local path. 
```cat /opt/datacenter.txt```

Now we can delete the contianer using the following command ```az storage container delete --name datacenter-blob-17996 --account-name datacenterst27578```, if it works, you will see "deleted": true


And finally, verify that the container is no longer there ```az storage container list --account-name datacenterst27578```

## Thoughts and takeaways
That was pretty cool, I failed the first time because I misunderstood and I only deleted the datacenter.txt blob in the container and not the container itself. I simply misunderstoof the assignment I suppose. Oh well, time for tea. 



