## The Problem
The Nautilus DevOps team is currently working on setting up a simple application on the Azure cloud. They aim to establish an Azure Load Balancer in front of a Virtual Machine (VM) where an Nginx server is currently running. While the Nginx server currently serves a sample page, the team plans to deploy the actual application later.

1. Set up an Azure Load Balancer named xfusion-lb.
2. Configure the Load Balancer’s frontend IP configuration with the name xfusion-lb-ip and assign a public IP address with the same name (xfusion-lb-ip).
3. Create a backend pool named xfusion-backend-pool and add the VM running Nginx to this pool.
4. Create a health probe named xfusion-health-probe on port 80 to check the VM's health.
5. Set up a load balancer rule named xfusion-lb-rule to route traffic on port 80 to the backend pool on port 80.
6. Add an inbound rule to the existing NSG of the VM to allow HTTP traffic on port 80.


## The Solution




Inbound Rule
<img width="1832" height="657" alt="image" src="https://github.com/user-attachments/assets/8e3cd937-4401-4e6e-b2c7-cd0d5e6b5fa8" />

<img width="806" height="653" alt="image" src="https://github.com/user-attachments/assets/f9396847-1228-451e-b2f2-f22e3139d68d" />

