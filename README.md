# cursedfs

Make a disk image formatted with both ext2 and FAT, at once.

```bash
~/cursedfs% wget 'https://github.com/meithecatte/cursedfs/releases/download/v1.0/cursed.img'
~/cursedfs% sudo mount -o loop -t ext2 cursed.img mountpoint/
~/cursedfs% ls mountpoint/
mkfs.cursed
~/cursedfs% sudo umount mountpoint/
~/cursedfs% sudo mount -o loop -t msdos cursed.img mountpoint/
~/cursedfs% ls mountpoint/
gudnuse.ogg
```

# Why?

[I got nerd-sniped](https://twitter.com/Foone/status/1217162186130198529?s=20)

# How?

It turns out this is surprisingly simple to do: just create a FAT volume with a
lot of reserved sectors and put the ext2 into the reserved sectors. This works
because the filesystems choose different places to put their superblock: FAT
uses the very first sector, while ext2 leaves the first kilobyte unused.

# Can I write to the filesystems?

Yes! When I first decided to do this, I thought writing to the image would
surely break everything, but as it turns out, the method I've found means
the filesystems don't conflict.
