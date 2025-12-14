## The Problem
The Nautilus DevOps team has already set up a virtual machine and allocated a public IP address. The final task is to attach this public IP to the VM's network interface card (NIC).

An existing VM named datacenter-vm-pip and a public IP address named datacenter-pip already exist.

1. Attach the public IP datacenter-pip to the network interface of the VM datacenter-vm-pip.
2. Make sure the VM is properly assigned the public IP.

## The solution

First I gathered the required information such as the resource group name with ```az group list``` verified the VM was there with ```az vm list``` and checked the public IP with ```az network public-ip list```

The command to make this change happen is as followed, you just assocaite the public IP with the exisiting nic on the vm in the same resource group and give the config a name. NOW! This is exactly how you do it. The terminal in KodeKloud however kept telling me that the resource 'datacenter-pip' does not exisit in the resource group. It did, I checked it.... over 50 times. 
```az network nic ip-config update --name ipconfig1 --resource-group kml_rg_main-c42ff1f453794498 --nic-name datacenter-vm-pipVMNic --public-ip-address datacenter-pip```

As it bugged out, I completed this challenge in the console. I opened the resource group that the public IP was 100% in, then opened the public IP, clicked 'Associate' then specified the NIC name datacenter-vm-pipVMNic in the same resource group and that was it. 

I then verifed it in the CLI with 
```az vm show --name datacenter-vm-pip --resource-group kml_rg_main-c42ff1f453794498```

## Thoughts and takeaways
It worked, thats the main thing, not a particularly hard challenge but it was unbelievably frustratiing that the CLI would not let me complete the task. If you dont believe me that it issue was not me, check the MS documentation, I did when I though I was doing something wrong https://docs.azure.cn/en-us/virtual-network/ip-services/virtual-network-static-public-ip?tabs=azurecli.
Anyway, time for a tea. 
