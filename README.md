# Topologi
![image](https://cdn.discordapp.com/attachments/677050949432377345/1049940255916171334/image.png)
# Pembagian Subnet
![image](https://media.discordapp.net/attachments/677050949432377345/1049940071844937820/image.png?width=846&height=559)
# Pembagian IP
![image](https://user-images.githubusercontent.com/74979139/206114789-c3bb1c5b-0b33-4a62-b05d-be3e2f6057fd.png)
# Routing
- Strix
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.191.0.1
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 192.191.0.5
	netmask 255.255.255.252
  ```
- Westalis
```
auto eth0
iface eth0 inet static
	address 192.191.0.6
	netmask 255.255.255.252
	gateway 192.191.0.5
  
auto eth1
iface eth1 inet static
	address 192.191.0.9
	netmask 255.255.252.248
  
auto eth2
iface eth2 inet static
	address 192.191.0.65
	netmask 255.255.255.192
  
auto eth3
iface eth3 inet static
	address 192.191.4.1
	netmask 255.255.252.0
```
- Ostania
```
auto eth0
iface eth0 inet static
	address 192.191.0.2
	netmask 255.255.255.252
	gateway 192.191.0.1
  
auto eth1
iface eth1 inet static
	address 192.191.2.1
	netmask 255.255.254.0
  
auto eth2
iface eth2 inet static
	address 192.191.1.1
	netmask 255.255.255.0
  
auto eth3
iface eth3 inet static
	address 192.191.0.17
	netmask 255.255.255.248
```
- Eden
```
auto eth0
iface eth0 inet static
	address 192.191.0.10
	netmask 255.255.255.248
  gateway 192.191.0.9
```

- WISE
```
auto eth0
iface eth0 inet static
	address 192.191.0.11
	netmask 255.255.255.248
  gateway 192.191.0.9
```
- Garden
```
auto eth0
iface eth0 inet static
	address 192.191.0.18
	netmask 255.255.255.248
	gateway 192.191.0.17
```
- SSS
```
auto eth0
iface eth0 inet static
	address 192.191.0.19
	netmask 255.255.255.248
	gateway 192.191.0.17
```
- Forger
- Desmond
- Blackbell
- Briar
```
auto eth0
iface eth0 inet dhcp
```
## Command Routing
- Strix
```
# dari Ostania
route add -net 192.191.1.0 netmask 255.255.255.0 gw 192.191.0.2
route add -net 192.191.2.0 netmask 255.255.254.0 gw 192.191.0.2
route add -net 192.191.0.16 netmask 255.255.255.248 gw 192.191.0.2
# dari Westalis
route add -net 192.191.4.0 netmask 255.255.252.0 gw 192.191.0.6
route add -net 192.191.0.64 netmask 255.255.255.192 gw 192.191.0.6
route add -net 192.191.0.8 netmask 255.255.255.248 gw 192.191.0.6
```
- Westalis
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.191.0.5
```
- Ostania
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.191.0.1
```

## Konfigurasi Routing
- tambahkan kode berikut di `/etc/sysctl.conf` untuk `Strix`, `Westalis` dan `Ostania`
```
net.ipv4.ip_forward=1
net.ipv4.conf.all.accept_source_route = 1
```

## Konfigurasi dhcpd
```
# (Forger)
subnet 192.191.0.64 netmask 255.255.255.192 {
    range 192.191.0.66 192.191.0.126;
    option routers 192.191.0.65;
    option broadcast-address 192.191.0.127;
    option domain-name-servers 192.191.0.10; # IP Eden
    default-lease-time 600;
    max-lease-time 7200;
}

# (Desmond)
subnet 192.191.4.0 netmask 255.255.252.0 {
    range 192.191.4.2 192.191.7.191;
    option routers 192.191.4.1;
    option broadcast-address 192.191.7.255;
    option domain-name-servers 192.191.0.10;
    default-lease-time 600;
    max-lease-time 7200;
}

# (Blackbell)
subnet 192.191.2.0 netmask 255.255.254.0 {
    range 192.191.2.2 192.191.3.0;
    option routers 192.191.2.1;
    option broadcast-address 192.191.3.255;
    option domain-name-servers 192.191.0.10;
    default-lease-time 600;
    max-lease-time 7200;
}

# (Briar)
subnet 192.191.1.0 netmask 255.255.255.0 {
    range 192.191.1.2 192.191.1.201;
    option routers 192.191.1.1;
    option broadcast-address 192.191.1.255;
    option domain-name-servers 192.191.0.10;
    default-lease-time 600;
    max-lease-time 7200;
}

# (self)
subnet 192.191.0.8 netmask 255.255.255.248 {}
```
