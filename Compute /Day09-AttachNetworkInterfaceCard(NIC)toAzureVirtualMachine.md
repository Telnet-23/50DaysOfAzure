## The Problem

The Nautilus DevOps team is migrating services to Azure. They are breaking down tasks to ensure better control and optimization. You are tasked with attaching an existing network interface (NIC) to a virtual machine (VM).

An existing VM named devops-vm and a network interface named devops-nic already exist in the West US region.

1. Attach the network interface devops-nic to the VM devops-vm.
2. Ensure the NIC's status is attached before submitting the task.
3. Make sure that the virtual machine initialization has been completed before submitting this task.

## The Solution

First I verified the name of the resource group with ```az group list```

With that bit of info, I had all the details I needed so I checked the nics currently attached to the vm with 
```az vm nic list --resource-group kml_rg_main-a6928867186a4b7a --vm-name devops-vm```

To attach a NIC, you have to stop and deallocate a VM so I ran the following commands
```
az vm stop --resource-group kml_rg_main-a6928867186a4b7a --name devops-vm
az vm deallocate -g kml_rg_main-a6928867186a4b7a --vm-name devops-vm
```
I suspect there is a better way of doing both of these commands in one command but I'm not aware of it, or at least I wasnt when I did the challenge.

Once the VM is stopped and deallocated, you can add (attach) the nic to the vm 
```az vm nic add --nics devops-nic --resource-group kml_rg_main-a6928867186a4b7a --vm-name devops-vm```

You will get output once its done to confirm it worked. The start your vm again
```az vm start --resource-group kml_rg_main-a6928867186a4b7a --name devops-vm```

And finally, verify the NIC is now attached
```az vm nic list --resource-group kml_rg_main-a6928867186a4b7a --vm-name devops-vm```

## Thoughts and takeaways
I forgot to deallocate... I'll confess. I stopped it and tried to attach the NIC and it threw an error. We live we learn, thats the point :smile: time for tea. 
