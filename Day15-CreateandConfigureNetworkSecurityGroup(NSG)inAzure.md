## The Problem 

The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the Azure cloud. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition. To achieve this, they have segmented large tasks into smaller, more manageable units. This granular approach enables the team to execute the migration in gradual phases, ensuring smoother implementation and minimizing disruption to ongoing operations. By breaking down the migration into smaller tasks, the Nautilus DevOps team can systematically progress through each stage, allowing for better control, risk mitigation, and optimization of resources throughout the migration process.

For this task, create a network security group (NSG) with the following requirements:

1. Name of the NSG should be xfusion-nsg.

2. Add an inbound security rule named Allow-HTTP for HTTP service on port 80, with the source CIDR range of 0.0.0.0/0.

3. Add another inbound security rule named Allow-SSH for SSH service on port 22, with the source CIDR range of 0.0.0.0/0.

## The Solution

Reference docs: https://learn.microsoft.com/en-us/cli/azure/network/nsg?view=azure-cli-latest

So I have attached the docs above on how to do it in the CLI but my CLI was bigging out and not loading as you can see:
<img width="1124" height="550" alt="image" src="https://github.com/user-attachments/assets/9cca3e5f-ecd5-4eca-bed7-17500c174752" />

So I'm going to have to GUI it. Which is a bit dissapointing because I've done that plenty, I dont think I have ever CLI'd an NSG. Oh well. 

Open up Azure and go to the Resource Group then 'Create' and add a Network Security Group. Giv it the required name then when its build, open it and click 'Settings' > 'Inbound Security Rules' and create the two rules. They'll look like this.
<img width="565" height="711" alt="image" src="https://github.com/user-attachments/assets/4ce89a8c-6fad-496f-8eff-11f03a837468" />

Once they're both built you'll see them in the console like this
<img width="1677" height="355" alt="image" src="https://github.com/user-attachments/assets/edd9f213-0691-438e-a434-e149c1d16ea2" />

## Thoughts and takeaways
Its a shame my CLI didnt work. I'll lab this in my own tenent and get familiar with NSG's in CLI. oh well. Time for tea. 

