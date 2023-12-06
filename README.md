# Jarkom-Modul-4-E23-2023

1. Soal shift dikerjakan pada Cisco Packet Tracer dan GNS3 menggunakan metode perhitungan CLASSLESS yang berbeda.
Keterangan: Bila di CPT menggunakan VLSM, maka di GNS3 menggunakan CIDR atau sebaliknya
2. Jika tidak ada pemberitahuan revisi soal dari asisten, berarti semua soal BERSIFAT BENAR dan DAPAT DIKERJAKAN.
3. Untuk di GNS3 CLOUD merupakan NAT1 jangan sampai salah agar bisa terkoneksi internet.
4. Pembagian IP menggunakan Prefix IP yang telah ditentukan pada modul pengenalan
5. Pembagian IP dan routing harus SE-EFISIEN MUNGKIN.


---
### Penyelesaian
---
Untuk menyelesaikan praktikum modul ini saya memilih mengerjakannya dengan membaginya menjadi:
- VLSM : Menggunakan Cisco Packet Tracer (CPT)
- CIDR : Menggunakan GNS3

Sebelumnya dilakukan terlebih dahulu pembagian subnet (rute) sebagai berikut:

![bagi](img/bagi.png)

![rute](img/rute.png)

Dari pembagian subnet ini nantinya akan ditemukan pembagian ip yang sesuai menggunakan metode classless VLSM dan CIDR Tree. Perhitungan ip sudah termasuk ip router. Pembagian ip digunakan untuk melakukan subnetting pada topologi, setelah subnetting berhasil langkah terakhir adalah melakukan routing.

---
### VLSM (CPT)
---

Berikut ini adalah VLSM tree yang telah dibuat :

![tree](img/treevlsm.jpg)

- Karena pada pembagian subnet tercatat total ip adalah 4255 dan netmask yang cukup untuk menampungnya adalah /19 yang mana mampu menampung ip sebanyak 8190.
- Root dari tree adalah netmask /19 dengan ip yang dimulai dari 10.48.0.0.
- Pada pembuatan tree ini saya menggunakan penambahan dari ip terkecil, Kaki kiri dari tree akan selalu menunjukkan awal mula dari ip yang tersedia, sedangkan kaki kanan adalah ip setelah ip kaki kiri, pada kaki kiri juga saya berikan batas atas atau broadcast address dari ip dengan netmask tersebut untuk mempermudah penentuan ip di kaki kanan tree
- Iterasi dilakukan terus menerus dari netmask /19 hingga /30.

Sehingga diperoleh pembagian ip VLSM:

![vlsm](img/vlsm.png)

Untuk isi config pembagian ip diset seperti ini:
- Router memliki IP NID + 1
- Host / Client memiliki IP Rourter + 1 atau IP Client sesubnet + 1
- Host / Client memiliki gateway sesuai IP router dalam subnet mereka
- 1 router bisa memiliki beberapa IP karena dalam 1 router dapat menangani beberapa ethernet interface / subnet

Karena config semuanya kurang lebih mirip, jadi dibawah ini diberi contoh assign IP Router dan Client dalam 1 Subnet saja:

- Himmel :

![h1](img/himmel1.png)

![h2](img/himmel2.png)

- SchwerMountains :

![s1](img/schwer.png)

- Jika config sudah sesuai maka dalam 1 Subnet ini semuanya pasti bisa saling melakukan ping
- Konfigurasi IP ini dilakukan ke SETIAP subnet nya sebagaimana pembagian IP di sheet perhitungan.

Berikut merupakan config selengkapnya dari setiap node :

- RohrRoad

![s1](img/rohrroad.png)

- Flamme

![s1](img/flamme.png)

- SchwerMountains

![s1](img/schwerm.png)

- Himmel

![s1](img/himmel.png)

- Frieren

![s1](img/frieren.png)

- LakeKoridor

![s1](img/lake.png)

- Aura

![s1](img/aura.png)

- Denken

![s1](img/denken.png)

- RoyalCapital

![s1](img/royalcapital.png)

- WilleRegion

![s1](img/willeregion.png)

- Eisen

![s1](img/eisen.png)

- Richter

![s1](img/richter.png)

- Revolte

![s1](img/revolte.png)

- Stark

![s1](img/stark.png)

- Lugner

![s1](img/lugner.png)

- TurkRegion

![s1](img/turkregion.png)

