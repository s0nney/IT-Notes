Fixing issues with proper disk size allocation in Proxmox.


# Ubuntu VM:
1. df -h
 
2. sudo lvdisplay
 
3. sudo run lvextend -l +100%FREE /dev/mapper/ubuntu--vg-ubuntu--lv

4. sudo resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv


