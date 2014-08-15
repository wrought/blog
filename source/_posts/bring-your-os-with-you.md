title: Bring Your OS With You
date: 2014-08-15 13:40:24
tags:
- operating system
- os
- linux
- crunchbang
- philosophy
- style
- tools
---

I support and celebrate operating systems based on Linux, well, because there are not many better options. ;) On the other hand, I also believe that community-supported tools and systems are worth our participation and involvement, because for what we all put in, we each, and collectively, get much more out. Simple as that.

Right now I run [CrunchBang](http://crunchbang.com/), a snappy, simplified, developer-conscious flavor of [Debian](https://en.wikipedia.org/wiki/Debian), notably running the OpenBox window manager rather than something heftier like GNOME.

Since installing CrunchBang, I have come to appreciate its simplicity so much that I have wanted to continue using it, with all of my alterations, even as I upgrade my laptop. In this post, I outline a strategy to simplify management of your Linux system based on my experience so far with my operating system.

> Bring your OS with you

1. Pick an operating system. (For me at the moment, it's CrunchBang)
    1. Download an `.iso` (image) file
    1. Use `unetbootin` or `dd` ([details](http://linuxcommand.org/man_pages/dd1.html)) to copy the image to a usb drive
        1. For using `dd`, find out the device names of your disks with `dmesg | grep sd`, which allows you to see details about drives and when they are connected.
        1. Pick the right locations and fire __[WARNING, MAY DESTROY STUFF]__:
            `dd if=/home/username/downloads/linux-foo-bar-0.1.iso of=/dev/sdBBB`
        1. Once finished, you can reboot, select the flash drive as the boot disk (usually change some settings in BIOS and then use some key like F12 to select boot device from a list)
        1. Follow your OS's installation instructions.
1. Exact backup to empty drive with `dd`
    1. Boot from a live OS (live disk, like CD or usb drive with linux on it)
    1. Again, find the correct device names of disks first
    1. This time copy from your computer's disk instead of an image to some backup file __[WARNING, MAY DESTROY STUFF]__:
        `dd if=/dev/sdAAA of=/dev/sdBBB`
    1. To recover a _borked_ system, you can always copy in the other direction to restore __[WARNING, MAY DESTROY STUFF]__:
        `dd if=/dev/sdBBB of=/dev/sdAAA`
1. Backup with `horcrux` on top of `duplicity` ([details](http://chrispoole.com/project/horcrux/))
    1. This is for more magic, like multiple restoration points, partial backups, and most importantly, backing up to multiple locations in case of multiple failures
    1. `horcrux` is pretty much a `bash` script for `duplicity`, so read it and `man duplicity`!
1. Store _special_ files with `tomb` ([details](https://www.dyne.org/software/tomb/))
    1. A fun and tiny way to bury bits on your disk, excellent alternative to full-disk encryption schemes
1. Migrate to new devices with `dd` and `lvm`
    1. When it's time to upgrade or replace your computer, you can carry everything with you. There is only one important question:
        1. Is the destination hard drive bigger or smaller than my current one?
            1. Either way you will have to resize the _physical volume_ and _logical volumes_ in question, but if the destination drive is bigger, than you can copy now and resize later ;)
                1. Resizing un-encrypted partitions can be as easy as running `gparted`, `parted`, `fdisk`, or simply with `lvm` commands
            1. However, encrypted partitions are not as easy to manage. See notes below for resizing encrypted partitions:

> *Pro-tip:* Check the progress of `dd` with ``sudo kill -USR1 `pidof dd` ``

### Enlarging LUKS Encryption over LVM

These days, it's easy to implement full-disk encryption at the time of your operating system's installation. Further, it's usually recommended to use LVM to manage your disks, even on a personal computer. `lvm` creates a layer of abstraction on top of typical partitions, which can make some forms of disk management much easier or less risky. If you installed a recent distribution of linux based on Debian, and installed fill-disk encryption it is likely you are using LUKS over LVM. 

For debian-based systems, this guide called [Resize Encrypted Partitions](https://help.ubuntu.com/community/ResizeEncryptedPartitions) should be close to what you need, with some noteworthy updates:

1. **Step 1.** When creating a new partition "next to and to the left of (after) your crypt", don't let this language confuse you. You want the encrypted partition to have a new partition immediately following it so that you may use `fdisk` to overwrite this new partition by expanding the encrypted partition over the new partition. This should help make more sense of the situation. It's likely that you have `/dev/sda1` with `/boot` on it and `/dev/sda2` as an extended partition that contains your encrypted partition (something like `/dev/sda5` maybe, depending on how many partitions you made at installation and later with LVM). This is why it is likely that creating another Linux partition inside of the `/dev/sda2` extended partition would likely use the name `/dev/sda6` as the instructions note. If you view this in `gparted` you would see `/dev/sda2` wrapped around the encrypted `/dev/sda5` as well as around the following new partition `/dev/sda6`, ending the wrapper.
1. **Step 2.** Don't bother with `/dev/urandom` it takes forever, just use `/dev/zero` or if you prefer, you can use `shred` instead of `dd` with the `--iterations` flag as such: `sudo shred --iterations=1 /dev/sda6`
1. **Step 3.** This is a very confusing reference. You are instructed to use `fdisk` in the same process as it is used for shrinking partitions in the instructions preceeding these (above). However, there are superfluous warnings, commands, and instructions that make it difficult to implement here. The important concept to note, in my opinion, is simply that you are using fdisk to expand your encrypted partition over the new, adjacent partition. This means you should use `fdisk /dev/sda` to `d` delete partitions `6`, `5` and `2`, then `n` re-create them as partitions `2` (`e` expanded) and `5` (`l` logical) such that (by default) `/dev/sda5` expands over the blocks previously partitioned for `/dev/sda6`. Check with `p` and when you are satisfied, `w` write to the disk.
1. After **Step 8.** If you are troubleshooting the process, to deactivate your LVM, use `sudo vgchange -an`
1. **Step 11.** Repeat as necessary for each _logical volume_ you wish to resize (e.g. `root`, `swap`, and `home`)
1. **Step 12.** You won't be able to resize the filesystem for swap. If you do resize a swap volume, when you reboot and complete the resizing successfully, simply use `mkswap` appropriately such as:
    `sudo swapoff`
    `sudo mkswap /dev/crypt1/swap_1`
    `sudo swapon`

## The Future

Maybe in the future I will switch to ArchLinux to [avoid major upgrade headaches](https://en.wikipedia.org/wiki/Rolling_release/), get on board with the new future-of-linux features, and benefit from a great community with lots of documentation..

In fact, I'm downloading Arch right now... ;)
