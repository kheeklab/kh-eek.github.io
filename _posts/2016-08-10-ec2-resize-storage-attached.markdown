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

 ```xvda                               202:64   0   32G  0 disk```  <br />
 ```└─xvda1                            202:65   0   8G  0 part /``` <br />

Our goal is to make xvde1 use the whole available space from xvde. Here's how to resize your partition:

```fdisk /dev/xvda``` (the disk name, not your partition) This enters into the ```fdisk``` utility. </br>

 1. ```u``` #Change the display to sectors
 2. ```p``` #Print info
