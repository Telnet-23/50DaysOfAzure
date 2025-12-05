## The Problem

The Nautilus DevOps team is migrating a portion of their infrastructure to Azure. During the migration, they have created several virtual machines (VMs) in different regions. The team has identified one VM that is not tagged properly so they decided to tag it as needed.

Add the tag Environment=dev to the virtual machine named nautilus-vm.

## The Solution

First up, I ran ```az vm list``` which told me the resource group and the full id for the vm which would both be required for the task. I also ran ```az tag list``` to view the tags. 

Once I had the information required, I copied the information and pasted it into the --resource-id field because theres no way I'm typing that with zero errors. I then set the operation to merge and specified the tag.
```az tag update --resource-id /subscriptions/f0c3bcdd-5ce2-4fa0-8cf3-41559747512b/resourceGroups/kml_rg_main-244be54729dc4446/providers/Microsoft.Compute/virtualMachines/nautilus-vm --operation merge --tags Environment=dev```

The output from the above confirmed it worked but I verified anyway with.
```az vm show --name nautilus-vm --resource-group kml_rg_main-244be54729dc4446```

## Thoughts and takeaways
Tags are an area for me that I undertstand but I've never worked in an enrironment where tags are being used well. This was a great challenge because I've never handles tags via Azure CLI so a bit of google and playing and ofcourse, documentation: https://learn.microsoft.com/en-us/cli/azure/tag?view=azure-cli-latest#az-tag-update. Time for tea. 
