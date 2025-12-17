## The Problem

The Nautilus DevOps team is migrating services to Azure. They are breaking down tasks to ensure better control and optimization. You are tasked with attaching an existing data disk to a virtual machine (VM).

An existing VM named datacenter-vm and a managed disk named datacenter-disk already exist in the East US region.

1. Attach the disk datacenter-disk to the VM datacenter-vm as a data disk.
2. Ensure the disk is attached to the VM datacenter-vm.
3. Make sure that the virtual machine initialization has been completed before submitting this task.

## The Solution

First of all, I veirfied the information provided as you always should with ```az vm list``` to check the VM and ```az disk list``` respectivly. Both these commands did actually give me the name of the resource group but if you're unsure, run ```az group list``

Once I verified all the information, to attach the disk I ran  ```az vm disk attach -g KML_RG_MAIN-085BB31E099A4FCF --vm-name datacenter-vm --name datacenter-disk```

Lastly, I had to verifiy that the disk was infact attached, to do this I ran ```az vm show --resource-group KML_RG_MAIN-085BB31E099A4FCF --name datacenter-vm --query "storageProfile.dataDisks"```

And there it is in all its glory:
<img width="1017" height="572" alt="image" src="https://github.com/user-attachments/assets/484ac0f9-fb4c-4ffd-8a55-f042356d925f" />

## Thoughts and takeaways

That was fun! I've never actually attached a disk to a vm in the CLI so that was a first for me. Its normally something I'd do in the GUI but as the purpose of these challenges is to challenge yourself, why not try something new? :smile: time for tea. 
