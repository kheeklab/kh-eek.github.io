---
published: true
title: EC2 resize storage attached
layout: post
tags: [EC2, Linux]
categories: [EC2]
---
Here' what to do:

 ```df -h``` #print the name of your boot partition <br />
 ```lsblk``` #show info on all your block devices

You'll see from that output what the name of the disk is of your root partition. For example, you probably see something like this: <br />

 ```xvda                               202:64   0   30G  0 disk```  <br />
 ```└─xvda1                            202:65   0   8G  0 part /``` <br />

Our goal is to make xvde1 use the whole available space from xvda. Here's how to resize your partition:

```fdisk /dev/xvda``` (the disk name, not your partition) This enters into the ```fdisk``` utility.

 1. ```u``` #Change the display to sectors
 2. ```p``` #Print info
 3. ```d``` #Delete the partition
 4. ```n``` #New partition
 5. ```p``` #Primary partition
 6. ```1```  #Partition number
 7. ```2048``` #First sector
 8. Press Enter to accept the default
 9. ```p``` #Print info
 10 ```a``` #Toggle the bootable flag
 11. ```1``` #Select partition 1
 12. ```w``` #Write table to disk and exit
 
Now, reboot your instance: ```reboot```

After it comes back do:

```resize2fs /dev/xvda1``` (the name of your partition, not the block device)

And finally verify the new disk size:  df -h