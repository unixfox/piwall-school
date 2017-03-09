# Piwall setup guide

## Configuration of each raspberry pi client
1.First, replace the file `/etc/networking/interfaces` with this content:
```
auto eth0
iface eth0 inet static
 address 192.168.0.1
 netmask 255.255.255.0
 up route add -net 224.0.0.0 netmask 240.0.0.0 eth0
 ```
 **Note**: Change the last number of the IP address for the second raspberry pi and so on.

2.Add the file `/home/pi/.pititle` with this content:
 ```
[tile]
id=a
```
**Note**: Replace the letter id (`a`) with `b` for the second raspberry pi and so on.
