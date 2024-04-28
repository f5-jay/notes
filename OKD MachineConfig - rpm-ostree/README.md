# Machine Config Stuck - RPM-OSTree Failed


Any node that ends up in this situation will need manual intervention. Zincati cannot auto-update out of it, as rpm-ostreed is not available.

Nodes that are stuck require manually intervention to proceed with upgrades.
The workaround is to manually mount /boot, restart rpm-ostree and zincati, and let the
auto-upgrades proceed:


```
sudo mount /dev/disk/by-label/boot /boot
sudo systemctl reset-failed rpm-ostreed.service
sudo systemctl restart rpm-ostreed.service zincati.service
```
