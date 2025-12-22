## The Problem
The Nautilus DevOps Team deployed an Nginx server on an Azure VM in a public VNet named datacenter-vnet. However, the server is still inaccessible from the internet.

As a DevOps team member, complete the following tasks:

1. Verify VNet Configuration: Ensure datacenter-vnet allows internet access.
2. Attach Public IP: A public IP named datacenter-pip already exists. Attach this public IP to the VM datacenter-vm to make it accessible from the internet.
3. Ensure Accessibility: Confirm the VM datacenter-vm is accessible on port 80.

Use the provided Azure credentials to troubleshoot and resolve the issue.

## The Solution

I'm going to address this one issue at a time. 

The first issue it to confirm that the vnet can get out to the internet. If you do not understand routing or the idea od a 'defsult static route', this is a great example of what this is and why its required. So as a brief lesson...

A default static route is a route on a firewall (or in this case a VNET) that essentially states that if the route to a device is not in the routing table, go here. On a firewall this will pretty much always point to the gateway which in turn goes out to the internet. This route is configured as 0.0.0.0/0.0.0.0 because that contains every single possible IPv4 address. So its saying, if theres no route, go here for literally everything else. 

VNET are the same. So now with that bit of info, Open the VNET and check the subnets, you will see that the subnet created has an associated route table. Click on that. Right away you can see that there is a rule blocking the internet. You basically need to re-create or edit that to allow 0.0.0.0/0.0.0.0 to the destination 'Internet' which in Azure is essentially the gateway. 
<img width="1263" height="616" alt="Screenshot 2025-12-22 at 23 06 03" src="https://github.com/user-attachments/assets/35245861-8436-4c79-879a-ead1c4baf46b" />

Then the next problem, Open the already created public IP and associate it with the VM Nic. Nice and simple. 

Lastly, Add inbound port 80 to the NSG. 

After doing that, I ran ```curl 20.184.131.202``` from the host to ensure it worked but the connection was refused on port 80 so I had to do a little more troubleshooting. 

I connected to the VM with SSH and ran ```systemctl status nginx``` and found nginx was not installed. SO! Naturally I had to

```
sudo apt install -y nginx
sudo systemctl start nginx
sudo systemctl enable nginx
systemctl status nginx
```

I then again run ```curl 20.184.131.202``` this time with more success. So now thats confirmed, the challenge is complete. 

## Thoughts and takeaways

That was a fun challenge. A fair amount to cover off there and work out. Thats the point :smile: Tea time. 
