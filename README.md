emb-linux-img-tools
======

Embedded Linux Image Tools

* imgupd - firmware update script 
* imgmount - mount a disk image 
* imgpatch - install application to platform image


Examples
-------

### Installing an Application to a Platform Image

Say you have a platform image "sd.img" with two partitions. Partition 1 is your /boot and partition 2 is /.
Now say you have an application tarball "app.tar.gz" which you want to extract to the root partition of your sd image. This is very easy:

    sudo ./imgpatch app.tar.gz sd.img 2
    
The app is installed to the image in-place, and everything is cleanly unmounted automatically.

### Creating Whole Disk Image (with partition table)

Create empty disk image:

    dd if=/dev/zero of=disk bs=1M count=100

Setup some partitions:

    sudo fdisk disk
    
Mount the image (no filesystem yet):

    sudo ./imgmount disk
    
Create a filesystem (use device name from previous command):
    
    sudo mkfs.ext4 /dev/mapper/loop0p1
    
Remount now that filesystem is created:

    sudo ./imgmount -r disk
    
Enjoy!

    cd /mnt/loop0p1
    
Unmount when done:

    sudo ./imgmount -u disk
    

### Creating Raw Partition Image (no partition table)

Create empty disk image:

    dd if=/dev/zero of=part bs=1M count=100
    
Mount the image (no filesystem yet):

    sudo ./imgmount part
    
Create a filesystem (use device name from previous command):
    
    sudo mkfs.ext4 /dev/loop0
    
Remount now that filesystem is created:

    sudo ./imgmount -r part
    
Enjoy!

    cd /mnt/loop0
    
Unmount when done:

    sudo ./imgmount -u part
    


Links and Ideas
-----

For testing with loop block devices: 
http://bochs.sourceforge.net/doc/docbook/user/loop-device-usage.html

Will want to support squashfs:
http://squashfs.sourceforge.net/

We will want to read the uboot version:
http://stackoverflow.com/questions/5781738/getting-u-boots-version-from-userspace

Use bsdiff or Google's courgette to make compressed updates. (Not whole image, just certain binaries?)

Hash tree alongside filesystem to track changes.

TODO: Add example script.
