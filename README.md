# systemd-networkd-bootd
configuration to install arch with systemd-networkd and systemd-bootd instead of NetworkManager.service and GRUB


#### systemd-networkd config

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
WIFI support

WPA supplicant config

```
nano /etc/wpa_supplicant/wpa_supplicant.conf
```
```
ctrl_interface=/run/wpa_supplicant
update_config=1

network={
    ssid="YOUR_WIFI_NAME"
    psk="YOUR_WIFI_PASSWORD"
}
```
Enable it:

```
sudo systemctl enable wpa_supplicant@wlan0
```
```
sudo systemctl start wpa_supplicant@wlan0
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

------------------------------------------------------------------------------------------------------------------------

