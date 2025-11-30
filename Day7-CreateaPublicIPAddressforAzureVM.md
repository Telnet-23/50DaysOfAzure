## The Problem
The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the Azure cloud. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition. To achieve this, they have segmented large tasks into smaller, more manageable units. This granular approach enables the team to execute the migration in gradual phases, ensuring smoother implementation and minimizing disruption to ongoing operations. By breaking down the migration into smaller tasks, the Nautilus DevOps team can systematically progress through each stage, allowing for better control, risk mitigation, and optimization of resources throughout the migration process.

For this task, allocate a Public IP address, name it as nautilus-pip.


## The Solution
So I'll be honest, I didn't fully understand this challenge. On the surface its simple however, the name of it and what you have to do do not align. I opend the cli and ran ```az group list``` and found a resource group. I then ran ```az network vnet list``` and found no vnets. tHEN i RAN ```AZ VM LIST``` and found no VMS.

This is where it confused me. The task title suggests you're associated the public IP with a vm. But there is no vm made. It doesnt tell you to make a vm, so I didnt. I created the public IP as specifed using  ```az network public-ip create --name nautilus-pip --resource-group kml_rg_main-733467a2051d423c```. The command ran, the output verified it worked so I clicked 'check' expecting it to fail and give me a reason as to why, but it didnt it succeeded.

The title of the challange should be 'Create a public IP in Azure'. 

## Thoughts and takeaways
Yeah it was okay, aside from the confusion as to what I was actually meant to be doing. I guess this is why taking a minute or 2 to assess the environment with list and show commands is so important. Anyway. Time for tea.  
