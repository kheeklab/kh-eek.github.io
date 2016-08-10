---
published: true
title: EC2 resize storage attached
layout: post
tags: [EC2, Linux]
categories: [EC2]
---
Here' what to do:

 ```df -h``` #print the name of your boot partition
 ```lsblk``` #show info on all your block devices

You'll see from that output what the name of the disk is of your root partition. For example, you probably see something like this: <br />

 ```xvde                               202:64   0   32G  0 disk``` <br />
 ```└─xvde1                            202:65   0   8G  0 part /```