## The Problem
The Nautilus DevOps team is strategically planning the migration of a portion of their infrastructure to the Azure cloud. Acknowledging the magnitude of this endeavor, they have chosen to tackle the migration incrementally rather than as a single, massive transition. Their approach involves creating Virtual Networks (VNets) as the initial step, as they will be provisioning various services under different VNets.

1. Create a Virtual Network (VNet) named xfusion-vnet in the East US region with 192.168.0.0/24 IPv4 CIDR.

## The Solution

As always in Azure, the first thing I checked was ```az group list``` to identify which resource group(s) existed. The was 1 so I used that as the challenge did not say 'Create a new group'. 

I then ran the commmand ```az network vnet create --name xfusion-vnet --resource-group kml_rg_main-4d4112ba2b4e41a1 --location eastus --address-prefix 192.168.0.0/24``` to complete the task. It ran with no issues. 

I used ```az network vnet list``` to get a list of the networks just to verify (The output of the command above does confirm it exists but always check twice). 

And thats it, done!

## Thoughts and takeaways. 

I kind of feel like this challenge was more or less the same as yesterdays? Was i supposed to do one in the GUI and one in the CLI? Who knows. Still, nice refresher and quick little bit of practice never hurts. 
