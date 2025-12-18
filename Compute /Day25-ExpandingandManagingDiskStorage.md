## The Problem

The Nautilus DevOps team needs to expand the storage capacity of an existing virtual machine and add an additional data disk to support increased workloads. This task requires resizing the existing VM disk and mounting a new data disk to the VM.

As a member of the team, perform the following steps:

1) Expand the existing VM nautilus-vm disk from 32Gi to 64Gi.

2) Also create a new standard HDD data disk named nautilus-disk of 64Gi and mount the disk to VM nautilus-vm at location /mnt/nautilus-disk.

## The Solution

I'm going to break this down into 2 sections because to me, this is 50% Azure admin and 50% Linux admin. Which is fine but to make it easier to digest :smile:

STEP 1

First get all the required information about the existing disk such as resource group and confirming its current size.
```az disk list```

Then before you can do anything, stop and deallocate the VM
```
az vm stop --name nautilus-vm --resource-group KML_RG_MAIN-2E98568732C146E8
az vm deallocate --name nautilus-vm --resource-group KML_RG_MAIN-2E98568732C146E8
```
With the VM stopped, you can resize it's attached disk 
```az disk update --name nautilus-vm_disk1_0efd1164ddf941aaaeb9d11ae8ec4ec4 --resource-group KML_RG_MAIN-2E98568732C146E8 --size-gb 64```

And while it's off, you might as well create the new disk and attach it to the VM
```
az disk create --name nautilus-disk --resource-group KML_RG_MAIN-2E98568732C146E8 --size-gb 64 --sku Standard_LRS
az vm disk attach --resource-group KML_RG_MAIN-2E98568732C146E8 --vm-name nautilus-vm --name nautilus-disk
```
Then start the VM again now that the disk changes have been made. 
```az vm start --name nautilus-vm --resource-group KML_RG_MAIN-2E98568732C146E8```

Obtain the public IP associated with the VM to access it via SSH
```az network public-ip list```

STEP 2

There maybe a simpler way of doing this, but I'm far from uncomfortable in Linux so I figured I'd go all in. The task didn't ask you format the disk or anything but if you plan on using it, you'll need to format the disk so this is how you do it. 

SSH into the machine
```ssh azureuser@52.241.144.34```

Lisk all disks on the machine to confirm what your new disk is called. You will see it does not have a mount point and is 64GB. All disks (if you're unaware) are in the /dev directory in Linux. 
```lsblk```

Now we can format the disk using fdisk. Press enter on all the defaults to use the full disk as creating seperate partitions was not requested as part of the task. Once you've done that, enter ```w``` to write your changes.
```sudo fdisk /dev/sda```

Now lets make an ext4 file system on that partition. 
```sudo mkfs.ext4 /dev/sda```

Once you've done that, create the directory in /mnt
```sudo mkdir /mnt/nautilus-disk```

Then, if you edit fstab, the disk will auto mount upon reboot. Below is the layout of the entry you will use to achieve this. 
```/dev/sda /mnt/nautilus-disk ext4 defaults 0 0```

If you don't want to reboot the server (frankly I woundn't in this challenge as I have noidea for the lab will behave), you can remount all the disks. This command uses the fdisk file as its source of truth so if there is an error in your entry, it will tell you.
```sudo mount -a```

And finally, just for good measure, check your disk is now mounted with the correct mount path. 
```lsblk```

Mission complete :smile:

## Thoughts and takeaways

Nice Thursday morning challenge. I quite enjoyed that. This isnt something I've ever done in the CLI, only the GUI so great little bit of learning. I'm not sure this was faster in the cli then it is in the GUI but it might just be because I was having to google things. Bit more practice and I'm sure it's way faster like pretty much everything else in Azure. Time for tea. 
