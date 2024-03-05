+++
title = "Installing Arch Linux with a GUI"
date = "2022-11-01"
draft = true
+++

[Skip to crux](#crux)

Arch Linux is a work of art, no doubts whatsoever. But one of the most annoying parts of it is that you have no GUI when installing it. Here, I share a useful trick to make our lives a little bit easier.

## Why need a GUI

There are linux aficionados who question "Why need a GUI? You can do everything in the command line" and etc. First of all, TTY is different than the command line and most of us don't know to do many stuff on the TTY. A GUI is more comfortable and that is the whole reason GUI is invented. Having a GUI (especially a browser) is handy many a times. Maybe

- You want to click on things to connect to WiFi rather fiddling with `iwctl`.
- You are setting up raid and you would like to read the arch wiki in your PC's browser, copy commands rather reading on the phone and typing it out.
- You have to copy the blkid of some block device to a config file. (How do you copy text from TTY anyways, I used to painstakingly write the blkid on a piece of paper, type it out before)
- You prefer to partition using gparted than parted or cgdisk.
- You want to watch your favourite dog videos or listen to music on YouTube, Spotify, etc. while it installs.

Or a thousand other reasons.

I have had conversations with some of the Arch Linux team members and they seem to have aversion towards any kind of GUI in the default ISO, which I don't understand to be honest.

## Existing Options

There are many great projects who try to give you a smooth experience, providing GUIs or guided installers. A few of them are

- [archinstall](https://github.com/archlinux/archinstall)
- [Arch Linux Calamares Installer](https://alci.online/)
- [Arch Linux GUI](https://archlinuxgui.in/) - Discontinued
- [archfi](https://github.com/MatMoul/archfi)

### Problems with the existing options

- If the project is not officially supported, we have to rely on third parties to keep their scripts and installers up to date which many times they don't.
- Using install scripts is generally frowned upon in the Arch Linux Community and in their chat groups, you are pushed away if you use any install scripts other than archinstall. So, no getting help.

- I am sure the people who wrote those installers are good engineers but, the quality of engineering can't be guaranteed in third party installers.

<a name="crux"></a>

## Solving our "Problem"

Installing Arch Linux from the command line is not a hard work to do. You partition, mount drives, run pacstrap, create fstab, set time zone and locale, setup bootloader, create user, enable necessary services and reboot.

Most people are comfortable following instructions from the arch wiki, typing it out on the command line. But, where do you read the arch wiki? On your phone? pfft. Having a GUI during install is more of a quality of life improvement (Atleast for me). I can install arch from the command line following the installation guide, but let me type everything in a fancy terminal like gnome-terminal or alacritty rather than the TTY.

## Solution

Based on our previous arguement, all we need for a comfortable installation is a GUI (Window manager or DE) to have multiple windows open, a terminal (gnome-terminal or alacritty), a web browser, gparted and the package `arch-install-scripts` which contains the commands `pacman`, `pacstrap`, `genfstab`, and `arch-chroot` which does the install for us.

In my experience, the easiest way to get all these is the **Fedora ISO**.

### Fedora ISO

Fedora is one of the few distributions which include `pacman` and `arch-install-scripts` in their official repositories.

Go to the [Fedora website](https://getfedora.org) and download whichever flavour you like (Gnome, KDE, Mate, etc). Create a bootable USB with tool of your choice (rufus, ventoy, or dd).

Before booting into the Fedora ISO, assuming you want to dual boot Windows with Arch Linux, go to [this Arch Wiki page](https://wiki.archlinux.org/title/System_time#UTC_in_Microsoft_Windows) and follow instructions there to make Windows use UTC for hardware time.

Boot the ISO and you have a working Desktop Environment and a Browser.

You don't have to mess with the command line to connect to the internet through WiFi or mobile tethering. Fedora ISO when booted will have `NetworkManager` running and use your DE's interface to connect to your network.

`gparted` is not present in the default ISO and all required executables and libraries like `pacman`, `libalpm` etc are dependencies of `arch-install-scripts`. So, install `gparted` and `arch-install-scripts` using

```
sudo dnf install gparted arch-install-scripts
```

We also have to initialize the pacman keyring to install packages using pacman. So, run

```
pacman-key --init
pacman-key --refresh-keys
```

Now we have everything we need to install Arch Linux. Go to the [Arch Linux installation Guide](https://wiki.archlinux.org/title/installation_guide), read the wiki thoroughly and set up your Arch Linux the very way you want.

For the people who are familiar with the process and just want a quick glance at the steps, I am going to give the commands directly here itself, but remember, these will not be detailed or updated as the wiki. Always use the wiki to install Arch Linux and never follow any third party's resource. Having said that, here are the commands / steps to get things up and running.

[I know to install, skip past installation](#conclusion)

## Installing Arch Linux

- Partition your hard disks the way you want, set up raids, filesystems, lvm, dmcrypt or whatever you need and mount the root of the new installation at `/mnt/`.

- Mount the partitions of ESP, boot, and other disks/partitions/filesystems at their respective places.

- Set the number of parallel downloads to 8 (eight) in `/etc/pacman.conf` (This file appears once you install pacman using dnf on the live ISO). Also, modern versions of `arch-install-scripts` might have this set to 5 already.

- The default mirrors were fast enough for me, if it is not for you, edit the mirrorlist and use some local mirrors.

### Pacstrap

```
pacstrap /mnt base base-devel linux-zen linux-firmware networkmanager neovim man-db man-pages texinfo tldr gnome gnome-extra fish amd-ucode reflector
```

The `-K` option initializes a new keyring, which is recommended by the arch wiki. But it is not included here because, we want the keys to be copied from the host system (the live environment we are in), because we initialized the keyring and refreshed the keys just now. Substitute your prefered window manager or DE in place of `gnome` and `gnome-extra` and `intel-ucode` in place of `amd-ucode` for intel systems. Add packages for your fancy raid or lvm setups. Fish shell for a user friendly shell. Once it completes,

### Fstab

```
genfstab -U /mnt >> /mnt/etc/fstab
```

#### Important

_When `genfstab` is run from the Fedora ISO, it creates an entry for zram swap as well, which doesn't work in Arch Linux out of the box (It needs manual setup). This will stop you from booting. So, make sure you remove the zram entry from the fstab file (`/mnt/etc/fstab`)._

### Chroot

```
arch-chroot /mnt
```

### Time zone and time

```
ln -sf /usr/share/zoneinfo/Asia/Kolkata /etc/localtime
hwclock --systohc
```

### Localization

```
echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen
locale-gen
echo "LANG=en_US.UTF-8" >> /etc/locale.conf
```

### Hostname

```
echo "Billy" >> /etc/hostname
```

Thanks to [Mutahar](https://www.youtube.com/c/SomeOrdinaryGamers) for the name Billy.

You can also set the hostname using systemd. Check Arch Wiki to know how to do that.

### Initramfs

Add necessary modules, hooks, binaries to `/etc/mkinitcpio.conf`. I like setting the compression to `cat` or `lz4` for fast decompression of initramfs.

```
mkinitcpio -P
```

### User accounts

```
passwd
useradd -m -G wheel -s /usr/bin/fish -C "Bobby" bobby
passwd bobby
EDITOR=vim visudo // add bobby to sudoers
```

### Network Manager

```
systemctl enable NetworkManager
systemctl enable gdm // if gnome is installed
```

### Bootloader

```
bootctl install
systemctl enable systemd-boot-update
```

You have to create config files for systemd boot. Check the [arch wiki page](https://wiki.archlinux.org/title/systemd-boot) for details.

#### GRUB

To take the easier route, install grub.

```
pacman -S grub --noconfirm
grub-install --target=x86_64-efi --efi-directory=esp --bootloader-id=GRUB
grub-mkconfig -o /boot/grub/grub.cfg
```

### pacman.conf and makepkg.conf

Uncomment the `MAKEOPTS` flag in `/etc/makepkg.conf` and set its value to `$(nproc)`.

See parallel downloads are set in `/etc/pacman.conf`

Enable [multilib](https://wiki.archlinux.org/title/official_repositories#multilib) if needed

Enable [chaotic-aur](https://aur.chaotic.cx/) if needed

Reboot.

## Post Installation

You will be greeted with GDM's greeter. Login with bobby's password and open a terminal.

### AUR

If chaotic-aur is enabled, simply install yay with

```
sudo pacman -Syu yay
```

If not

```
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```

And that's it. You have a functional Arch Linux setup ready.

<a name="conclusion"></a>

## Shortcomings of this method

Like any method, this is not perfect (but close to perfect, according to me)

- First `dnf` run takes a long time on all Fedora systems as dnf downloads all the package databases. Nothing much we can do in our live ISO.
- `genfstab` adds a `zram` entry in Fedora. We have to manually remove the entry.
- Sometimes, due to old version of `arch-install-scripts` or some other bug, the signature verification of some or all of the downloaded files fail, we may temporarily set `SigLevel` not to check and get around this, but it is not recommended. Also remember that pacstrap deletes downloaded files without confirmation if signature verification fails.

## Conclusion

This article is meant to supplement [this page](https://wiki.archlinux.org/title/Install_Arch_Linux_from_existing_Linux) of the Arch Wiki. Refer the Arch Wiki's installation guide exclusively for installation steps.

Hope you learnt something useful. If you have any feedback, send an [email](mailto://berinaniesh@gmail.com). You can also submit pull requests to the [github repo of this website](https://github.com/berinaniesh/berinaniesh.github.io). Have a good one. Cheers!
