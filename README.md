# Jarkom_Modul5_Lapres_C13

# LAPRES MODUL 5 JARKOM

### KELOMPOK C13:
#### 1) Rida Adila 051111840000002
#### 2) Bayu Surya B. 05111840000114

********

#### A) MEMBUAT TOPOLOGI
#
**TOPOLOGI**
![image](https://user-images.githubusercontent.com/71973415/103262262-0b38cc00-49d7-11eb-8e1e-8392c696e42d.png)
#

**Topologi.sh :**

```
# Switch

uml_switch -unix switch1 > /dev/null < /dev/null & 
uml_switch -unix switch2 > /dev/null < /dev/null & 
uml_switch -unix switch3 > /dev/null < /dev/null & 
uml_switch -unix switch4 > /dev/null < /dev/null & 
uml_switch -unix switch5 > /dev/null < /dev/null & 
uml_switch -unix switch6 > /dev/null < /dev/null & 

# Router
xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.76.57 eth1=daemon,,,switch4 eth2=daemon,,,switch3 mem=96M &
xterm -T KEDIRI -e linux ubd0=KEDIRI,jarkom umid=KEDIRI eth0=daemon,,,switch3 eth1=daemon,,,switch1 eth2=daemon,,,switch5 mem=96M &
xterm -T BATU -e linux ubd0=BATU,jarkom umid=BATU eth0=daemon,,,switch4 eth1=daemon,,,switch2 eth2=daemon,,,switch6 mem=96M &

# DNS_Server
xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch2 mem=128M &
xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch2 mem=128M &

# Web_Server
xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch1 mem=128M &
xterm -T PROBOLINGGO -e linux ubd0=PROBOLINGGO,jarkom umid=PROBOLINGGO eth0=daemon,,,switch1 mem=128M &

# Client
xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch6 mem=96M &
xterm -T GRESIK -e linux ubd0=GRESIK,jarkom umid=GRESIK eth0=daemon,,,switch5 mem=96M &
```

#### B) SUBNETTING DAN ROUTING DENGAN VLSM
#
![image](https://user-images.githubusercontent.com/71973415/103262396-64a0fb00-49d7-11eb-861d-52ff12c6e944.png)
#
![image](https://user-images.githubusercontent.com/71973415/103262462-95813000-49d7-11eb-8db6-fdb9eef00df5.png)
#
![image](https://user-images.githubusercontent.com/71973415/103262529-c19cb100-49d7-11eb-9bb5-4a5a44482d97.png)
#
**GAMBAR TREE VLSM :**
![image](https://user-images.githubusercontent.com/71973415/103262545-d2e5bd80-49d7-11eb-9481-45621ccfdf5e.png)
#
**Untuk server :**

![image](https://user-images.githubusercontent.com/71973415/103262584-eb55d800-49d7-11eb-90f9-8fa5a5c9a974.png)
#
**Dari pohon yang didapatkan, pembagian IP nya adalah :**

![image](https://user-images.githubusercontent.com/71973415/103262636-1c360d00-49d8-11eb-8733-0f3bdd83488b.png)

![image](https://user-images.githubusercontent.com/71973415/103263136-88fdd700-49d9-11eb-8817-d9272e8f5ea1.png)

- Atur intefaces pada setiap UML dengan ```nano /etc/network/interfaces```

**SURABAYA :**
```auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.76.58
netmask 255.255.255.248
gateway 10.151.76.57

auto eth1
iface eth1 inet static
address 192.168.0.6
netmask 255.255.255.252

auto eth2
iface eth2 inet static
address 192.168.0.2
netmask 255.255.255.252
```

- ```service networking restart``` di UML Surabaya



**KEDIRI :**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.0.1
netmask 255.255.255.252
gateway 192.168.0.2

auto eth1
iface eth1 inet static
address 192.168.0.11
netmask 255.255.255.248

auto eth2
iface eth2 inet static
address 192.168.2.2
netmask 255.255.255.0
```

- ```service networking restart``` di UML Kediri

#
**BATU :**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.0.5
netmask 255.255.255.252
gateway 192.168.0.6

auto eth1
iface eth1 inet static
address 10.151.77.115
netmask 255.255.255.248

auto eth2
iface eth2 inet static
address 192.168.1.2
netmask 255.255.255.0
```

- ```service networking restart``` di UML Batu


**MALANG :**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.77.113
netmask 255.255.255.248
gateway 10.151.77.115
```

- ```service networking restart``` di UML Malang
#
**MOJOKERTO :**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.77.114
netmask 255.255.255.248
gateway 10.151.77.115
```

- ```service networking restart``` di UML Mojokerto.


**SIDOARJO :**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.1.1
netmask 255.255.255.0
gateway 192.168.1.2
```

- ```service networking restart``` di UML Sidoarjo.
#
**GRESIK :**
```auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.2.1
netmask 255.255.255.0
gateway 192.168.2.2
```

- ```service networking restart``` di UML Gresik.
#
**PROBOLINGGO :**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.0.10
netmask 255.255.255.248
gateway 192.168.0.11
```
- ```service networking restart``` di UML Probolinggo
#
**MADIUN :**
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.0.9
netmask 255.255.255.248
gateway 192.168.0.11
```

- ```service networking restart``` di UML Madiun.
#
- Di UML Router, yakni : Batu, Sby, Kediri , lakukan perintah ```nano /etc/sysctl.conf``` . Kemudian hilangkan tanda pagar sehingga menjadi ```net.ipv4.ip_forward=1```. Kemudian jalankan ```sysctl -p```

#### C) ROUTING DENGAN VLSM
#
![image](https://user-images.githubusercontent.com/71973415/103262686-45569d80-49d8-11eb-8d2d-c9f646d8c93b.png)

- Kemudian tambahkan route pada uml Surabaya. ```nano route.sh``` , kemudian ```bash route.sh```
```
route add -net 10.151.77.112 netmask 255.255.255.248 gw 192.168.0.5
route add -net 192.168.1.0 netmask 255.255.255.0 gw 192.168.0.5
route add -net 192.168.2.0 netmask 255.255.255.0 gw 192.168.0.1
route add -net 192.168.0.8 netmask 255.255.255.248 gw 192.168.0.1
```
#
#### D) Memberikan ip pada subnet SIDOARJO dan GRESIK secara dinamis menggunakan bantuan DHCP SERVER (Selain subnet tersebut menggunakan ip static). Kemudian setting DHCP RELAY pada router yang menghubungkannya
#

- DI BATU, SBY, KEDIRI : ```apt-get install isc-dhcp-relay```

- Kemudian isikan IP Servers dengan IP MOJOKERTO sebagai DHCP Servernya, yaitu ```10.151.77.114```

- ```nano /etc/default/isc-dhcp-relay```. Interfaces yg diisi di relay :
```
Kediri : eth0 eth2
Sby : eth1 eth2
Batu : eth0 eth1 eth2
```
- Restart relay dengan ```service isc-dhcp-relay restart```


- DI MOJOKERTO Install isc-dhcp-server dengan perintah ```apt-get install isc-dhcp-server```.
- Kemudian mengedit file dengan perintah ```nano /etc/default/isc-dhcp-server```. Isikan eth0 pada INTERFACES
- DI  MOJOKERTO ```nano /etc/dhcp/dhcpd.conf```. Kemudian isikan dengan syntax berikut :
```
subnet 10.151.77.112 netmask 255.255.255.248 {
    option routers 10.151.77.115;
    option broadcast-address 10.151.77.119;
}
subnet 192.168.1.0 netmask 255.255.255.0 {
	range 192.168.1.3 192.168.1.213;
    	option routers 192.168.1.2;
    	option broadcast-address 192.168.1.255;
    	option domain-name-servers 10.151.77.113, 202.46.129.2;
    	default-lease-time 600;
    	max-lease-time 7200;
}
subnet 192.168.2.0 netmask 255.255.255.0 {
	range 192.168.2.3 192.168.2.203;
    	option routers 192.168.2.2;
    	option broadcast-address 192.168.2.255;
    	option domain-name-servers 10.151.77.113, 202.46.129.2;
    	default-lease-time 600;
    	max-lease-time 7200;
}
```
- Di mojokerto, restart server dengan ```service isc-dhcp-server restart```

- Untuk testing dilakukan pada 2 UML klien (sidoarjo, gresik), yaitu mengubah file ```nano /etc/network/interfaces``` menjadi:

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp
```

- Kemudian ```service networking restart``` pada klien
- Cek pada klien, dengan ```cat /etc/resolv.conf```
- Lakukan ```ifconfig``` pada klien
#
#
##### 1)  Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi SURABAYA menggunakan iptables, namun Bibah tidak ingin kalian menggunakan MASQUERADE
#
- (atur di uml sby )
- ```iptables -t nat -A POSTROUTING -s 192.168.0.0/16 -o eth0 -j SNAT --to-source 10.151.76.58```
- cek : ```ping its.ac.id``` di semua uml
#
##### 2) Kalian diminta untuk mendrop semua akses SSH dari luar Topologi (UML) Kalian pada server yang memiliki ip DMZ (DHCP dan DNS SERVER) pada SURABAYA demi menjaga keamanan

- (atur di uml sby )
- ```iptables -A FORWARD -p tcp --dport 22 -d 10.151.77.112/29 -i eth0 -j DROP```
- Cek ```nc -l -p 22``` di malang ( sebelumnya install netcat dulu )
- Di putty, ```nc 10.151.77.113 22```
#
##### 3) Karena tim kalian maksimal terdiri dari 3 orang, Bibah meminta kalian untuk membatasi DHCP dan DNS server hanya boleh menerima maksimal 3 koneksi ICMP secara bersamaan yang berasal dari mana saja menggunakan iptables pada masing masing server , selebihnya akan di DROP.

- (atur di uml malang dan mojo )

- ```iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP```
- cek : ping malang atau mojo di 4 tempat

###### 4) Akses dari subnet SIDOARJO hanya diperbolehkan pada pukul 07.00 - 17.00 pada hari Senin sampai Jumat.

- (atur di uml malang )
```iptables -A INPUT -s 192.168.1.0/24 -m time --timestart 07:00 --timestop 17:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT```
```iptables -A INPUT -s 192.168.1.0/24 -m time --timestart 17:01 --timestop 06:59 -j REJECT```
- cek : ping di sidoarjo ke malang

##### 5) Akses dari subnet GRESIK hanya diperbolehkan pada pukul 17.00 hingga pukul 07.00 setiap harinya.

- (atur di uml malang )
```iptables -A INPUT -s 192.168.2.2/25 -m time --timestart 07:01 --timestop 16:59 -j REJECT```
- cek : Ping di gresik ke malang

##### 6) Bibah ingin SURABAYA disetting sehingga setiap request dari client yang mengakses DNS Server akan didistribusikan secara bergantian pada PROBOLINGGO port 80 dan MADIUN port 80

- atur di UML Surabaya
- ```iptables -t nat -A PREROUTING -p tcp -d 10.151.77.113 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 192.168.0.10:80```
- ```iptables -t nat -A PREROUTING -p tcp -d 10.151.77.113 -j DNAT --to-destination 192.168.0.9:80```
- ```iptables -t nat -A POSTROUTING -p tcp -d 192.168.0.10 --dport 80 -j SNAT --to-source 10.151.77.113```
- ```iptables -t nat -A POSTROUTING -p tcp -d 192.168.0.9 --dport 80 -j SNAT --to-source 10.151.77.113```

##### 7)  Bibah ingin agar semua paket didrop oleh firewall (dalam topologi) tercatat dalam log pada setiap UML yang memiliki aturan drop.

( atur di uml sby )
- ```iptables -N LOGGING```
- ```iptables -A FORWARD -j LOGGING ```
- ```iptables -A LOGGING -m limit --limit 2/min -j LOG --log-prefix "IPTables-Dropped: " --log-level 4 ```
- ```iptables -A LOGGING -j DROP```
#
( atur di uml malang)
- ```iptables -N LOGGING``` 
- ```iptables -A INPUT -j LOGGING``` 
- ```iptables -A LOGGING -m limit --limit 2/min -j LOG --log-prefix "IPTables-Dropped: " --log-level 4``` 
- ```iptables -A LOGGING -j DROP```
#
( atur di uml mojokerto)
- ```iptables -N LOGGING``` 
- ```iptables -A INPUT -j LOGGING``` 
- ```iptables -A LOGGING -m limit --limit 2/min -j LOG --log-prefix "IPTables-Dropped: " --log-level 4``` 
- ```iptables -A LOGGING -j DROP```
