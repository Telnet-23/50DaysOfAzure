## The Problem

The Nautilus DevOps Team is working on setting up a new virtual machine (VM) to host a web server for a critical application. The team lead has requested you to create an Azure VM that will serve as a web server using Nginx. This VM will be part of the initial infrastructure setup for the Nautilus project. Ensuring that the server is correctly configured and accessible from the internet is crucial for the upcoming deployment phase.

As a member of the Nautilus DevOps Team, your task is to create a VM with the following specifications:

Instance Name: The VM must be named datacenter-vm.

Image: Use any available Ubuntu image to create this VM.

Custom Script Extension/User Data: Configure the VM to run a custom script during its launch. This script should:

  - Install the Nginx package.
  - Start the Nginx service.
  
Network Security Group (NSG): Ensure that the VM allows HTTP traffic on port 80 from the internet.

## The Solution

This one is pretty simple, Basically follow what you did yesterday around the VM build but also allow port 80 inbound as well as SSH:
<img width="855" height="454" alt="Screenshot 2025-12-15 at 21 02 27" src="https://github.com/user-attachments/assets/58d81869-fa74-4693-ae5f-7caba83a5932" />

Continue with teh task but add a short basic bash script to install, start and enable NGINX
<img width="912" height="472" alt="Screenshot 2025-12-15 at 21 02 51" src="https://github.com/user-attachments/assets/80f8a239-1e81-4067-af33-40e9fbe33646" />

Once thats done, Navigate to the public IP:
<img width="1319" height="407" alt="Screenshot 2025-12-15 at 21 07 21" src="https://github.com/user-attachments/assets/bed9153a-1386-4c2c-bda2-73fc1e8b2124" />

And thats it :smile:

## Thoughts and takeaway
That was simple enough. It's a great little lab though. A real deployment you'll likelt use. Time for tea. 
