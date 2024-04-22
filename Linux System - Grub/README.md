# GRUB

Useful Resources
- https://docs.fedoraproject.org/en-US/fedora/latest/system-administrators-guide/kernel-module-driver-configuration/Working_with_the_GRUB_2_Boot_Loader/
- https://www.baeldung.com/linux/grub-menu-management
- https://itsfoss.com/update-grub/

GRUB (Grand Unified Bootloader)
Common tool for performing the boot process in Linux systems.

NOTE: Despite the intended similarity in the way it is used, the method of managing it from one Linux distribution to another varies.


GRUB parameters are stored in /etc/default/grub

EXAMPLE:

$ cat /etc/default/grub
GRUB_TIMEOUT="5"
GRUB_DISTRIBUTOR="$(sed 's, release .*$,,g' /etc/system-release)"
GRUB_DEFAULT="saved"
GRUB_DISABLE_SUBMENU="true"
GRUB_TERMINAL_OUTPUT="console"
GRUB_CMDLINE_LINUX=""
GRUB_DISABLE_RECOVERY="true"
GRUB_ENABLE_BLSCFG="true"


To edit the /etc/default/grub file:


```
vi /etc/default/grub
```

To update grub.cfg 

```
grub2-mkconfig -o /boot/grub2/grub.cfg
```



(for Ubuntu)
Ubuntu, and other Linux distrobutions provide a command line utility called update-grub.  The update-grub command is simply a stub for running ‘grub-mkconfig -o /boot/grub/grub.cfg’ to generate grub2 config file.

NOTE: Around ten years ago, when grub2 was just introduced, update-grub2 command was also introduced. Today, update-grub2 is just a symbolic link to update-grub and both update grub2 configuration (because grub2 is the default).


```
update-grub
```
```
update-grub2
```


-----------------------



Menu Auto-Hide Fuction
Hides the GRUB menu when only one kernel is available.  Older kernel verisons preserved for the purpose of rescue don't count.

To Disable:

```
grub2-editenv - unset menu_auto_hide
```
