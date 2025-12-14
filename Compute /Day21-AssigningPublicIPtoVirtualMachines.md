## The Problem
The Nautilus DevOps Team has received a new request from the Development Team to set up a new Azure Virtual Machine (VM). This VM will be used to host a new application that requires a stable public IP address. To ensure that the VM has a consistent public IP, a Static Public IP address needs to be associated with it. The VM will be named datacenter-vm, and the Static Public IP will be named datacenter-pip. This setup will help the Development Team to have a reliable and consistent access point for their application.

1. Create an Azure VM named datacenter-vm using any available Ubuntu image, with the VM size Standard_B1s.

2. Generate an SSH public key on the azure-client host and associate it with the VM for SSH access.

3. Associate a Static Public IP address named datacenter-pip with this VM.

4. Ensure the VM is accessible via SSH using the generated public key.

## The Solution

Right, I have tried to do this via the CLI several times now and I cannot get it to work, so for the sake of moving forward, This ones going to be console based. 

1. Create a new ssh key on the azure-client with ```ssh-keygen -t rsa``` then run ```cat /root/.ssh/id_rsa.pub```. Leave that on the screen, you'll need it in a minute.

2. Sign into Azure with the given credentials

3. Give the machine the specified name and build it as a B1 Ubuntu box as requested. It cannot have any infrastructre redundancy to use the B series of VM's. The key thing here is to set the SSH public key source to 'Use an existing public key' and paste in the public key you made earlier. 
<img width="921" height="543" alt="Screenshot 2025-12-14 at 19 36 07" src="https://github.com/user-attachments/assets/365c4a1a-8750-4597-a592-3ac160d4fb72" />

4. make sure you use standard storage and not premium or the deployment will fail.

5. Create a public IP in 'Networking' and name it as specified.
<img width="1305" height="667" alt="Screenshot 2025-12-14 at 19 37 28" src="https://github.com/user-attachments/assets/881ad323-19f1-45ee-a663-fa7fefa2f9aa" />

Once the VM is created, obtain the public IP from the resource and ssh into it with the user you made (azureuser by default). If it has worked, you wont get prompted for a password. 
<img width="691" height="449" alt="Screenshot 2025-12-14 at 19 50 04" src="https://github.com/user-attachments/assets/1918506b-6e04-4304-bd5d-cb6821f9ebc7" />

## Thoughts and takeaways
This one was weirdly difficult. I mean, it wasnt, but it was in the CLI. I hit issue after issue and I couldnt work out how to add the public key to the vm during the build using the CLI. I'm sure there's a way and I'll keep digging to see if I can work it out. Time for tea.


