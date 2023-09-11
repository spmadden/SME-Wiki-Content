## Migrate from Ext3 to Ext4

With the advent of the new Extention 4 (ext4) filesystem becoming stable, it’s now benefitial and almost advisible to migrate from your Extention 3 (ext3) filesystem to Extention 4. While there are a number of other articles out there ranting and raving about the benefits of migrating to Extention 4, I will not go into that here. Suffice to say that I was sold and will detail the basic process of migrating your filesystem to Extention 4.

Truly ext4 is backwards compatible with ext3 with the addition of Extents, Background defragging and Directory Indexing, hence these are the options on the filesystem that we will be adding. Note: If you followed my previous tutorial on encrypting partitions, replace /dev/filesystem with your /dev/mapper/encryptedPartition

      tune2fs -O extents,uninit_bg,dir_index /dev/filesystem

Following this command, the filesystem will be left in an inconsistant state. Ext4 also adds basic checksumming of data for better reliability. Because the filesystem has been using the ext3 options, these were never created. As such, you will have to run a fsck on the partition to return it to a consistent state.

      e2fsck -pf /dev/filesystem

That’s really it. It’s a simple process and you will be able to mount your partitions under the new Extention 4 filesystem with all of your files intact.

Just remember to edit /etc/fstab and change your ‘ext3′ to ‘ext4′ for the filesystem you just migrated, otherwise you won’t take advantage of the ext4 features.