- GlobeForest

![s1](img/globeforest.png)

- Linie

![s1](img/linie.png)

- GranzChannel

![s1](img/granzchannel.png)

- Lawine

![s1](img/lawine.png)

- BredtRegion

![s1](img/bredtregion.png)

- Sein

![s1](img/sein.png)

- Heiter

![s1](img/heiter.png)

- RiegelCanyon

![s1](img/riegelcanyon.png)

- LaubHills

![s1](img/laub.png)

- AppetitRegion

![s1](img/appetit.png)

- LakeKorridor

![s1](img/lake.png)


**ROUTING**

Untuk routing dilakukan dengan cara beberapa tahap:
- Routing dilakukan dengan cara static dimana next hop dari routing adalah adjacent router terdekat dengan subnet yang ingin dituju, semisal aura ingin berkenalan dengan subnet a10 maka NID dan netmask diisi milik a10 dan next-hop nya adalah IP Denken yang mengarah ke aura.
- Pada static routing juga dibutuhkan default routing agar router dapat mengirimkan paket sesuai dengan tujuan.
- Kemudian untuk setiap router yang terhubung dengan router lain (nexthop untuk berkenalan lebih dari 1 hop) yang memiliki host/client perlu mengenali subnet mereka juga
- Contoh:
    - Flamme harus berkenalan dengan subnet a1, a3, a4, a5
    - Frieren harus berkenalan dengan subnet a1, a2, a3, a4, a5
    - Lawine harus berkenalan dengan subnet a18 dan a19
    - dst.

- Binding everywhere dari setiap router cukup 1 saja yang mengarah ke router aura / terdekat dengan aura, hal ini dilakukan untuk efisiensi routing (100% success)
- Jika aura sudah disetup sebagaimana pengaturan routing di atas maka otomatis semua subnet bisa saling mengenal via aura

Untuk melihat CONFIG SELENGKAPNYA sebagai berikut :

- Fern

  ![s1](img/fern2.png)

- Flamme

  ![s1](img/flamme2.png)

- Himmel

  ![s1](img/himmel5.png)

- Frieren

  ![s1](img/frieren2.png)

- Aura

  ![s1](img/aura2.png)

- Denken

  ![s1](img/denken2.png)

- Eisen

  ![s1](img/eisen2.png)

- Lugner

  ![s1](img/lugner2.png)

- Linie

  ![s1](img/linie2.png)

- Lawine

  ![s1](img/lawine2.png)

- Heiter

  ![s1](img/heiter2.png)


**HASIL PING**
![s1](img/hasil.png)



### CIDR

# Topologi GNS
![gns](img/gns.jpg)

Prefix IP

```
10.48
```

### Penggabungan IP

#### Rute
![subA](img/subA.jpg)

![rute](img/rute.jpg)


#### Penggabungan I 
![subB](img/subB.jpg)

![gabB](img/gabB.jpg)

#### Penggabungan II
![subC](img/subC.jpg)

![gabC](img/gabC.jpg)

#### Penggabungan III
![subD](img/subD.jpg)

![gabD](img/gabD.jpg)  

#### Penggabungan IV
![subE](img/subE.jpg)

![gabE](img/gabE.jpg)

#### Penggabungan V
![subF](img/subF.jpg)

![gabF](img/gabF.jpg)

#### Penggabungan VI
![subB](img/subG.jpg)

![gabB](img/gabG.jpg) 

### Pembagian IP-CIDR
![IPCIDR](img/IPCIDR.jpg)



### Konfigurasi
Berikut adalah konfigurasi jaringan tiap node pada topologi.
- Aura
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.48.65.1
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 10.48.66.34
	netmask 255.255.255.252

auto eth3
iface eth3 inet static
	address 10.48.192.9
	netmask 255.255.255.252
```

- Denken
```
auto eth0
iface eth0 inet static
	address 10.48.65.2
	netmask 255.255.255.252

auto eth1
iface eth1 inet static
	address 10.48.64.1
	netmask 255.255.255.0
```

- RoyalCapital (63 host)
```
auto eth0
iface eth0 inet static
	address 10.48.64.64
	netmask 255.255.255.0
	gateway 10.48.64.1
```
- WilleRegion (63 host)
  
```
auto eth0
iface eth0 inet static
	address 10.48.64.65
	netmask 255.255.255.0
	gateway 10.48.64.1
