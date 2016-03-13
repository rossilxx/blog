---
layout: post
title:  "linux misc skills"
date:   2016-02-24
author: rossi
categories: linux
---

Use the proc pseudo file-system to find your file back
----
Sometimes you may delete a file by mistake. We can find it back if some process still held the file descriptor.
+ First, find the process.<br>You can use `lsof` command like this:

  	lsof | grep deleted | grep myfile
  	less    4158    rossi    4r    REG    3,65    114383    1276722    /home/rossi/myfile (deleted)

+ Second, go to the proc folder and find the fd point to this file

  	$ ls -l /proc/4158/fd/4
  	lr-x------  1 rossi rossi 64 Oct 31 16:18 /proc/4158/fd/4 -> /home/rossi/myfile (deleted)

+ Third, copy the file to a new location

  	$cp /proc/4158/fd/4 <new location>

Sometimes we want to delete log files to free space. But the disk space will not freed if the process is still held the fd. We can operator on the proc pseudo file directly in the /proc/fd folder to free the space. In the above case, if we want clean the myfile's data on the disk. We can run the command like this:

  	$echo "" > /proc/4158/fd/4
