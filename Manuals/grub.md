# Grub
## Change Default Device
1. go to /etc/default/grub
2. chenge ```GRUB_DEFAULT=0```
3. run ```sudo grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg```