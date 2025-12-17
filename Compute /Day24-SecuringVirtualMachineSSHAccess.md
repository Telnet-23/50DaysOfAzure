## The Problem
The Nautilus DevOps team needs to set up a new Virtual Machine (VM) on the Azure cloud that can be accessed securely from their landing host (azure-client). Follow the steps below to complete this task:

1. Create an SSH Key: On the azure-client host, check if an SSH key already exists. If it doesn’t exist, create a new SSH key on the azure-client host that will be used for password-less SSH access.

2. Create a Virtual Machine: Use the Azure Portal or Azure CLI to create a new Virtual Machine named xfusion-vm in the westus region. Set the VM size to Standard_B1s and configure the VM with SSH access for the azureuser account using the newly created SSH key.

3. Configure SSH Access: Ensure that the SSH key from the azure-client host is added to the azureuser account on xfusion-vm, enabling secure, password-less SSH access from the azure-client host.

4. Verify Connectivity: Test the connection from azure-client to xfusion-vm using SSH to confirm that password-less access has been set up correctly.

Complete these tasks entirely within the Azure Portal or Azure CLI.

## The Solution

First lets made the key on the host ```ssh-keygen -t rsa```

Then list the groups to find out the resource group name```az group list```

And finally, create the VM. 
```az vm create --resource-group kml_rg_main-264aff194d5f44fe --name xfusion-vm --image Ubuntu2204 --size Standard_B1s --storage-sku Standard_LRS --os-disk-size-gb 30 --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub --location westus```

Then test you can SSH on and confirm that you do not need to enter a password. ```ssh azureuser@172.185.18.108``` and thats it :smile:

## The Solution
Nice challenge. I think I said the other day I didnt knonw how to put a pre-generated ssh key onto an Azure vm via CLI. Now I do :smile: thats why these challenges are great. Time for tea. 
