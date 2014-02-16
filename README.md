emb-linux-img-tools
======

Embedded Linux Image Tools

* imgupd - firmware update script 
* imgmount - mount a disk image 
* appinstall - install application to platform image

For testing with loop block devices: 
http://bochs.sourceforge.net/doc/docbook/user/loop-device-usage.html

Will want to support squashfs:
http://squashfs.sourceforge.net/

We will want to read the uboot version:
http://stackoverflow.com/questions/5781738/getting-u-boots-version-from-userspace

Testing
-------

Create empty disk:

    dd if=/dev/zero of=disk bs=1M count=100

Set up /dev/loop* to point to disk:

    sudo losetup -f --show disk
    
When you are done:
    
    sudo losetup -d /dev/loop0 # or whatever you got from losetup -f
    
To test imgupd:

    ./imgupd show
    ./imgupd install <item-name>
    
TODO: Add example script.