```

- Frieren
```
auto eth0
iface eth0 inet static
	address 10.48.66.33
	netmask 255.255.255.252

auto eth1
iface eth1 inet static
	address 10.48.16.2
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 10.48.66.1
	netmask 255.255.255.224
```

- LakeKorridor (24 host)
```
auto eth0
iface eth0 inet static
	address 10.48.66.3
	netmask 255.255.255.224
	gateway 10.48.66.1
```

- Flamme
```
auto eth0
iface eth0 inet static
	address 10.48.16.1
	netmask 255.255.255.252

auto eth1
iface eth1 inet static
	address 10.48.8.2
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 10.48.36.9
	netmask 255.255.255.252

auto eth3
iface eth3 inet static
	address 10.48.32.1
	netmask 255.255.252.0
```
- Fern
```
auto eth0
iface eth0 inet static
	address 10.48.8.1
	netmask 255.255.255.252

auto eth1
iface eth1 inet static
	address 10.48.0.1
	netmask 255.255.248.0
```

- LaubHills (397 host)
```
auto eth0
iface eth0 inet static
	address 10.48.0.2
	netmask 255.255.248.0
	gateway 10.48.0.1
```

- AppetitRegion (625 host)
```
auto eth0
iface eth0 inet static
	address 10.48.3.0
	netmask 255.255.248.0
	gateway 10.48.0.1
```

- RohrRoad (1000 host)
```
auto eth0
iface eth0 inet static
	address 10.48.32.2
	netmask 255.255.252.0
	gateway 10.48.32.1
```

- Himmel
```
auto eth0
iface eth0 inet static
	address 10.48.36.10
	netmask 255.255.255.252

auto eth1
iface eth1 inet static
	address 10.48.36.1
	netmask 255.255.255.248
```
- Eisen
```
auto eth0
iface eth0 inet static
	address 10.48.192.10
	netmask 255.255.255.252

auto eth1
iface eth1 inet static
	address 10.48.146.1
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 10.48.168.1
	netmask 255.255.255.252

auto eth3
iface eth3 inet static
	address 10.48.176.1
	netmask 255.255.255.252

auto eth4
iface eth4 inet static
	address 10.48.192.1
	netmask 255.255.255.248
```
- Stark
```
auto eth0
iface eth0 inet static
	address 10.48.176.2
	netmask 255.255.255.252
	gateway 10.48.176.1
```
- Lugner
```
auto eth0
iface eth0 inet static
	address 10.48.168.2
	netmask 255.255.255.252

auto eth1
iface eth1 inet static
	address 10.48.160.1
	netmask 255.255.252.0

auto eth2
iface eth2 inet static
	address 10.48.164.1
	netmask 255.255.255.0
```
- TurkRegion (1000 host)
```
auto eth0
iface eth0 inet static
	address 10.48.160.2
	netmask 255.255.252.0
	gateway 10.48.160.1
```
- GrobeForest (250 host)
```
auto eth0
iface eth0 inet static
	address 10.48.164.2
	netmask 255.255.252.0
	gateway 10.48.164.1
```

- Richter
```
auto eth0
iface eth0 inet static
	address 10.48.192.2
	netmask 255.255.255.248
	gateway 10.48.192.1
```
- Revolte
```
auto eth0
iface eth0 inet static
	address 10.48.192.3
	netmask 255.255.255.248
	gateway 10.48.192.1
```

- Linie
```
auto eth0
iface eth0 inet static
	address 10.48.146.2
	netmask 255.255.255.252

auto eth1
iface eth1 inet static
	address 10.48.136.1
	netmask 255.255.252.0

auto eth2
iface eth2 inet static
	address 10.48.144.1
	netmask 255.255.254.0
```
- Lawine
```
auto eth0
iface eth0 inet static
	address 10.48.136.2
	netmask 255.255.255.252

auto eth1
iface eth1 inet static
	address 10.48.132.1
	netmask 255.255.255.192
```
- BredtRegion (29 host)
```
auto eth0
iface eth0 inet static
	address 10.48.132.3
	netmask 255.255.255.192
	gateway 10.48.132.1
```
- Heiter
```
auto eth0
iface eth0 inet static
	address 10.48.132.2
	netmask 255.255.255.192

auto eth1
iface eth1 inet static
	address 10.48.128.1
	netmask 255.255.252.0
