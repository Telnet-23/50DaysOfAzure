## The Problem

The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the Azure cloud. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition. To achieve this, they have segmented large tasks into smaller, more manageable units. This granular approach enables the team to execute the migration in gradual phases, ensuring smoother implementation and minimizing disruption to ongoing operations.

Create a Virtual Network (VNet) named devops-vnet in the East US region with any IPv4 CIDR block.

## The Solution

First of all, It's best practice to do this all in the CLI. I would also open the web portal too and get familiar with it and cross reference your work at the end but yes! Try and use the CLI as much as you can. 

Sign in with ```az login```

Next I'm going to run ```az group list``` to find the existing resource group. 

And the final stage is to create the VNET. I'm also going to create a subnet in that VNET for good measure. I'll explain this a little after but this is the command:

```az network vnet create --name devops-vnet --resource-group kml_rg_main-2d2639ee5b0648c9 --location eastus --address-prefix 10.10.0.0/16 --subnet-name MySubnet --subnet-prefix 10.10.10.0/24```

You will recieve an output the confirms it has been made, its name, its location etc. Job done. 

## Subnetting and VSLM
NOW! If you are new to subnetting, the above might seem a bit.... confusing, what is a CIDR? what does /16 and /24 mean and all that good stuff. So Let me break it down a bit and maybe this will help subnetting click for at least 1 person. 

IPv4 - IPv4 is a 32 bit address. The you will notice it is broken into 4 portions seperated by '.'. These sections are called octects because each one contains 8 bits, 8x4 = 32. 

A certain portion of addresses will be used up by the network to somewhat identify it as an individual network, this can be identifed in the subnet mask which translates also to the CIDR notation or /16, /24. 
A /16 means that the first 2 octects of an address space cannot change because they are ocupied by the network, the last 16 bits are fair game for host devices. 

In the above example, the network address is 10.10.0.0/16. I can have hosts on 10.10.0.1/16 all the way up to 10.10.255.254/16. That! is a big old subnet. So what do we do? We can either make the VNET small to begin with or! we can break it down into smaller subnets using Variable Lengh Subnet Masking or VSLM. 

With VSLM, I stated I want to take the 10.10.10.0/24 space and have that as it's own subnet. That means I've removing that range from the full CIDR block. So devices allocated and IP from 10.10.10.1-.254/24 can all talk to eachother as they will be o nthe same network. 

I could also make 10.10.20.128/25 and 10.10.1.0/22 if I saw fit. These are smaller and bigger subnets then a /24 respecivly but thats the glory. But notice that in all these, the first 2 octects do not change. They cannot due to the original poll these are being created from being a /16. 

Hopefully thats made sense to someone and made it click and doesnt just sound like the wafflings of a mad man. Time for a tea. 
