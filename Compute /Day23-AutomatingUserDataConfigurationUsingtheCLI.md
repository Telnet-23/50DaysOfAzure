## The Problem 

The Nautilus DevOps Team is working on setting up a new virtual machine (VM) to host a web server for a critical application. The team lead has requested you to create an Azure VM that will serve as a web server using Nginx. This VM will be part of the initial infrastructure setup for the Nautilus project. Ensuring that the server is correctly configured and accessible from the internet is crucial for the upcoming deployment phase.

As a member of the Nautilus DevOps Team, your task is to create a VM using Azure CLI with the following specifications:

Instance Name: The VM must be named nautilus-vm.

Image: Use any available Ubuntu image to create this VM.

Custom Script Extension/User Data: Configure the VM to run a custom script during its launch. This script should:

Install the Nginx package.
Start the Nginx service.
Network Security Group (NSG): Ensure that the VM allows HTTP traffic on port 80 from the internet.

Instructions:

Use Azure CLI commands to set up the VM in the specified configuration.
Ensure the VM is accessible from the internet on port 80.
The Nginx service should be running after setup.


Use the Azure CLI commands to complete the task.

## The Solution

As always, establish what the Resource group is called
```az group list```

Then, in the client, I built a very basic script using ```vi script.sh``` which looked like this. 
```
#!/bin/bash

sudo apt update
sudo apt install -y nginx
sudo systemctl start nginx
sudo systemctl enable nginx
```
With the script made, I built the VM and passed the script in as custom data. I had a real hard time finding out how to actually do this. All the documentation was showing was JSON which isnt really what I'm trying to achieve. Reddit to the rescue!
```az vm create --resource-group kml_rg_main-8c81fba29f1f43b5 --name nautilus-vm --image Ubuntu2204 --size Standard_B2s --storage-sku Standard_LRS --os-disk-size-gb 30 --admin-username azureuser --generate-ssh-keys --location eastus --custom-data script.sh```

Once that completed, which shocked even me. It worked first try. But once it built, I used SSH on to the vm and confirmed that nginx was running. 
```systemctl status nginx```
<img width="967" height="518" alt="image" src="https://github.com/user-attachments/assets/fc02578b-5bd7-4532-bcda-cf0c5f9fce0b" />

Then I left the vm and found out what the NSG was called using the list command below. This confirmed that port 22 was open (which I knew because I used SSH already) but that was the only open port. 
```az network nsg list```

I edited the NSG to allow port 80 inbound. 
```az network nsg rule create --resource-group kml_rg_main-8c81fba29f1f43b5 --nsg-name nautilus-vmNSG --name inbound80 --priority 100 --direction Inbound --access Allow --protocol Tcp --destination-port-ranges 80```

To verify that took effect, I again listed the NSG. 
```az network nsg list```

And my final test was to curl the public IP from the host and confirm that the web page showed. Once that came back as intended. Mission accomplished. 
```curl 20.169.152.149```

## Thoughts and takeaways
That was great. It was only a couple of days ago that I said I need to work out how to pass custome executions into builds using Azure CLI and here we are. My hand was forced :smile: With that in mind; time for tea. 
