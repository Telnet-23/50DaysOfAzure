## The Problem

The Nautilus DevOps team is expanding their Azure infrastructure and requires the setup of a private Virtual Network (VNet) along with a subnet. This VNet and subnet configuration will ensure that resources deployed within them remain isolated from external networks and can only communicate within the VNet. Additionally, the team needs to provision a Virtual Machine (VM) under the newly created private VNet. This VM should be accessible over SSH from within the VNet only, allowing for secure communication and resource management within the Azure environment.

The name of the VNet must be nautilus-priv-vnet, create a subnet named nautilus-priv-subnet under the same. Further, create a Virtual Machine named nautilus-priv-vm under this VNet. Additionally, create a Network Security Group (NSG) named nautilus-priv-nsg, and ensure that the NSG rules for the VM allow access only from within the VNet's CIDR block. Ensure all resources are created in the East US region.

## The Solution

In order to make this one work, I had to do it in the GUI as the CLI was not allowing me to specify a different location to the existing resource group and I apprently did not have permission to create a new resource group. So!

So, I created a VNET called nautilus-priv-vnet and a subnet in there called nautilus-priv-subnet with a 10.0.0.0/16 CIDR block. I then made a VM called nautilus-priv-vm and in the creation of this, I put it in the nautilus-priv-subnet and specified that I do not want a public IP and I did not create a security group with it as by default, that will allow port 22 in form anywhere. It doesnt have a public IP, but thats not the point. 

I made an NSG called nautilus-priv-nsg in the East US region then configuired it to allow inbound SSH traffic on port 22 from 10.0.0.0/16 to 10.0.0.0/16 and applied it to the NIC on my VM. 

And thats it, nice and simple :smile:

## Thoughts and takeaways

This one kept failing for me stating that the CIDR block was not included in my NSG... It was. I eventualy configuredit and then went for a cup of tea and checked out and it worked so maybe a timing issue? Seems odd but it worked. So with that, time for more tea. 
