## The Problem

The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the Azure cloud. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition. To achieve this, they have segmented large tasks into smaller, more manageable units. This granular approach enables the team to execute the migration in gradual phases, ensuring smoother implementation and minimizing disruption to ongoing operations. By breaking down the migration into smaller tasks, the Nautilus DevOps team can systematically progress through each stage, allowing for better control, risk mitigation, and optimization of resources throughout the migration process.

Create a managed disk with the following requirements:

  - Name of the disk should be nautilus-disk.

  - Disk type must be Standard_LRS.

  - Disk size must be 2 GiB

## The Soultion

First of all I found the resource group with ```az group list```

Next up, I ran the following command to created the disk as specified ```az disk create --resource-group kml_rg_main-e76a14c1af6f4ff2 --name nautilus-disk --size-gb 2 --sku Standard_LRS```

Then I confirmed with ```az disk list```

## Thoughts and takeaways
Nice easy one on a Sunday morning. I like that these Azure challenges (so far at least) are really making sure the fundations are there. Alot of it so far has been around VM's and networking but from what I can see, we have some storage coming up and more networking plus some more intense bits like AKS which will be fun with my newly found Kubernetes baseline obtained via the 100 days of DevOps course. :smile: tea time. 
