HP@PRANAB MINGW64 ~/Downloads
$  ssh -i "tws-volume-key.pem" ubuntu@ec2-54-79-37-55.ap-southeast-2.compute.amazonaws.com
Welcome to Ubuntu 24.04.1 LTS (GNU/Linux 6.8.0-1016-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Mon Oct 28 18:52:58 UTC 2024

  System load:  0.08              Processes:             104
  Usage of /:   23.2% of 6.71GB   Users logged in:       0
  Memory usage: 19%               IPv4 address for enX0: 172.31.2.20
  Swap usage:   0%


Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


The list of available updates is more than a week old.
To check for new updates run: sudo apt update

Last login: Mon Oct 28 18:09:27 2024 from 152.59.24.142
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

ubuntu@ip-172-31-2-20:~$ lsblk
NAME     MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
loop0      7:0    0 25.2M  1 loop /snap/amazon-ssm-agent/7993
loop1      7:1    0 55.7M  1 loop /snap/core18/2829
loop2      7:2    0 38.8M  1 loop /snap/snapd/21759
xvda     202:0    0    8G  0 disk
├─xvda1  202:1    0    7G  0 part /
├─xvda14 202:14   0    4M  0 part
├─xvda15 202:15   0  106M  0 part /boot/efi
└─xvda16 259:0    0  913M  0 part /boot
xvdf     202:80   0   10G  0 disk
ubuntu@ip-172-31-2-20:~$ lsblk
NAME     MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
loop0      7:0    0 25.2M  1 loop /snap/amazon-ssm-agent/7993
loop1      7:1    0 55.7M  1 loop /snap/core18/2829
loop2      7:2    0 38.8M  1 loop /snap/snapd/21759
xvda     202:0    0    8G  0 disk
├─xvda1  202:1    0    7G  0 part /
├─xvda14 202:14   0    4M  0 part
├─xvda15 202:15   0  106M  0 part /boot/efi
└─xvda16 259:0    0  913M  0 part /boot
xvdf     202:80   0   10G  0 disk
xvdg     202:96   0   12G  0 disk
xvdh     202:112  0   14G  0 disk
ubuntu@ip-172-31-2-20:~$ lvm
  WARNING: Running as a non-root user. Functionality may be unavailable.
lvm> exit
  Exiting.
ubuntu@ip-172-31-2-20:~$ sudo su
root@ip-172-31-2-20:/home/ubuntu# lvm
lvm> pvs
lvm> exit
  Exiting.
root@ip-172-31-2-20:/home/ubuntu# lvm
lvm> pvcreate /dev/xvdf /dev/xvdg /dev/xvdh
  Physical volume "/dev/xvdf" successfully created.
  Physical volume "/dev/xvdg" successfully created.
  Physical volume "/dev/xvdh" successfully created.
lvm> pvs
  PV         VG Fmt  Attr PSize  PFree
  /dev/xvdf     lvm2 ---  10.00g 10.00g
  /dev/xvdg     lvm2 ---  12.00g 12.00g
  /dev/xvdh     lvm2 ---  14.00g 14.00g
lvm> vgcreate tws_vg /dev/xvdf /dev/xvdg
  Volume group "tws_vg" successfully created
lvm> vgs
  VG     #PV #LV #SN Attr   VSize  VFree
  tws_vg   2   0   0 wz--n- 21.99g 21.99g
lvm> lvcreate -L 10G -n tws_lv tws_vg
  Logical volume "tws_lv" created.
lvm> pvdisplay
  --- Physical volume ---
  PV Name               /dev/xvdf
  VG Name               tws_vg
  PV Size               10.00 GiB / not usable 4.00 MiB
  Allocatable           yes
  PE Size               4.00 MiB
  Total PE              2559
  Free PE               2559
  Allocated PE          0
  PV UUID               vQ7O0r-nDsQ-XJ36-SM3L-PDo2-Axw7-rYMo0S

  --- Physical volume ---
  PV Name               /dev/xvdg
  VG Name               tws_vg
  PV Size               12.00 GiB / not usable 4.00 MiB
  Allocatable           yes
  PE Size               4.00 MiB
  Total PE              3071
  Free PE               511
  Allocated PE          2560
  PV UUID               jnZBGJ-OWIy-5ybl-Zf4r-99zf-38RX-irOM8d

  "/dev/xvdh" is a new physical volume of "14.00 GiB"
  --- NEW Physical volume ---
  PV Name               /dev/xvdh
  VG Name
  PV Size               14.00 GiB
  Allocatable           NO
  PE Size               0
  Total PE              0
  Free PE               0
  Allocated PE          0
  PV UUID               9VFTHn-zdjA-kBWp-eRoE-wue2-nVpC-jniwG5

lvm> vgdisplay
  --- Volume group ---
  VG Name               tws_vg
  System ID
  Format                lvm2
  Metadata Areas        2
  Metadata Sequence No  2
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                1
  Open LV               0
  Max PV                0
  Cur PV                2
  Act PV                2
  VG Size               21.99 GiB
  PE Size               4.00 MiB
  Total PE              5630
  Alloc PE / Size       2560 / 10.00 GiB
  Free  PE / Size       3070 / 11.99 GiB
  VG UUID               ilPkGG-fkou-SBMl-fZKN-1hbQ-Ozwt-1f9Vga

lvm> exit
  Exiting.
root@ip-172-31-2-20:/home/ubuntu# lsblk
NAME            MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
loop0             7:0    0 25.2M  1 loop /snap/amazon-ssm-agent/7993
loop1             7:1    0 55.7M  1 loop /snap/core18/2829
loop2             7:2    0 38.8M  1 loop /snap/snapd/21759
xvda            202:0    0    8G  0 disk
├─xvda1         202:1    0    7G  0 part /
├─xvda14        202:14   0    4M  0 part
├─xvda15        202:15   0  106M  0 part /boot/efi
└─xvda16        259:0    0  913M  0 part /boot
xvdf            202:80   0   10G  0 disk
xvdg            202:96   0   12G  0 disk
└─tws_vg-tws_lv 252:0    0   10G  0 lvm
xvdh            202:112  0   14G  0 disk
root@ip-172-31-2-20:/home/ubuntu# lvs
  LV     VG     Attr       LSize  Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  tws_lv tws_vg -wi-a----- 10.00g
root@ip-172-31-2-20:/home/ubuntu# mkdir /mnt/tws_lv_mount
root@ip-172-31-2-20:/home/ubuntu# mkfs.ext4 /dev/tws_vg/tws_lv
mke2fs 1.47.0 (5-Feb-2023)
Creating filesystem with 2621440 4k blocks and 655360 inodes
Filesystem UUID: 2e842dff-bd0f-436b-8e47-f1fe9660aed6
Superblock backups stored on blocks:
        32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632

Allocating group tables: done
Writing inode tables: done
Creating journal (16384 blocks): done
Writing superblocks and filesystem accounting information: done

root@ip-172-31-2-20:/home/ubuntu# mount  /dev/tws_vg/tws_lv /mnt/tws_lv_mount
root@ip-172-31-2-20:/home/ubuntu# df -h
Filesystem                 Size  Used Avail Use% Mounted on
/dev/root                  6.8G  1.6G  5.2G  24% /
tmpfs                      479M     0  479M   0% /dev/shm
tmpfs                      192M  884K  191M   1% /run
tmpfs                      5.0M     0  5.0M   0% /run/lock
/dev/xvda16                881M   76M  744M  10% /boot
/dev/xvda15                105M  6.1M   99M   6% /boot/efi
tmpfs                       96M   12K   96M   1% /run/user/1000
/dev/mapper/tws_vg-tws_lv  9.8G   24K  9.3G   1% /mnt/tws_lv_mount
root@ip-172-31-2-20:/home/ubuntu# cd /mnt/tws_lv_mount/
root@ip-172-31-2-20:/mnt/tws_lv_mount# ls
lost+found
root@ip-172-31-2-20:/mnt/tws_lv_mount# mkdir devops
root@ip-172-31-2-20:/mnt/tws_lv_mount# cd devops/
root@ip-172-31-2-20:/mnt/tws_lv_mount/devops# vim Hello-doston.txt
root@ip-172-31-2-20:/mnt/tws_lv_mount/devops# cd
root@ip-172-31-2-20:~# cd /home/ubuntu/
root@ip-172-31-2-20:/home/ubuntu# cat /mnt/tws_lv_mount/devops/Hello-doston.txt
This is my first file after the mounted
root@ip-172-31-2-20:/home/ubuntu# unmount /mnt/tws_lv_mount
Command 'unmount' not found, did you mean:
  command 'umount' from deb mount (2.39.3-9ubuntu6.1)
Try: apt install <deb name>
root@ip-172-31-2-20:/home/ubuntu# umount /mnt/tws_lv_mount
root@ip-172-31-2-20:/home/ubuntu# cat /mnt/tws_lv_mount/devops/Hello-doston.txt
cat: /mnt/tws_lv_mount/devops/Hello-doston.txt: No such file or directory
root@ip-172-31-2-20:/home/ubuntu#  mount  /dev/tws_vg/tws_lv /mnt/tws_lv_mount
root@ip-172-31-2-20:/home/ubuntu# cat /mnt/tws_lv_mount/devops/Hello-doston.txt
This is my first file after the mounted
root@ip-172-31-2-20:/home/ubuntu# lsblk
NAME            MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
loop0             7:0    0 25.2M  1 loop /snap/amazon-ssm-agent/7993
loop1             7:1    0 55.7M  1 loop /snap/core18/2829
loop2             7:2    0 38.8M  1 loop /snap/snapd/21759
xvda            202:0    0    8G  0 disk
├─xvda1         202:1    0    7G  0 part /
├─xvda14        202:14   0    4M  0 part
├─xvda15        202:15   0  106M  0 part /boot/efi
└─xvda16        259:0    0  913M  0 part /boot
xvdf            202:80   0   10G  0 disk
xvdg            202:96   0   12G  0 disk
└─tws_vg-tws_lv 252:0    0   10G  0 lvm  /mnt/tws_lv_mount
xvdh            202:112  0   14G  0 disk
root@ip-172-31-2-20:/home/ubuntu# mkdir /mnt/tws_disk_mount
root@ip-172-31-2-20:/home/ubuntu# cd /mnt/
root@ip-172-31-2-20:/mnt# ls
tws_disk_mount  tws_lv_mount
root@ip-172-31-2-20:/mnt# mkfs -t ext4 /dev/xvdh
mke2fs 1.47.0 (5-Feb-2023)
/dev/xvdh contains a LVM2_member file system
Proceed anyway? (y,N) y
Creating filesystem with 3670016 4k blocks and 917504 inodes
Filesystem UUID: ea27a5c0-633f-4bec-aeee-2ef3f3b4221b
Superblock backups stored on blocks:
        32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208

Allocating group tables: done
Writing inode tables: done
Creating journal (16384 blocks): done
Writing superblocks and filesystem accounting information: done

root@ip-172-31-2-20:/mnt# cd
root@ip-172-31-2-20:~# cd /home/ubuntu/
root@ip-172-31-2-20:/home/ubuntu# ls
root@ip-172-31-2-20:/home/ubuntu# ls
root@ip-172-31-2-20:/home/ubuntu# mount /dev/xvdh /mnt/tws_disk_mount/
root@ip-172-31-2-20:/home/ubuntu# df -h
Filesystem                 Size  Used Avail Use% Mounted on
/dev/root                  6.8G  1.6G  5.2G  24% /
tmpfs                      479M     0  479M   0% /dev/shm
tmpfs                      192M  884K  191M   1% /run
tmpfs                      5.0M     0  5.0M   0% /run/lock
/dev/xvda16                881M   76M  744M  10% /boot
/dev/xvda15                105M  6.1M   99M   6% /boot/efi
tmpfs                       96M   12K   96M   1% /run/user/1000
/dev/mapper/tws_vg-tws_lv  9.8G   32K  9.3G   1% /mnt/tws_lv_mount
/dev/xvdh                   14G   24K   13G   1% /mnt/tws_disk_mount
root@ip-172-31-2-20:/home/ubuntu# lvm
lvm> lvextend -L +5G -n tws_lv tws_vg
  Please specify a logical volume path.
lvm> lvextend -L +5G -n tws_lv tws_vg
  Please specify a logical volume path.
lvm>  lvextend -L +5G -n /dev/tws_vg/tws_lv
  Size of logical volume tws_vg/tws_lv changed from 10.00 GiB (2560 extents) to 15.00 GiB (3840 extents).
  Logical volume tws_vg/tws_lv successfully resized.
lvm> exit
  Exiting.
root@ip-172-31-2-20:/home/ubuntu# df -h
Filesystem                 Size  Used Avail Use% Mounted on
/dev/root                  6.8G  1.6G  5.2G  24% /
tmpfs                      479M     0  479M   0% /dev/shm
tmpfs                      192M  888K  191M   1% /run
tmpfs                      5.0M     0  5.0M   0% /run/lock
/dev/xvda16                881M   76M  744M  10% /boot
/dev/xvda15                105M  6.1M   99M   6% /boot/efi
tmpfs                       96M   12K   96M   1% /run/user/1000
/dev/mapper/tws_vg-tws_lv  9.8G   32K  9.3G   1% /mnt/tws_lv_mount
/dev/xvdh                   14G   24K   13G   1% /mnt/tws_disk_mount
root@ip-172-31-2-20:/home/ubuntu# lsblk
NAME            MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
loop0             7:0    0 25.2M  1 loop /snap/amazon-ssm-agent/7993
loop1             7:1    0 55.7M  1 loop /snap/core18/2829
loop2             7:2    0 38.8M  1 loop /snap/snapd/21759
xvda            202:0    0    8G  0 disk
├─xvda1         202:1    0    7G  0 part /
├─xvda14        202:14   0    4M  0 part
├─xvda15        202:15   0  106M  0 part /boot/efi
└─xvda16        259:0    0  913M  0 part /boot
xvdf            202:80   0   10G  0 disk
└─tws_vg-tws_lv 252:0    0   15G  0 lvm  /mnt/tws_lv_mount
xvdg            202:96   0   12G  0 disk
└─tws_vg-tws_lv 252:0    0   15G  0 lvm  /mnt/tws_lv_mount
xvdh            202:112  0   14G  0 disk /mnt/tws_disk_mount
root@ip-172-31-2-20:/home/ubuntu# cd
root@ip-172-31-2-20:~# su
root@ip-172-31-2-20:~# sudo su
root@ip-172-31-2-20:~# exit
exit
root@ip-172-31-2-20:~# exit
exit
root@ip-172-31-2-20:~# sudo su - pranab
su: user pranab does not exist or the user entry does not contain all the required fields
root@ip-172-31-2-20:~# sudo su - Pranab
su: user Pranab does not exist or the user entry does not contain all the required fields
root@ip-172-31-2-20:~# sudo su -Pranab
su: invalid option -- 'r'
Try 'su --help' for more information.
root@ip-172-31-2-20:~# sudo su -HP
su: invalid option -- 'H'
Try 'su --help' for more information.
root@ip-172-31-2-20:~# sudo su - HP
su: user HP does not exist or the user entry does not contain all the required fields
root@ip-172-31-2-20:~# sudo su - PRANAB
su: user PRANAB does not exist or the user entry does not contain all the required fields
root@ip-172-31-2-20:~# pwd
/root
root@ip-172-31-2-20:~# cd/home/Pranab
bash: cd/home/Pranab: No such file or directory
root@ip-172-31-2-20:~# cd /home/Pranab
bash: cd: /home/Pranab: No such file or directory
root@ip-172-31-2-20:~#
exit
ubuntu@ip-172-31-2-20:~$
logout
Connection to ec2-54-79-37-55.ap-southeast-2.compute.amazonaws.com closed.

