### Sometimes proxmox isn't able to set the logical volumes of our virtualized disk sizes very well. 
### We can fix that.

1. `df -h`

Grab the allocated storage for our partition that we're interested in. 
For a typical ubuntu machine, you might be met with something like: `/dev/mapper/ubuntu--vg-ubuntu--lv`.

2. `sudo lvdisplay`

Grab information for the logical volume that we're interested in. This will tell us what the associated volume group too. 

3. `sudo lvextend -l +100%FREE /dev/mapper/ubuntu--vg-ubuntu--lv`

We will begin the allocation here. `-l +100%FREE` means to use ALL unallocated space in the volume group.

4. `sudo resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv`

Resize the filesystem to use the new allocated space.
