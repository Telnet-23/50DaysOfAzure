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

After that I viewd the key in /root/.ssh/id_rsa.pub using ```cat /root/.ssh/id_rsa.pub``` and copied the key to a notepad.

The I did the following:
```ssh azureuser@172.184.152.48```

Then I elevated my permissions to the root user with 
```sudo su``` then navigated to the root home directory with ```cd ~```

The confirmed the directory was present with ```ls -a``` followed by ```cd .ssh```

At this point I opene the authorised_keys file with ```vi authorised_keys``` and pasted the contents of the key into that file then ```:wq!```

I then confirmed the key want in correctly with ```cat authorised_keys``` then left the vm with ```exit```

Once I exited the vm, I ran ```ssh root@172.184.152.48``` and boom, I was in as root. 

## Thoughts and takeaways

That challenge was weirdly hard. I cant quite explain it but when I SSH'd into the box and swithed to root, I added the key in the correct place but the ssh as root still didnt work. I had to navigate to the home directory with ```cd ~``` before going to .ssh. This doesnt really make sense as ```pwd``` told me I was already there. I'm sure theres a reason. Also I reckon theres a better way of doing this then copying and pasting but I couldnt get SCP to work without the root credentials so maybe not. Let me know if you know a better way :smile: time for tea. 

