## The Problem
As part of a data migration project, the team lead has tasked the team with migrating data from an existing Azure Blob container to a new Blob container. The existing container contains a substantial amount of data that must be accurately transferred to the new container. The team is responsible for creating the new Blob container and ensuring that all data from the existing container is copied or synced to the new container completely and accurately. It is imperative to perform thorough verification steps to confirm that all data has been successfully transferred to the new container without any loss or corruption.

As a member of the Nautilus DevOps Team, your task is to perform the following:

Create a New Private Azure Blob Container: Name the container nautilus-dest-9812 under the storage account nautilusst28637.

Data Migration: Migrate the file nautilus.txt from the existing nautilus-source-12601 container to the new nautilus-dest-9812 container.

Ensure Data Consistency: Ensure that both containers have the file nautilus.txt and confirm the file content is identical in both containers.

Use Azure CLI: Use the Azure CLI to perform the creation and data migration tasks.

## The Solution
So off, the bat we need to make the new container with the specified name using the specified account and make it private. To do that, I ran 
```
az storage container create --name nautilus-dest-9812 --account-name nautilusst28637 --public-access off
```

Next you need to copy the file over from one conteinr in the blob to the other. I had to google this as I wasn't sure of the exact command but like all things in Azure CLI, It's actually pretty self explanitory. 
```
az storage blob copy start --account-name nautilusst28637 --source-container nautilus-source-12601 --source-blob nautilus.txt --destination-container nautilus-dest-9812 --destination-blob nautilus.txt
```

After that runs, you should get the following output to verify that it was successful. 
```
{
  "client_request_id": "e05112ec-e637-11f0-976a-2ada0cad7618",
  "copy_id": "33de4771-3039-4943-b60b-35719cd6aeb2",
  "copy_status": "success",
  "date": "2025-12-31T11:00:10+00:00",
  "etag": "\"0x8DE485BC49BD69B\"",
  "last_modified": "2025-12-31T11:00:11+00:00",
  "request_id": "bbd08121-601e-007b-2e44-7a1189000000",
  "version": "2022-11-02",
  "version_id": null
}
```

Now, the final part of the challenege tells to you confirm the content in the file is the same. How do you do that? you cant ```cat``` a file in Azure. What you can do, is comapare the MD5 hash of the content contained in the file. If the Hash is the same, the content is the same. Yo do this, you just need to list the container and pipe that to the correct attribute. 
```
az storage blob list --container-name nautilus-source-12601 --account-name nautilusst28637 | grep "contentMd5"
az storage blob list --container-name nautilus-dest-9812 --account-name nautilusst28637 | grep "contentMd5"
```


## Thoughts and takeaways
I really liked this one. I pretty much like all challenges that force me to learn something new. This was one of them :smile: time for tea. 
