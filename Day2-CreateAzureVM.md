## Note
Complete this task in the Azure GUI. Only because! Tomorrows challenge is the same from what I can see, but via the Azure CLI. 

## The Problem
The Nautilus DevOps team is planning to migrate a portion of their infrastructure to the Azure cloud incrementally. As part of this migration, you are tasked with creating an Azure Virtual Machine (VM).

The requirements are:

1) Use the existing resource group.

2) The VM name must be datacenter-vm, it should be in West US region.

3) Use the Ubuntu 22.04 LTS image for the VM.

4) The VM size must be Standard_B1s.

5) Attach a default Network Security Group (NSG) that allows inbound SSH (port 22).

6) Attach a 30 GB storage disk of type Standard HDD.

7) The rest of the configurations should remain as default.

## The solution 

Once you open the Azure Portal you want to click on 'Virtual Machines' then 'Create +' and start building the VM. On the first window, you can achieve tasks 1-5. Below you can see I have told the VM that it belongs in the exisiting resource group, added the name 'datacenter-vm' and specified the region as 'West US', Chosen the 'Ubuntu 22.04 LTS' image and set the size the 'Standard_B1'

<img width="1027" height="797" alt="image" src="https://github.com/user-attachments/assets/47e71b3b-0e09-4d36-a82e-2fe75f8a9cd6" />

If you scroll down a little, you can specifiy to authenticate using SSH, doing this with automatically create an NSG that allows inbound port 22 as 22 is the port for SSH.
<img width="940" height="666" alt="image" src="https://github.com/user-attachments/assets/90c3ea14-9fea-4383-a46f-77986af53185" />

Proceed with the setup until you get to 'OS Disk' and as stated above, specify a 30GB HDD. 
<img width="928" height="587" alt="image" src="https://github.com/user-attachments/assets/d6590865-3098-4a11-bba4-dbf0e0521aba" />

SSH onto the machine using ```ssh azureuser@publicip```. Then enter the password you set and you're done. 

If like me you didn't use a password and instead opted for an SSH Public Key source, you would have downloaded a Private Key when you created the resource. This will need to use ```ssh -i /path/to/key azureuser@publicip```.

## Thoughts

Nice little simple one. I think for anybody trying to learn Linux, this lab is actually great. If you spun up the VM you did here in your own Azure Tenant, it would proably cost you about £7 a month if that. Especially if you remember to turn it off when you're not using it. You should however, at the very least, use the NSG to lock down SSH access to your home IP or where ever you tend to lab from.

As mentioned previously, creating and manageing cloud resources in the CLI is generally preferred but you should still be familiar with the GUI. It's nice to know how to achieve the same result in both as I'm sure we'll find out tomorrow. Tea time. 
