# systemd-networkd-bootd
configuration to install arch with systemd-networkd and systemd-bootd instead of NetworkManager.service and GRUB


### systemd-networkd config

#### Ethernet Support
check your network adapter
```
ip a
```

enable systemd-networkd service and systemd-resolvd
```
systemctl enable systemd-networkd.service
```
```
systemctl enable systemd-resolved.service
```

soft link the resolv.conf file
```
ln -sf /run/systemd/resolve/stub-resolv.conf /etc/resolv.conf
```

create ```/etc/systemd/network/20-wired.network``` config file
```
nano /etc/systemd/network/20-wired.network
```
```
[Match]
Name=<network-adapter-name>

[Network]
DHCP=yes
```
-----------------------------------------------------------------------------------------------------------------------
#### WIFI support

```
sudo nano /etc/iwd/main.conf
```
```
[General]
EnableNetworkConfiguration=false
```

Wi-Fi network config for networkd

```
nano /etc/systemd/network/25-wireless.network
```
```
[Match]
Name=<wireless-network-adapter-name>

[Network]
DHCP=yes
```

Connecting to WiFi using iwd (one time)
```
iwctl
```
```
device list
station wlan0 scan
station wlan0 get-networks
station wlan0 connect YOUR_SSID
```

------------------------------------------------------------------------------------------------------------------------

### systemd-bootd config
