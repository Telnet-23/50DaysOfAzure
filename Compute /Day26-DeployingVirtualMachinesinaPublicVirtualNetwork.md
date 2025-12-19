## The Problem

The Nautilus DevOps Team has received a request from the Networking Team to set up a new public VNet to support a set of public-facing services. This VNet will host various resources that need to be accessible over the internet. As part of this setup, you need to ensure the VNet has public subnets with automatic public IP assignment for resources. Additionally, a new VM will be launched within this VNet to host public applications that require SSH access. This setup will enable the Networking Team to deploy and manage public-facing applications.

Create a public VNet named devops-pub-vnet, and a subnet named devops-pub-subnet under the same, make sure public IP is being auto-assigned to resources under this subnet. Further, create a VM named devops-pub-vm under this VNet. Make sure SSH port 22 is open for this instance and accessible over the internet. Use the Azure portal to complete the task and ensure that SSH access is configured correctly.

## The Solution
Okay, so it says to use the portal but come on, you know me better then that. CLI is the best way to do anything right :smile:

First find out what the resource group is called
```az group list```

First up lets make the Virtual Network as requested:
```az network vnet create --name devops-pub-vnet --resource-group kml_rg_main-3a250a43fad4482e --address-prefix 10.0.0.0/16 --subnet-name devops-pub-subnet --subnet-prefix 10.0.0.0/24```

Now lets create an ssh key on the client machine
```ssh-keygen -t rsa```

And build a VM in that subnet
```az vm create --resource-group kml_rg_main-3a250a43fad4482e --name devops-pub-vm --image Ubuntu2204 --size Standard_B1s --storage-sku Standard_LRS --os-disk-size-gb 30 --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub --location eastus```

Once that builds you'll see the public IP so ssh into it
```ssh azureuser@20.42.92.104```

And thats it, All done :smile:

## Thoughts and takeaways
Was pretty good. I think this was the first challenge that had you build multiple resources that had to communicaate, the only thing missing in it really was creating a resource group but thats simple enough. Yeah. Good one. Time for tea. 
