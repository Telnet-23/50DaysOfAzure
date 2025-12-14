## The Problem

The Nautilus DevOps team is in the process of migrating some of their workloads to Azure. One of the tasks involves creating a new Virtual Machine (VM) using the Azure CLI. The team does not have access to the Azure portal but can manage Azure resources via the azure-client host (the landing host for this lab).

1) Create a new Azure Virtual Machine named xfusion-vm using the Azure CLI.

2) Use the Ubuntu2204 image and set the VM size to Standard_B2s.

3) Make sure the admin username is set to azureuser and SSH keys are generated for secure access.

4) Use Standard_LRS storage account, disk size must be 30GB and ensure the VM xfusion-vm is in the running state after creation.

## The Solution

First of all, this lab opened with no login details so to check that the lab had not bugged out I ran ```az group list``` to verify what I suspected... the lab lauched with me already signed into the Azure tenant. Good! Now thats out the way, the fun bit. 

The secifications have been listed in the steps so the main thing to make sure you paste those details in exactly. I have already found the resource group by running the above command, your resource group will almost certainly be called something different. 
```az vm create --resource-group kml_rg_main-b093c0f5384d4120 --name xfusion-vm --image Ubuntu2204 --size Standard_B2s --storage-sku Standard_LRS --os-disk-size-gb 30 --admin-username azureuser --generate-ssh-keys```

Once that's built you'll see it's state is also 'VM Running' which is what we want.
<img width="1011" height="319" alt="image" src="https://github.com/user-attachments/assets/25f14a9c-6ae7-4885-a5de-1541289ecd48" />

For an extra step to verify and to ensure all is well, you might as well SSH into the VM as you already have the key on this lab VM
<img width="721" height="799" alt="image" src="https://github.com/user-attachments/assets/553d2d79-8877-4923-b4c9-0c388d2d63f2" />

Once you're happy with that, click 'Check' and thats it :smile:

## Thoughts

Lovely little lab. You may have realised how much faster that was then yesterdays challange where we did the same thing clicking through the GUI. This is declarative, quick and very easily repeatable with no real reason for human error. Time for a tea. 

