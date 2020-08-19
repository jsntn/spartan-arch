# spartan-arch

This is a set of scripts designed to automate the creation of a minimal VM running Arch Linux and i3/Emacs as a Windows manager. This VM can be used as a file editor for the  host via folder sharing and as a development environment. Currently, the VM costs about 90MB of RAM to run.

## Requirements for Virtual Box VM
- 8GB of space on disk
- 1GB of RAM
- Clipboard sharing in both directions enabled
- Two shared folders `org` and `workspace` auto-mount and permanent

## Installation
Boot the VM on archlinux iso and then run the command
```shell
wget https://raw.githubusercontent.com/jsntn/spartan-arch/my-version/install.sh -O install.sh
bash install.sh [user] [password] [fast]
```
All arguments are optional and will be prompted for if not passed on invocation:
- `[user]` is your username
- `[password]` is what you want the root and user password to be
- `[fast]` is boolean 1 or 0 and controls using `rankmirrors` during set up which will be slow

The install.sh script will run and then reboot the computer once done.

You want to boot on disk this time and eject the cd from the VM.

If the virtual machine doesn't boot successfully, but appears `grub>` prompt, boot it from cd, then try to fix it as the following way,

```shell
mount /dev/sda1
arch-chroot /mnt
grub-mkconfig -o /boot/grub/grub.cfg
```

(via [Grub not installed on reboot?](https://github.com/abrochard/spartan-arch/issues/1))

You would probably like to continue to solve the internet connection from virtual machine with NAT, install `dhcpcd` first, then enable the service,

```shell
pacman -Sy dhcpcd
systemctl enable dhcpcd.service
```

(via [Install Arch Linux on Oracle VM VirtualBox](https://web.archive.org/web/20200819055253/https://kuroigengetsu.gitbooks.io/installarchlinuxonvirtualbox/content/chapter1.html))

Eject the cd and reboot the virtual machine.

Login as your user then run the command
```shell
bash post-install.sh
```
The script will ask for the root password a couple of times.

## Usage
Once the VM is booted, log in as your user and call `startx` to start Xorg.

## TODO
- dhcpcd on boot
- ssh-keys generation

## Thanks

- [Install Arch Linux on VirtualBox](https://web.archive.org/web/20200819055606/https://kuroigengetsu.gitbooks.io/installarchlinuxonvirtualbox/content/)