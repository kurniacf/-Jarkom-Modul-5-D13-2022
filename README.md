# Praktikum Jaringan Komputer Modul 5 Kelompok D13

# Jarkom-Modul-5-D13-2022

## **Data Kelompok D13**
| **No** | **Nama**                  | **NRP**    |
| ------ | ------------------------- | ---------- |
| 1      | Marcellino Mahesa Janitra | 5025201105 |
| 2      | Kurnia Cahya Febryanto    | 5025201073 |
| 3      | Abisha Kean Tuana Sirait  | 5025201052 |

## Daftar Isi
- [Topologi Jaringan](#topologi)
- [Pembagian Subnet](#pembagian-subnet)
- [Pembagian IP](#pembagian-ip)
- [Routing](#routing)
  - [Eden](#eden)
  - [WISE](#wise)
  - [Garden](#garden)
  - [SSS](#sss)
  - [Ostania](#ostania)
  - [Westalis](#westalis)
  - [Strix](#strix)
- [Command Routing](#command-routing)
  - [Eden](#eden-1)
  - [WISE](#wise-1)
  - [Garden](#garden-1)
  - [SSS](#sss-1)
  - [Ostania](#ostania-1)
  - [Westalis](#westalis-1)
  - [Strix](#strix-1)
- [konfigurasi Routing](#konfigurasi-routing)
- [Konfigurasi DHCP](#konfigurasi-dhcp)

- [No 1](#no-1)
- [No 2](#no-2)
- [No 3](#no-3)
- [No 4](#no-4)
- [No 5](#no-5)
- [No 6](#no-6)

# Topologi
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
auto eth0
iface eth0 inet static
	address 192.191.0.11
	netmask 255.255.255.248
  gateway 192.191.0.9
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

- tes ping google di wise
![image](https://user-images.githubusercontent.com/74979139/206895940-54013285-ac58-4d5b-8a2c-17d080594919.png)

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

## tes ping ke ```Eden``` dari 3 client bersamaan
- ```Blackbell```

![image](https://user-images.githubusercontent.com/74979139/206896052-e5b65447-365c-44f6-a039-86bbd47c486b.png)
- ```Forger```

![image](https://user-images.githubusercontent.com/74979139/206896059-6f32ab26-4f37-4f5f-a6d8-cb6f7c31cc11.png)
- ```Desmond```

![image](https://user-images.githubusercontent.com/74979139/206896063-e3659f54-e3a7-4dc4-bcf0-a837189e9026.png)


# **No. 4**
Akses menuju Web Server hanya diperbolehkan disaat jam kerja yaitu Senin sampai Jumat pada pukul 07.00 - 16.00.
- pada Web Server (Garden dan SSS)
```
iptables -A INPUT -m time --timestart 07:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -j REJECT
```
- diantara jam 07:00 dan 16:00 bakalan ```ACCEPT```
- selain itu ```REJECT```
## Test
- ngeping ke garden saat diluar jam kerja

![image](https://user-images.githubusercontent.com/74979139/206896137-28cc87f6-fbb9-448f-8de3-64787ef215f3.png)

- ngeping ke sss saat diluar jam kerja

![image](https://user-images.githubusercontent.com/74979139/206896162-3956d1dd-545e-437c-bc37-c68a2fda7781.png)

- ngeping ke garden saat jam kerja

![image](https://user-images.githubusercontent.com/74979139/206897070-039ee40c-27d5-4974-9a35-fbc3b2621bc8.png)

- ngeping ke sss saat jam kerja

![image](https://user-images.githubusercontent.com/74979139/206897094-802fa3ac-b934-4e07-a5bc-41c9a5caebfa.png)



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

## Test
- menggunakan command ```while true; do nc -l -p 80 -c 'echo $HOSTNAME'; done``` pada ```SSS``` dam ```Garden``` untuk mengetahui host mana yang diakses
- jika ingin nge ping ke port 433, ganti ```-p 80``` dengan ```-p 433```
- untuk nge ping nya pakai command ```nc [ip Garden] 80``` atau ```nc [ip SSS] 433```

# **No. 6**
Karena Loid ingin tau paket apa saja yang di-drop, maka di setiap node server dan router ditambahkan logging paket yang di-drop dengan standard syslog level
- pada setiap node server dan router
```
iptables -A INPUT  -j LOG --log-level debug --log-prefix 'Dropped Packet'
```

## Test
- gunakan command ```iptables -L``` untuk melihat config test sudah ada belum
