# Piwall setup guide

## Requirements
- Raspbian Jessie (the lastest version of Raspbian)
- Each Raspberry Pi must be connected to each other (internet is required only for the first step of the configuration of the Raspberry Pi client and master)

## Configuration of each Raspberry Pi client

1.First, install the program `pwomxplayer` and the librairy `pwlibs` using their Debian package:

>1. Download the files and save it to the Desktop: https://github.com/unixfox/piwall-school/raw/master/pwomxplayer_20130815_armhf.deb & https://github.com/unixfox/piwall-school/raw/master/pwlibs1_1.7_armhf.deb
>2. Install it using dpkg -i /home/ubuntu/Desktop/pwomxplayer_20130815_armhf.deb or double click on the file on the Desktop.

2.Replace the file `/etc/networking/interfaces` with this content:
```
auto eth0
iface eth0 inet static
 address 192.168.0.1
 netmask 255.255.255.0
 up route add -net 224.0.0.0 netmask 240.0.0.0 eth0
 ```
 **Note**: Change the last number of the IP address with `2` for the second Raspberry Pi and so on for the others Raspberry Pi.

and restart the networking service using this command:
```
sudo service networking restart
```

3.Add the file `/home/pi/.pititle` with this content:
 ```
[tile]
id=a
```
**Note**: Replace the letter id `a` with `b` for the second Raspberry Pi and so on for the others Raspberry Pi.

4.Add the file `/etc/systemd/systemd/piwallclient.service` with this content:
```
[Unit]
Description=Piwall Client

[Service]
ExecStart=/usr/bin/pwomxplayer --autotile udp://239.0.1.23:1234?buffer_size=1200000B
Environment=DISPLAY=0
User=pi
Group=pi

[Install]
WantedBy=multi-user.target
```
5.Reload the configuration of the daemon system manager or reboot the Raspberry Pi:
```
sudo systemctl daemon-reload
```

## Configuration of the master Raspberry Pi
