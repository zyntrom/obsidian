## Preparation:

* [Arch Linux Download Link](https://archlinux.org/download/)
* [Youtube Guide](https://www.youtube.com/watch?v=68z11VAYMS8&t=1197s)
* [Arch Linux Guide](https://wiki.archlinux.org/title/Installation_guide)
* [iwctl WiFi Guide](https://wiki.archlinux.org/title/Iwd#iwctl)
* Install the ISO and flash it to the USB .

## 1. Installation (UEFI Method)

* Plug in the USB and boot into it . (From the UEFI boot menu)
* Select Arch Linux installation from the menu of selections.

## 2. Keyboard Layout

* If you want to change keyboard layout. (By default it is us)

```bash
#keyboard layout for it
loadkeys it

#keyboard layout for us
loadkeys us
```

## 3. WiFi connection  

* By default if you have Ethernet then it will automatically connect.
* If you have WiFi then use iwctl to connect

The Commands are:

```bash
iwctl
```

```bash
device list
```

```bash
station _name_ scan
```

```bash
station _name_ get-networks
```

```bash
station name connect SSID
```

* To test Internet connection use: (Use ctrl - c to stop any command from running)

```
ping google.com
```

## 4. Update the system clock

```bash
timedatectl
```
## 5. Disk Partitioning 

* In order to install Linux you need to need to divide your disk into three parts.
* They are root (/), swap, and boot. ( Optional if you already do not  have one )
* For this we can use fdisk or cfdisk. 
* In this case we will use cfdisk as it is easy to use.

```bash
lsblk
cfdisk /dev/<partition>
```

* If it ask for label type select gpt
* Delete partitions that are no longer in use and make space if it does not show free space. ( If dual booting do not delete Partitions you do not recognize if could be windows or other Linux OS )
* Then select free space  with arrows and select and enter new.

* First we need to make a boot partition when it ask for size give 100M as size
* Second we need to make a swap (Temp ram for the OS) it can be of size  2,4,8,16 or such ( Its better to give size in powers of 2 ). If you have 16 gb ram then give swap of 8G
* The last partition can  be as much as you want because it is the root (/) partition 
  eg: 100G
* Then Finally select write.
  
## 6. Formatting created Partition

* To see all the created and existing partition

```bash
lsblk
```

* First we need  to Format the root partition 

```bash
mkfs.ext4 /dev/_root_partition_
```

* Second we need to Format swap partition 

```bash
mkswap /dev/_swap_partition_
```

* At Last we need to Format boot partition (Do not do this if you already have a boot partition by other Linux OS as it will remove the entry for the other OS)

```bash
mkfs.fat -F 32 /dev/efi_system_partition
```

## 7. Mount the file systems

* Mount point for root (/) partition 

```bash
mount /dev/root_partition /mnt
```

* Mount point for boot partition

```bash
#it makes file called efi in boot in /mnt 
mount --mkdir /dev/efi_system_partition /mnt/boot/efi
```

* At last Activate the created swap partition 

```bash
swapon /dev/swap_partition
```

## 8. Installation of Main System files

* We  now need to install most of the programs need for the base OS to run 

```bash
pacstrap -K /mnt base linux linux-firmware sof-firmware base-devel grub efibootmgr nano networkmanager 
```

## 9. Generating File System and config

* Now we need to create File System for the users and basic configuration for the OS to work 

* To get info on the file system mounted  

```bash
genfstab /mnt
```

* Saving the info into a file

```bash
genfstab /mnt > /mnt/etc/fstab
```

* To confirm the file write

```bash
cat /mnt/etc/fstab
```

## 10. Chroot into the System 

```bash
arch-chroot /mnt
```

## 11.  Date, Time and Location Config

* Setting up date and location 

```bash
ln -sf /usr/share/zoneinfo/Asia/India /etc/localtime
```

* To confirm date

```bash
date
```

* To sync system clock

```bash
hwclock --systohc
```

## 12. Localization

* Edit Local by removing comment on `en_US.UTF-8 UTF-8` from the file 

```Bash
nano /etc/locale.gen
#or ( Direct Command ) 
echo "en_US.UTF-8 UTF-8" > /etc/locale.gen
```

* Now generate the locale

```bash
locale-gen
```

* Specify locale in locale.conf

```bash
nano /etc/locale.conf
#Then add `LANG=en_US.UTF-8`

#Or ( Direct Command )
echo "LANG=en_US.UTF-8" > /etc/locale.conf
```

* ( Optional ) if you want to change keyboard layout

```bash
echo "KEYMAP=us" > /etc/vconsole.conf
```

* Next Add the hostname 

```bash
#Use nano to edit manually 
nano /etc/hostname #give a host name (eg archii)

#direct command
echo "archii" > /etc/hostname
```

## Setting Root password and User

* To config root password 

```bash
passwd
#Then type the password
```

* To add a user 

```bash
useradd -m -G wheel -s /bin/bash username
```

```bash
passwd username
```

*  Now add the user to sudo list 

```bash
#exit the user if you entered the user with exit command  
exit
#As Root User
EDITOR=nano visudo
#Then uncomment %wheel ALL=(ALL) ALL
```

* To enter a user profile

```bash
su username
```

* Once you entered the user update the system

```bash
#y is checking update and u is install the updates
sudo pacman -Syu
```

## Setting up Network Manager

* For you to use internet when you load the OS

```bash
sudo systemctl enable NetworkManager
```

## Setting up Grub for dual booting

* Check  for existing boot partitions 

```bash
lsblk -f
```

* Mount the boot partition

```bash
mount /dev/nvme0n1p1 /mnt/boot/efi
```
* Chroot into arch
* Install dual booting package

```bash
sudo pacman -S grub efibootmgr os-prober
```

* Edit or check /etc/default/grub and ensure this line is uncommented

```bash
sudo nano /etc/default/grub
```

edit

```bash
GRUB_DISABLE_OS_PROBER=false
```

* Now run 


```bash
sudo os-prober
```

* GRUB to EFI

```bash
sudo grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=Arch
```

* Generate GRUB Configuration

```bash
sudo grub-mkconfig -o /boot/efi/grub/grub.cfg
```


* Umount all the mounted partitions 

```bash
umount -a
```

* Finally reboot

```bash
reboot
```

## Booting the OS

* Start the computer 
* Select the Arch Linux
* Login to your user
* Connect to the internet (Ethernet or WiFi with iwctl )

Command to set the font size:

```bash
setfont -d
```

## Setting up GUI

* Important packages for GUI

```bash
sudo pacman -S plasma sddm konsole nvim kate firefox  
```

## Final Setup and startup

* As the final setup we need to start sddm our window manager 

```bash
sudo systemctl enable --now sddm
```

Now Enjoy Arch Linux 