## The Problem
The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the Azure cloud. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition.

For this task, create a Virtual Network (VNet) named nautilus-vnet and one subnet named nautilus-subnet within the VNet in the East US region. Make sure the IPv4 address range is 10.0.0.0/16.

## The Solution

First up I ran ```az group list ``` to get the name of my resource group. 

Then I ran the command to create the vnet and it's specified subnet within the East US Region
```az network vnet create --name nautilus-vnet --resource-group kml_rg_main-87c7785b135049a0 --location eastus --address-prefix 10.0.0.0/16 --subnet-name nautilus-subnet --subnet-prefix 10.0.1.0/24```

Once done, I double verified with 
```az network vnet list```

And with that, it's done.

## Thoughts and takeaways
I somewhat feel the last 3 days have all kind of been the same challenge. Simple enough once you get the jist of it. I guess the key thing here is take the time to understand subnetting. One day it does just click I promise :smile:
