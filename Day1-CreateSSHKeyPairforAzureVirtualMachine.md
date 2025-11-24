## The Problem

The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the Azure cloud. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition. To achieve this, they have segmented large tasks into smaller, more manageable units. This granular approach enables the team to execute the migration in gradual phases, ensuring smoother implementation and minimizing disruption to ongoing operations. By breaking down the migration into smaller tasks, the Nautilus DevOps team can systematically progress through each stage, allowing for better control, risk mitigation, and optimization of resources throughout the migration process.

For this task, create an SSH key pair with the following requirements:

1. The name of the SSH key pair should be devops-kp.

2. The key pair type must be rsa.

## The Solution
 ** The CLI commands will use the resource group name my demo tenant had. Yours will probably be different. 
 
Step one was to sign into the Azure tenant with the credentials provided. I did not include them in 'The Problem' as they will expire within the hour and... I'm not sharing my creds publicly :smile:

To do this run ```az login``` and enter the code provided on the screen to allow the device CLI access. Then sign in with the credentials.

The next step is to select the correct subscription. In this case, just press enter. 

Now, you need to determine what resource group to put the SSH Key into. But how do you determine that without a GUI? Simples! ```az group list```

Then, the final step is to create the SSH Key pair in the resource group. To do this run ```az sshkey create --name "devops-kp" --resource-group "kml_rg_main-75ed5ef16fcc4be8"```.

Once that has run and shown you the output, you can verify with ```az sshkey list --resource-group "kml_rg_main-75ed5ef16fcc4be8"```. Providing it is there, job done :smile: 

## NOTE!

You can!! do all of this in the Azure GUI (I tried and confirmed) however, I would highly recommend you don't. In the real world, CLI is preffered by most employers. 
