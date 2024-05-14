## This is the default config for different proxmox settings I use.

## Proxmox intitial setup.

1. **suppress messages**

```xml
sudo dmesg -n 1
```

---

2. **disable AER**

```xml
nano /etc/default/grub
```

```xml
GRUB_DEFAULT=0 
GRUB_TIMEOUT=5
GRUB_DISTRIBUTOR=`lsb_release -i -s 2> /dev/null || echo Debian`
GRUB_CMDLINE_LINUX_DEFAULT="pci=nommconf"
GRUB_CMDLINE_LINUX="pci=noaer"
```

---

3. **disable services that pacman ssd to REDUCE SSD wearout** *

```xml
systemctl to stop & disable pve-ha-lrm/pve-ha-crm 
systemctl stop pve-ha-lrm
systemctl disable pve-ha-lrm
systemctl disable pve-ha-lrm
systemctl stop pve-ha-lrm
```

---

4. change to non-subscription proxmox to drop any errors and allow updates(can pay if you want of course)

```xml
   nano /etc/apt/sources.list
```

```xml
deb http://ftp.debian.org/debian bookworm main contrib
deb http://ftp.debian.org/debian bookworm-updates main contrib

Proxmox VE pve-no-subscription repository provided by proxmox.com

## NOT recommended for production use

deb http://download.proxmox.com/debian/pve bookworm pve-no-subscription

security updates

deb http://security.debian.org/debian-security bookworm-security main contribdeb http://ftp.debian.org/debian bookworm main contrib
deb http://ftp.debian.org/debian bookworm-updates main contrib

Proxmox VE pve-no-subscription repository provided by proxmox.com

## NOT recommended for production use

deb http://download.proxmox.com/debian/pve bookworm pve-no-subscription

security updates

deb http://security.debian.org/debian-security bookworm-security main contribdeb http://ftp.debian.org/debian bookworm main contrib
deb http://ftp.debian.org/debian bookworm-updates main contrib

Proxmox VE pve-no-subscription repository provided by proxmox.com
```

---

5. edit crontab to reduce energy

```xml
crontab -e
```

```xml
@reboot echo "powersave" | tee /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor
```
