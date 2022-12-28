# asus-g15-GA503-2022-Ubuntu-setup

Doing the fresh install and keeping the older nvidia drivers works for maintaining suspend and hibernate behavior.
However, if you update to a much new Nvidia driver it can break your suspend and not be able to go back even when rolling back the drivers.


Using Nvidia 515.86.01 this was the fix for suspend:
help diagnosing:
https://askubuntu.com/questions/1196871/gnome-supend-on-laptop-lid-close-no-longer-works-since-19-10-upgrade
https://superuser.com/questions/958594/logind-conf-not-working-closing-lid-will-not-suspend-laptop
key --> https://askubuntu.com/questions/1391976/ubuntu-20-04-suspend-logs-off-and-wakes-up
tl;dr solution:
sudo rm /etc/systemd/system/systemd-suspend.service.requires/*
sudo reboot now

Hibernate solution:
Redo all the hibernate stuff from the initial setup doc
https://askubuntu.com/questions/411583/could-not-stat-the-resume-device-file
look for errors in /var/log/pm-suspend.log  when running sudo pm-hiberate
https://blog.ivansmirnov.name/how-to-set-up-hibernate-on-ubuntu-20-04/
in the /etc/initramfs-tools/conf.d/resume  file the RESUME must be caps or it will not work!
pm-hibernate works now but wifi can be sketch after resume...
to make the hibernate menu work systemd needs to get fixed but dunno what it is.
Shortcut is might be to tell it to use pm-hibernate but this doesnt work as it...
https://askubuntu.com/questions/974788/how-to-make-linux-prefer-sudo-pm-hibernate-over-systemctl-hibernate-as-default


Change grub resolution for boot menu:
The boot screen resolution is changed by changing your default grub settings. Open a terminal and enter:
sudo nano /etc/default/grub
Use the down arrow or Page Down until you see the line that looks like this:
#GRUB_GFXMODE=640x480
Below that line, enter the following, substituting the 1920x1080 for a supported resolution:
GRUB_GFXMODE=1920x1080
GRUB_GFXPAYLOAD_LINUX=keep
To save your changes, hit Ctrl+o, with "o" as in Ohio, not zero. To exit nano, hit Ctrl+x. Now, update grub:
sudo update-grub

and login screen:
https://albertomatus.com/changing-login-display-in-ubuntu-20-04/