```
- RiegelCanyon (510 host)
```
auto eth0
iface eth0 inet static
	address 10.48.128.3
	netmask 255.255.252.0
	gateway 10.48.128.1
```

- Sein
```
auto eth0
iface eth0 inet static
	address 10.48.128.2
	netmask 255.255.252.0
	gateway 10.48.128.1
```
- GranzChannel (254 host)
```
auto eth0
iface eth0 inet static
	address 10.48.144.2
	netmask 255.255.254.0
	gateway 10.48.144.1
```


### Routing tiap node;
- Aura
```
# kiri 
route add -net 10.48.0.0 netmask 255.255.248.0 gw 10.48.66.33 
route add -net 10.48.8.0 netmask 255.255.255.252 gw 10.48.66.33 
route add -net 10.48.32.0 netmask 255.255.252.0 gw 10.48.66.33 
route add -net 10.48.36.8 netmask 255.255.255.252 gw 10.48.66.33 
route add -net 10.48.36.0 netmask 255.255.255.248 gw 10.48.66.33 
route add -net 10.48.16.0 netmask 255.255.255.252 gw 10.48.66.33 
route add -net 10.48.66.0 netmask 255.255.255.224 gw 10.48.66.33 

# kanan 
route add -net 10.48.64.0 netmask 255.255.255.0 gw 10.48.65.2 

# bawah
route add -net 10.48.176.0 netmask 255.255.255.252 gw 10.48.192.10 
route add -net 10.48.192.0 netmask 255.255.255.248 gw 10.48.192.10
route add -net 10.48.168.0 netmask 255.255.255.252 gw 10.48.192.10 
route add -net 10.48.160.0 netmask 255.255.252.0 gw 10.48.192.10 
route add -net 10.48.164.0 netmask 255.255.255.0 gw 10.48.192.10 
route add -net 10.48.146.0 netmask 255.255.255.252 gw 10.48.192.10
route add -net 10.48.136.0 netmask 255.255.255.252 gw 10.48.192.10 
route add -net 10.48.132.0 netmask 255.255.255.192 gw 10.48.192.10 
route add -net 10.48.128.0 netmask 255.255.252.0 gw 10.48.192.10 
route add -net 10.48.144.0 netmask 255.255.254.0 gw 10.48.192.10
```
- Frieren
```
# semua
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.48.66.34

route add -net 10.48.0.0 netmask 255.255.248.0 gw 10.48.16.1 
route add -net 10.48.8.0 netmask 255.255.255.252 gw 10.48.16.1
route add -net 10.48.32.0 netmask 255.255.252.0 gw 10.48.16.1 
route add -net 10.48.36.8 netmask 255.255.255.252 gw 10.48.16.1 
route add -net 10.48.36.0 netmask 255.255.255.248 gw 10.48.16.1 
```
- Flamme
```
# semua
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.48.16.2

route add -net 10.48.0.0  netmask 255.255.248.0 gw 10.48.8.1
route add -net 10.48.36.0 netmask 255.255.255.248 gw 10.48.36.10 
```
- Fern
```
# semua
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.48.8.2
```
- Himmel
```
# semua
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.48.36.9
```
- Denken
```
# semua
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.48.65.1
```
- Eisen
```
# semua
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.48.192.9

route add -net 10.48.160.0 netmask 255.255.252.0 gw 10.48.168.2 
route add -net 10.48.164.0 netmask 255.255.255.0 gw 10.48.168.2 
route add -net 10.48.136.0 netmask 255.255.255.252 gw 10.48.146.2 
route add -net 10.48.132.0 netmask 255.255.255.192 gw 10.48.146.2 
route add -net 10.48.128.0 netmask 255.255.252.0 gw 10.48.146.2 
route add -net 10.48.144.0 netmask 255.255.254.0 gw 10.48.146.2 
```
- Lugner
```
# semua
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.48.168.1
```
- Linie
```
# semua
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.48.146.1

route add -net 10.48.132.0 netmask 255.255.255.192 gw 10.48.136.2
route add -net 10.48.128.0 netmask 255.255.252.0 gw 10.48.136.2 
```
- Lawine
```
# semua
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.48.136.1

route add -net 10.48.128.0 netmask 255.255.252.0 gw 10.48.132.2 
```
- Heiter
```
# semua
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.48.132.1
```

### Testing
Command
```
route -n
```

```
ping 10.48.132.2
```

