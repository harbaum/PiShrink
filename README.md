# PiShrink #
PiShrink is a bash script that automatically shrink a pi image that will then resize to the max size of the SD card on boot. This will make putting the image back onto the SD card faster and the shrunk images will compress better.

## Usage ##
`sudo pishrink.sh [-s|-c] imagefile.img [newimagefile.img]`

If the `-s` option is given the script will skip the autoexpanding part of the process.  If you specify the `newimagefile.img` parameter, the script will make a copy of `imagefile.img` and work off that. You will need enough space to make a full copy of the image to use that option.

The `-c` option will clean the image up a little bit before shrinking it. Currently this will

  - Remove the ssh host keys and install a script to re-generate them on first boot
  - Remove cached debian packages from /var/cache/apt
  - Remove old log files

The `-c` option is intended to be used when preparing an image for use on a different Pi or for distribution.

## Prerequisites ##
If you are trying to shrink a [NOOBS](https://github.com/raspberrypi/noobs) image it will likely fail. This is due to [NOOBS paritioning](https://github.com/raspberrypi/noobs/wiki/NOOBS-partitioning-explained) being significantly different than Raspian's. Hopefully PiShrink will be able to support NOOBS in the near future.

If using Ubuntu, you will likely see an error about `e2fsck` being out of date and `metadata_csum`. The simplest fix for this is to use Ubuntu 16.10 and up, as it will save you a lot of hassle in the long run.

## Installation ##
```bash
wget https://raw.githubusercontent.com/Drewsif/PiShrink/master/pishrink.sh
chmod +x pishrink.sh
sudo mv pishrink.sh /usr/local/bin
```

## Example ##
```bash
[user@localhost PiShrink]$ sudo pishrink.sh pi.img
e2fsck 1.42.9 (28-Dec-2013)
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
/dev/loop1: 88262/1929536 files (0.2% non-contiguous), 842728/7717632 blocks
resize2fs 1.42.9 (28-Dec-2013)
resize2fs 1.42.9 (28-Dec-2013)
Resizing the filesystem on /dev/loop1 to 773603 (4k) blocks.
Begin pass 2 (max = 100387)
Relocating blocks             XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
Begin pass 3 (max = 236)
Scanning inode table          XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
Begin pass 4 (max = 7348)
Updating inode references     XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
The filesystem on /dev/loop1 is now 773603 blocks long.

Shrunk pi.img from 30G to 3.1G
```

## Contributing ##
If you find a bug please create an issue for it. If you would like a new feature added, you can create an issue for it but I can't promise that I will get to it.

Pull requests for new features and bug fixes are more than welcome!
