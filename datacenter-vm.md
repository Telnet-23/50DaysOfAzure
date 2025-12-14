```az vm create --resource-group kml_rg_main-0a99db0bd3714119 --name datacenter-vm --image Ubuntu2204 --size Standard_B1s --storage-sku Standard_LRS --os-disk-size-gb 30 --admin-username azureuser --generate-ssh-keys```

```az network public-ip create --resource-group kml_rg_main-0a99db0bd3714119 --name datacenter-pip```

```az network nic ip-config update --name ipconfig1 --nic-name myVMNic --resource-group kml_rg_main-0a99db0bd3714119 --public-ip-address datacenter-pip```
