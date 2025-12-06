## The Problem

The Nautilus DevOps team is working on setting up secure SSH access for their virtual machines in Azure. One of the requirements is to add the SSH public key of the root user from the Azure client host (landing host) to the xfusion-vm Azure VM's authorized_keys file. This ensures secure and password-less SSH access to the VM.

Task Details:
1. VM Details:

The VM is named xfusion-vm and is running in the West US region. The default SSH user is azureuser — use this user to connect to the VM.
You need to add the root user's SSH public key from the Azure client host to the authorized_keys file of the VM's root user.
The SSH public key of the root user on the Azure client host is located at /root/.ssh/id_rsa.pub.

2. Public Key Addition:

Copy the public key located at /root/.ssh/id_rsa.pub on the Azure client host to the authorized_keys file of the root user on xfusion-vm.
Ensure that the proper permissions for the .ssh folder and authorized_keys file are set on the VM.

3. Verification:

After adding the public key, make sure that you are able to SSH into the xfusion-vm VM as the root user from the Azure client host without needing a password.

Important Notes:
Ensure that the VM is up and running before attempting to SSH.
You may need to adjust the firewall or security group rules for the VM to allow SSH access.

## The Solution

First, I tried to SSH using the VM name but it failed (DNS, its always DNS). So I instead ran ```az network public-ip list``` and obtained the public IP.

The I did the following:
```ssh azureuser@172.184.152.48```

Now it was time to confirm if the directory exisited and if not, create it. So you're aware, It did not. I made the directory and set the permissions to allow the user rwx, with the group having no permission
```sudo mkdir -p /root/.ssh && sudo chmod 700 /root/.ssh```

Then I created the authorised_keys directory and set the permissions and chaged the ownership user and group to root
```sudo chmod 600 /root/.ssh/authorized_keys```
```sudo chown root:root /root/.ssh/authorized_keys```

