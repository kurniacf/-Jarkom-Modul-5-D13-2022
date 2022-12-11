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

# **No. 1** 
Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Strix menggunakan iptables, tetapi Loid tidak ingin menggunakan MASQUERADE.
- pada Strix
```
IPETH0="$(ip -br a | grep eth0 | awk '{print $NF}' | cut -d'/' -f1)"
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source "$IPETH0" -s 192.191.0.0/21
```

# **No. 2** 
Kalian diminta untuk melakukan drop semua TCP dan UDP dari luar Topologi kalian pada server yang merupakan DHCP Server demi menjaga keamanan.
- pada Strix
```
iptables -A FORWARD -d 192.191.0.11 -i eth0 -p tcp -j DROP
iptables -A FORWARD -d 192.191.0.11 -i eth0 -p udp -j DROP
```
- menggunakan ```iptables```
- ```-A``` mengappend rule ```FORWARD``` karena akan diteruskan ke dhcp server
- ```-d``` merupakan destinasi ke ip dhcp server yaitu ```192.191.0.11```
- ```-i``` nge match paket pada interface yg di mau in, disini ```eth0``` karena terhubung ke NAT
- ```-p``` protocolnya apa, disoal diminta ```tcp``` dan ```udp```
- ```-j``` jump packet ke sebuah target aksi, di soal diminta ```DROP```

# **No. 3**
Loid meminta kalian untuk membatasi DHCP dan DNS Server hanya boleh menerima maksimal 2 koneksi ICMP secara bersamaan menggunakan iptables, selebihnya didrop.
- Config DHCP Server (WISE) dan DNS Server (Eden)
```
iptables -A INPUT -p icmp -m connlimit --connlimit-above 2 --connlimit-mask 0 -j DROP
```
- menggunakan rule connection limit ```-m connlimit```
- ```--connlimit-mask 0``` untuk semua paket masuk bakalan menggunakan filtering dari connlimit
- untuk diatas 2 paket ```--connlimit-above 2```
- ```-j DROP``` akan di drop 

# **No. 4**
Akses menuju Web Server hanya diperbolehkan disaat jam kerja yaitu Senin sampai Jumat pada pukul 07.00 - 16.00.
- pada Web Server (Garden dan SSS)
```
iptables -A INPUT -m time --timestart 07:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -j REJECT
```
- diantara jam 07:00 dan 16:00 bakalan ```ACCEPT```
- selain itu ```REJECT```

# **No. 5**
Karena kita memiliki 2 Web Server, Loid ingin Ostania diatur sehingga setiap request dari client yang mengakses Garden dengan port 80 akan didistribusikan secara bergantian pada SSS dan Garden secara berurutan dan request dari client yang mengakses SSS dengan port 443 akan didistribusikan secara bergantian pada Garden dan SSS secara berurutan.

- pada Ostania
```
iptables -A PREROUTING -t nat -p tcp --dport 80 -d 192.191.0.18 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 192.191.0.19:80
iptables -A PREROUTING -t nat -p tcp --dport 433 -d 192.191.0.19 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 192.191.0.18:433
```
- ```-A``` append rule ```PREROUTING```
- yang pertama, destination port untuk rule ini 80 untuk ```Garden``` ```--dport 80 -d 192.191.0.18``` ke ```SSS``` dengan port 80 ```--to-destination 192.191.0.19:80```
- yang kedua gantian, destination port untuk rule ini 80 dari ```SSS``` ```--dport 433 -d 192.191.0.19``` ke ```Garden``` dengan port 80 ```--to-destination 192.191.0.18:433```
- ```--every 2``` mengatur distribusi packet

# **No. 6**
Karena Loid ingin tau paket apa saja yang di-drop, maka di setiap node server dan router ditambahkan logging paket yang di-drop dengan standard syslog level
- pada setiap node server dan router
```
iptables -A INPUT  -j LOG --log-level debug --log-prefix 'Dropped Packet'
```
