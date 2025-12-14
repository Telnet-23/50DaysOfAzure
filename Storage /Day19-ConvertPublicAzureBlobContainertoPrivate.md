## The problem 
The Nautilus DevOps team has been using Azure Blob Storage to manage their data. Recently, they realized that one of their containers, currently public, needs to be restricted for internal use only. Your task is to convert a public Azure Blob container to private.

Two blob containers named devops-container-13548 and devops-priv-30925 are available in the East US region within the storage account devopsst27094. The devops-container-13548 is currently public, and devops-priv-30925 is private.

1. Convert the blob container devops-container-13548 from public to private while leaving devops-priv-30925 unchanged.

2. Make sure the access level for devops-container-13548 is set to private with no public access.

## The Solution

First up, lets list the containers to ensure all is there. I'm sure it is but you should work these labs out as if you've been given the bare minimum information and not the correct name of the containers and which one is public. verify yourself :smile: 
```az storage container list --account-name devopsst27094```

Now, what you'll see is ```public access``` on devops-container-13548 shows as 'container' where as on devops-priv-30925 , ```public access``` shows as null. So we need to change that. To do this, use this command.
```az storage container set-permission --name devops-container-13548 --account-name devopsst27094 --public-access off```

Now once done, list the containers again and verify that ```public access``` on both now shows 'null' menaing none. They're private, no blob or container is exposed publicly. 
```az storage container list --account-name devopsst27094```

## Thoughts and takeaways
Nice little lab that, Never actually had to do that with a CLI and nobody was forcing me now. I'm liking the challenge of doing these challenges in the CLI as much as I can. Makes it.... well; a bit challenging :smile: Time for tea. 
