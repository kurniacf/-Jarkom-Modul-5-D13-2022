# Praktikum Jaringan Komputer Modul 4 Kelompok D13

# Jarkom-Modul-4-D13-2022

| **No** | **Nama**                  | **NRP**    |
| ------ | ------------------------- | ---------- |
| 1      | Marcellino Mahesa Janitra | 5025201105 |
| 2      | Kurnia Cahya Febryanto    | 5025201073 |
| 3      | Abisha Kean Tuana Sirait  | 5025201052 |

---

## Daftar Isi

## Topologi
![image](https://cdn.discordapp.com/attachments/677050949432377345/1049940255916171334/image.png)
## Pembagian Subnet
![image](https://media.discordapp.net/attachments/677050949432377345/1049940071844937820/image.png?width=846&height=559)
## Pembagian IP
![image](https://user-images.githubusercontent.com/74979139/206114789-c3bb1c5b-0b33-4a62-b05d-be3e2f6057fd.png)
## Routing

### Eden
```
auto eth0
iface eth0 inet static
	address 192.191.0.10
	netmask 255.255.255.248
  	gateway 192.191.0.9
```

### WISE
```
auto eth0
iface eth0 inet static
	address 192.191.0.11
	netmask 255.255.255.248
  	gateway 192.191.0.9
```

### Garden
```
auto eth0
iface eth0 inet static
	address 192.191.0.18
	netmask 255.255.255.248
	gateway 192.191.0.17
```

### SSS
```
auto eth0
iface eth0 inet static
	address 192.191.0.19
	netmask 255.255.255.248
	gateway 192.191.0.17
```

### Ostania
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

### Westalis
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
	netmask 255.255.255.128
  
auto eth3
iface eth3 inet static
	address 192.191.4.1
	netmask 255.255.252.0
```

### Strix
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
- Forger
- Desmond
- Blackbell
- Briar

## Command Routing

### Eden
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### WISE
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Garden
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### SSS
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Ostania
```
echo nameserver 192.168.122.1 > /etc/resolv.conf

route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.191.0.1
route add -net 192.191.0.8 netmask 255.255.255.248 gw 192.191.0.1
# route add -net 192.191.0.64 netmask 255.255.255.128 gw 192.191.0.1
route add -net 192.191.4.0 netmask 255.255.252.0 gw 192.191.0.1
# route add -net 192.191.0.6 netmask 255.255.255.252 gw 192.191.0.1
```

### Westalis
```
echo nameserver 192.168.122.1 > /etc/resolv.conf

route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.191.0.5
# route add -net 192.191.0.1 netmask 255.255.255.252 gw 192.191.0.5
route add -net 192.191.1.0 netmask 255.255.255.0 gw 192.191.0.5
route add -net 192.191.2.0 netmask 255.255.254.0 gw 192.191.0.5
route add -net 192.191.0.16 netmask 255.255.255.248 gw 192.191.0.5
```

### Strix
```
iptables -t nat -A POSTROUTING -o eth0 -j SNAT -s 10.25.0.0/21 --to-source 192.168.122.2

# dari Ostania
route add -net 192.191.1.0 netmask 255.255.255.0 gw 192.191.0.2
route add -net 192.191.2.0 netmask 255.255.254.0 gw 192.191.0.2
route add -net 192.191.0.16 netmask 255.255.255.248 gw 192.191.0.2

# dari Westalis
route add -net 192.191.4.0 netmask 255.255.252.0 gw 192.191.0.6
route add -net 192.191.0.64 netmask 255.255.255.192 gw 192.191.0.6
route add -net 192.191.0.8 netmask 255.255.255.248 gw 192.191.0.6
```

## Konfigurasi Routing
- tambahkan kode berikut di `/etc/sysctl.conf` untuk `Strix`, `Westalis` dan `Ostania`
```
net.ipv4.ip_forward=1
net.ipv4.conf.all.accept_source_route = 1
```
