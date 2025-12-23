## The Problem
The Nautilus DevOps Team has received a request from the Development Team to set up a new repository for better code management. They need a secure way to access the repository using SSH.

1. Create an organization with the name it picks up by default ( do not use any custom name ), create a project named nautilus-project under it and an Azure DevOps repository named nautilus-repo under the same.
   
2. Add the root user's SSH public key from azure-client host to the Azure DevOps SSH keys.
   
3. Create an SSH config under /root/.ssh/config on azure-client host and make changes to authenticate with the created repository.
   
4. Clone the new repository on azure-client host under /root.
   
5. Add the contents of /root/pyapp directory to this repository, then add, commit, and push the changes to the repository. You might need to set the git user and email to commit your code; you can use any email ID and user name for that.

Please use the same credentials provided for logging into the Azure portal to log in to the Azure DevOps portal.

## The Solution

I'm not going to try this in the CLI, I started looking at how and trying to build a plan but even at step 2, I couldnt find a way to add the ssh key to the repo in the Dev tenant with the CLI. I'm sure theres a way and I'll certainly keep looking but I couldnt find one off the bat. 

So first of all, sign into the tenant and add a repo as stated.


** NOTE** And this is where this lab stops. For the life of me, I cannot open the DevOps tenant. it just re-directs to portal.azure.com. I've let KodeKloud know but for now, I cannot proceed. 
