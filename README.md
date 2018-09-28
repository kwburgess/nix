# nix
record of nix config

## Initial setup:
https://nixos.org/nixos/download.html - downloaded graphical live cd iso and burned it to usb using etcher 1.4.4 on mac
Created an empty partition (500GB+) on laptop. 
Booted from usb iso on restart.

```bash
# lists partitions on the disk
fdisk -l

# once you've identified the partition you want to install nixos on, run this (example: /dev/sda, or /dev/nvme0n1p4
disk=/dev/nvme0n1p4
wipefs -a $disk
# magic - may need to create a partition table with correctly labeled partition types before formatting.
mkfs.ext4 -L nixos $disk

# mounts the partition you just created
mount /dev/disk/by-label/nixos /mnt
# mounts your boot disk (boot manager basically)
mount /dev/nvme0n1p1 /mnt/boot

nixos-generate-config --root /mnt

# I installed on a dual booted UEFI system, so I needed to do this https://nixos.org/nixos/manual/index.html#sec-installation
# add boot.loader.grub.useOSProber = true; 
vim /mnt/etc/nixos/configuration.nix

nixos-install
```
