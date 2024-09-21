$ ssh -i "AKKEY1.pem" ec2-user@54.237.135.181
   ,     #_
   ~\_  ####_        Amazon Linux 2023
  ~~  \_#####\
  ~~     \###|
  ~~       \#/ ___   https://aws.amazon.com/linux/amazon-linux-2023
   ~~       V~' '->
    ~~~         /
      ~~._.   _/
         _/ _/
       _/m/'
Last login: Sat Sep 21 05:11:52 2024 from 219.91.171.53
[ec2-user@ip-172-31-46-217 ~]$ df -h
Filesystem      Size  Used Avail Use% Mounted on
devtmpfs        4.0M     0  4.0M   0% /dev
tmpfs           475M     0  475M   0% /dev/shm
tmpfs           190M  456K  190M   1% /run
/dev/xvda1      8.0G  1.6G  6.4G  20% /
tmpfs           475M     0  475M   0% /tmp
/dev/xvda128     10M  1.3M  8.7M  13% /boot/efi
tmpfs            95M     0   95M   0% /run/user/1000
[ec2-user@ip-172-31-46-217 ~]$ lsblk
NAME      MAJ:MIN RM SIZE RO TYPE MOUNTPOINTS
xvda      202:0    0  12G  0 disk
├─xvda1   202:1    0   8G  0 part /
├─xvda127 259:0    0   1M  0 part
└─xvda128 259:1    0  10M  0 part /boot/efi
[ec2-user@ip-172-31-46-217 ~]$ df -ht
df: option requires an argument -- 't'
Try 'df --help' for more information.
[ec2-user@ip-172-31-46-217 ~]$ sudo lsblk
NAME      MAJ:MIN RM SIZE RO TYPE MOUNTPOINTS
xvda      202:0    0  12G  0 disk
├─xvda1   202:1    0   8G  0 part /
├─xvda127 259:0    0   1M  0 part
└─xvda128 259:1    0  10M  0 part /boot/efi
[ec2-user@ip-172-31-46-217 ~]$ sudo growpart /dev/xvda1
growpart disk partition
   rewrite partition table so that partition takes up all the space it can
   options:
    -h | --help       print Usage and exit
         --fudge F    if part could be resized, but change would be
                      less than 'F' bytes, do not resize (default: 1048576)
    -N | --dry-run    only report what would be done, show new 'sfdisk -d'
    -v | --verbose    increase verbosity / debug
    -u | --update  R  update the the kernel partition table info after growing
                      this requires kernel support and 'partx --update'
                      R is one of:
                       - 'auto'  : [default] update partition if possible
                       - 'force' : try despite sanity checks (fail on failure)
                       - 'off'   : do not attempt
                       - 'on'    : fail if sanity checks indicate no support

   Example:
    - growpart /dev/sda 1
      Resize partition 1 on /dev/sda
must supply partition-number
[ec2-user@ip-172-31-46-217 ~]$ sudo growpart /dev/xvda 1
CHANGED: partition=1 start=24576 old: size=16752607 end=16777183 new: size=25141215 end=25165791
[ec2-user@ip-172-31-46-217 ~]$ sudo resize2fs /dev/xvda 1
resize2fs 1.46.5 (30-Dec-2021)
resize2fs: Device or resource busy while trying to open /dev/xvda
Couldn't find valid filesystem superblock.
[ec2-user@ip-172-31-46-217 ~]$ sudo xfs_growfs /
meta-data=/dev/xvda1             isize=512    agcount=2, agsize=1047040 blks
         =                       sectsz=4096  attr=2, projid32bit=1
         =                       crc=1        finobt=1, sparse=1, rmapbt=0
         =                       reflink=1    bigtime=1 inobtcount=1
data     =                       bsize=4096   blocks=2094075, imaxpct=25
         =                       sunit=128    swidth=128 blks
naming   =version 2              bsize=16384  ascii-ci=0, ftype=1
log      =internal log           bsize=4096   blocks=16384, version=2
         =                       sectsz=4096  sunit=4 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
data blocks changed from 2094075 to 3142651
[ec2-user@ip-172-31-46-217 ~]$ df -h
Filesystem      Size  Used Avail Use% Mounted on
devtmpfs        4.0M     0  4.0M   0% /dev
tmpfs           475M     0  475M   0% /dev/shm
tmpfs           190M  452K  190M   1% /run
/dev/xvda1       12G  1.6G   11G  14% /
tmpfs           475M     0  475M   0% /tmp
/dev/xvda128     10M  1.3M  8.7M  13% /boot/efi
tmpfs            95M     0   95M   0% /run/user/1000
[ec2-user@ip-172-31-46-217 ~]$ lsblk
NAME      MAJ:MIN RM SIZE RO TYPE MOUNTPOINTS
xvda      202:0    0  12G  0 disk
├─xvda1   202:1    0  12G  0 part /
├─xvda127 259:0    0   1M  0 part
└─xvda128 259:1    0  10M  0 part /boot/efi
[ec2-user@ip-172-31-46-217 ~]$




