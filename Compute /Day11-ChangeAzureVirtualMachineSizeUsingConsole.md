## The Problem
The Nautilus DevOps team is migrating a portion of their infrastructure to Azure. During the migration, they have created several virtual machines (VMs) in different regions. The team has identified one VM that is underutilized and has decided to change its size to optimize resource usage.

1. Change the VM size from Standard_B1s to Standard_B2s for the virtual machine named datacenter-vm.

2. Ensure the VM is in the running state after the size change is complete.

## The solution
Now! I know the task says to do this in the console, but thats neither fun nor challenging is it :smile: Lets use the CLI!

First, lets confirm the resource group the machine is in with ```az vm list```, you will see the name, size and resource group in the output which is everything we need to confirm the vm is the correct one, and then amend the size.

So! Before we can resize, stop and deallocate the vm 
```az vm stop --resource-group kml_rg_main-ad3a2cd9149d4252 --name datacenter-vm```
```az vm deallocate --resource-group kml_rg_main-ad3a2cd9149d4252 --name datacenter-vm```

Once thats done, we can resize it with ```az vm resize --name datacenter-vm --resource-group kml_rg_main-ad3a2cd9149d4252 --size Standard_B2s```

That will spit out output that will confirm the size has changed
<img width="874" height="294" alt="image" src="https://github.com/user-attachments/assets/05fa6756-ad49-4184-b460-579b87f4add8" />

Now we need to power on the VM again with ```az vm start --resource-group kml_rg_main-ad3a2cd9149d4252 --name datacenter-vm```

If you cant be bothered to sift through the output or check in the console, you can assure it is in a running state with this command ```az vm get-instance-view --name datacenter-vm --resource-group kml_rg_main-ad3a2cd9149d4252 --query instanceView.statuses[1] --output table```

## Thoughts and Takeaways

Good little exercise. Tasks like this are true to real day to day cloud administration. Get familiar with the CLI, I promise once you get into the swing of it, its so much faster and more productive, plus you can start thinking about IaC and scripting deployments so they are repeatable with less room for human error. Thime for tea. 
