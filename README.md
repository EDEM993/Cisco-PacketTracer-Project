# Cisco-PacketTracer-Project
PacketTracer-School-Project

A projektfeladatunk témájának a bank főépületében található irodák hálózatának újratervezését és dokumentálását választottuk. A bank 2025-ben ünnepelte 60. születésnapját, de a mai napig nem található részletes és pontos leírás az épületben használt hálózatokhoz. Ez nagyon megnehezíti az itt dolgozó rendszergazdák dolgát, és a felmerülő problémák kezelése is sokkal hosszadalmasabb emiatt.
A projektünkben az irodákat, az ügyintézőt, a szerverszobát, a várót, a titkárságot és a fő irodát terveztük meg. Az itt található hálózati eszközök és PC-k, laptopok cseréje is része a projektnek, amely ezáltal akár egy kivitelezési ajánlathoz tárgyalási alapként is szolgálhatna.
A tervezéshez a Cisco Packet Tracer szimulációs programot használtuk, amely a hálózati topológiák tervezését segítő és megjelenítő program.

[BEB-Portfólió.pdf](https://github.com/user-attachments/files/26458990/BEB-Portfolio.pdf)

[BEB-Cisco.zip](https://github.com/user-attachments/files/26459854/BEB-Cisco.zip)


<img width="1110" height="569" alt="image" src="https://github.com/user-attachments/assets/0e3010b3-6a9a-4742-988e-488a761fe5ca" />


Technikai Konfiguráció (Ágról ágra):


<details>
<summary>📂 <b>Iroda 1 - Konfiguráció és IP Táblázat</b></summary>

<br>

Az IP címek statikusan vannak kiosztva. A router az iroda 2-ben és iroda 3-ban található routerekkel OSPF protokollon keresztül kommunikál.

**Eszközök és IP kiosztás:**

| Eszköz | IP-cím | Alhálózati maszk | Alapértelmezett átjáró | Név |
| :--- | :--- | :--- | :--- | :--- |
| Router | 192.168.10.1 | 255.255.255.0 | - | iroda1 |
| Router (Serial) | 10.10.10.1 | 255.0.0.0 | - | - |
| Router (Serial) | 30.30.30.2 | 255.0.0.0 | - | - |
| Switch | - | - | - | SwitchI1 |
| Nyomtató | 192.168.10.5 | 255.255.255.0 | 192.168.10.1 | PrinterI1 |
| PC | 192.168.10.2 | 255.255.255.0 | 192.168.10.1 | I1(1) |
| PC | 192.168.10.3 | 255.255.255.0 | 192.168.10.1 | I1(2) |
| PC | 192.168.10.4 | 255.255.255.0 | 192.168.10.1 | I1(3) |

**A helységben lévő router futó config-ja:**
```
hostname iroda1
!
interface FastEthernet0/0
 ip address 192.168.10.1 255.255.255.0
 duplex auto
 speed auto
!
interface Serial0/0/0
 ip address 10.10.10.1 255.0.0.0
!
interface Serial0/0/1
 ip address 30.30.30.2 255.0.0.0
 clock rate 2000000
!
router ospf 1
 log-adjacency-changes
 network 10.10.0.0 0.0.255.255 area 0 
 network 20.20.0.0 0.0.255.255 area 0
 network 30.30.0.0 0.0.255.255 area 0
 network 192.168.10.0 0.0.0.255 area 0
 network 192.168.20.0 0.0.0.255 area 0
 network 192.168.30.0 0.0.0.255 area 0
</details

```





<details>
<summary>📂 <b>Iroda 2 - Konfiguráció és IP Táblázat</b></summary>Az IP címek statikusan vannak kiosztva. A router az iroda 1-ben és iroda 3-ban található routerekkel OSPF protokollon keresztül kommunikál.Eszközök és IP kiosztás:EszközIP-címAlhálózati maszkAlapértelmezett átjáróNévRouter192.168.20.1255.255.255.0-iroda2Router (Serial)20.20.20.2255.0.0.0--Router (Serial)30.30.30.1255.0.0.0--Switch---SwitchI2Nyomtató192.168.20.8255.255.255.0192.168.20.1PrinterI2(1)Nyomtató192.168.20.9255.255.255.0192.168.20.1PrinterI2(2)PC192.168.20.2255.255.255.0192.168.20.1I2(1)PC192.168.20.3255.255.255.0192.168.20.1I2(2)PC192.168.20.4255.255.255.0192.168.20.1I2(3)PC192.168.20.5255.255.255.0192.168.20.1I2(4)PC192.168.20.6255.255.255.0192.168.20.1I2(5)PC192.168.20.7255.255.255.0192.168.20.1I2(6) A helységben lévő router futó config-ja:Plaintexthostname iroda2

 ```
!
interface FastEthernet0/0
 ip address 192.168.20.1 255.255.255.0
 duplex auto
 speed auto
!
interface Serial0/0/0
 ip address 20.20.20.2 255.0.0.0
 clock rate 2000000
!
interface Serial0/0/1
 ip address 30.30.30.1 255.0.0.0
!
router ospf 1
 log-adjacency-changes
 network 10.10.0.0 0.0.255.255 area 0
 network 20.20.0.0 0.0.255.255 area 0
 network 30.30.0.0 0.0.255.255 area 0
 network 192.168.10.0 0.0.0.255 area 0
 network 192.168.20.0 0.0.0.255 area 0
 network 192.168.30.0 0.0.0.255 area 0
</details>


```




<details><summary>📂 <b>Iroda 3 - Konfiguráció és IP Táblázat</b></summary>Az IP címek statikusan vannak kiosztva. A router az iroda 1-ben és iroda 2-ben található routerekkel OSPF protokollon keresztül kommunikál. A router a szerverszobában lévő fő switch-en keresztül van rákötve a hálózatra.Eszközök és IP kiosztás:EszközIP-címAlhálózati maszkAlapértelmezett átjáróNévRouter192.168.30.1255.255.255.0-iroda3Router (FE)100.100.100.3255.255.255.0--Router (Serial)10.10.10.2255.0.0.0--Router (Serial)20.20.20.1255.0.0.0--Switch---SwitchI3Nyomtató192.168.30.4255.255.255.0192.168.30.1PrinterI3PC192.168.30.3255.255.255.0192.168.30.1I3(1)PC192.168.30.2255.255.255.0192.168.30.1I3(2)A helységben lévő router futó config-ja:Plaintexthostname iroda3 
 
```
!
interface FastEthernet0/0
 ip address 192.168.30.1 255.255.255.0
 duplex auto
 speed auto
!
interface FastEthernet0/1
 ip address 100.100.100.3 255.255.255.0
 duplex auto
 speed auto
!
interface Serial0/0/0
 ip address 20.20.20.1 255.0.0.0
!
interface Serial0/0/1
 ip address 10.10.10.2 255.0.0.0
 clock rate 2000000
!
router ospf 1
 log-adjacency-changes
 network 10.10.0.0 0.0.255.255 area 0
 network 20.20.0.0 0.0.255.255 area 0
 network 30.30.0.0 0.0.255.255 area 0
 network 192.168.10.0 0.0.0.255 area 0
 network 192.168.20.0 0.0.0.255 area 0
 network 192.168.30.0 0.0.0.255 area 0
 network 100.100.100.0 0.0.0.255 area 0
</details>


```

<details><summary>📂 <b>Adattároló - Konfiguráció és IP Táblázat</b></summary>Az IP címek statikusan vannak kiosztva. A router a szerverszobában lévő fő switch-en keresztül van rákötve a hálózatra. A helységben lévő számítógépekkel együtt egy zárt vlan alhálózatban vannak.Eszközök és IP kiosztás:EszközIP-címAlhálózati maszkAlapértelmezett átjáróNévRouter172.168.10.1255.255.255.0-iroda2 (adattarolo)Router (FE)100.100.100.2255.255.255.0--Switch---adattarolo_switchPC172.168.10.2255.255.255.0172.168.10.1adat1PC172.168.10.3255.255.255.0172.168.10.1adat2PC172.168.10.4255.255.255.0172.168.10.1adat3PC172.168.10.5255.255.255.0172.168.10.1adat4PC172.168.10.6255.255.255.0172.168.10.1adat5PC172.168.10.7255.255.255.0172.168.10.1adat6A helységben lévő router futó config-ja:Plaintexthostname 
 adattarolo

```
 !
interface FastEthernet0/0
 ip address 172.168.10.1 255.255.255.0
 duplex auto
 speed auto
!
interface FastEthernet0/1
 ip address 100.100.100.2 255.255.255.0
 duplex auto
 speed auto
!
interface Vlan1
 no ip address
 shutdown
!
router ospf 1
 log-adjacency-changes
 network 100.100.100.0 0.0.0.255 area 0
</details>


```

<details><summary>📂 <b>Szerverszoba - Konfiguráció és IP Táblázat</b></summary>Az IP címek statikusan vannak kiosztva. A helységben megtalálható egy fő switch, aminek feladata a bankban lévő főbb routerek összekötése. A backup szerver IPv4-es és IPv6-os címzést is használ. A szerverkezelő laptop IPv6-os címzést használ és tűzfal is megtalálható benne.Eszközök és IP kiosztás:EszközIP-címAlhálózati maszkAlapértelmezett átjáróNévSwitch---Fo_SwitchSzerver100.100.100.1255.255.255.0-Fo_SzerverSzerver (IPv4)200.200.200.1255.255.255.0-Backup_SzerverSzerver (IPv6)2001:DB8:85A3::8A2E:370:733164-Backup_SzerverLaptop (IPv6)2001:DB8:85A3::8A2E:370:7332642001:DB8:85A3::8A2E:370:7331SzerverkezeloA helységben lévő switch futó config-ja:Plaintexthostname Fo_Switch

```
 !
access-list 1 permit 100.100.100.0 0.0.0.255
line con 0
!
line vty 0 4
 access-class 1 in
 login
line vty 5 15
 access-class 1 in
 login
</details>


```

<details><summary>📂 <b>Ügyintéző - Konfiguráció és IP Táblázat</b></summary>Az IP címek dinamikusan vannak kiosztva. A DHCP címkiosztásának feladatát a router végzi el. A router a szerverszobában lévő fő switch-en keresztül van rákötve a hálózatra. A helységben egy WIFI hálózat is megtalálható, ami dinamikusan osztja ki az IP címeket az eszközöknek.Eszközök és IP kiosztás:EszközIP-címAlhálózati maszkAlapértelmezett átjáróNévRouter10.10.10.1255.255.0.0-Router_UgyintezoRouter (FE)192.168.1.1255.255.255.0--Router (Ethernet)100.100.100.4255.255.255.0--Switch---Switch_UgyintezoPC (16 db)DHCP kliens-192.168.1.1Ü1 - Ü16Okostelefon (3 db)DHCP kliens-192.168.200.1Okostelefon 1 - 3Tablet (2 db)DHCP kliens-192.168.200.1Tablet 1 - 2WIFI Router10.10.10.2255.255.0.010.10.10.1Ugyintezo_WIFIA helységben lévő router futó config-ja:Plaintexthostname Router_Ugyintezo

```
 !
ip dhcp pool DHCP
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.1
!
interface FastEthernet0/0
 ip address 10.10.10.1 255.255.0.0
 duplex auto
 speed auto
!
interface FastEthernet0/1
 ip address 192.168.1.1 255.255.255.0
 duplex auto
 speed auto
!
interface Ethernet0/0/0
 ip address 100.100.100.4 255.255.255.0
 duplex auto
 speed auto
!
router ospf 1
 log-adjacency-changes
 network 100.100.100.0 0.0.0.255 area 0
</details>

```

<details><summary>📂 <b>Bejárat (VPN) - Konfiguráció és IP Táblázat</b></summary>Az IP címek statikusan vannak kiosztva. A helységben a két ATM (PC) között VPN kapcsolat található.Eszközök és IP kiosztás:EszközIP-címAlhálózati maszkAlapértelmezett átjáróNévRouter192.168.1.1255.255.255.0-VPN_Router_1Router (FE)1.0.0.2255.0.0.0--Router1.0.0.1255.0.0.0-VPN_Router_2Router (FE)2.0.0.1255.0.0.0--Router2.0.0.2255.0.0.0-VPN_Router_3Router (FE)192.168.2.1255.255.255.0--PC192.168.1.2255.255.255.0192.168.1.1ATM 1PC192.168.2.2255.255.255.0192.168.2.1ATM 2A helységben lévő routerek futó config-ja:Plaintext! VPN_Router_1:
hostname VPN_Router_1

```
 !
interface Tunnel1
 ip address 172.16.1.1 255.255.0.0
 mtu 1476
 tunnel source FastEthernet0/1
 tunnel destination 2.0.0.2
!
interface FastEthernet0/0
 ip address 192.168.1.1 255.255.255.0
 duplex auto
 speed auto
!
interface FastEthernet0/1
 ip address 1.0.0.2 255.0.0.0
 duplex auto
 speed auto
!
interface Vlan1
 no ip address
 shutdown
!
ip classless
ip route 0.0.0.0 0.0.0.0 1.0.0.1 
ip route 192.168.2.0 255.255.255.0 172.16.1.2

! VPN_Router_2:
hostname VPN_Router_2
!
interface FastEthernet0/0
 ip address 1.0.0.1 255.0.0.0
 duplex auto
 speed auto
!
interface FastEthernet0/1
 ip address 2.0.0.1 255.0.0.0
 duplex auto
 speed auto

! VPN_Router_3:
hostname VPN_Router_3
!
interface Tunnel2
 ip address 172.16.1.2 255.255.0.0
 mtu 1476
 tunnel source FastEthernet0/1
 tunnel destination 1.0.0.2
!
interface FastEthernet0/0
 ip address 192.168.2.1 255.255.255.0
 duplex auto
 speed auto
!
interface FastEthernet0/1
 ip address 2.0.0.2 255.0.0.0
 duplex auto
 speed auto
!
ip classless
ip route 0.0.0.0 0.0.0.0 2.0.0.1 
ip route 192.168.1.0 255.255.255.0 172.16.2.2

```

</details><details><summary>📂 <b>Fő iroda - Konfiguráció és IP Táblázat</b></summary>Az IP címek statikusan vannak kiosztva. A router a titkárságban található routerrel RIP protokollon keresztül kommunikál. A helységben egy WIFI hálózat is megtalálható, ami dinamikusan osztja ki az IP címeket az eszközöknek.Eszközök és IP kiosztás:EszközIP-címAlhálózati maszkAlapértelmezett átjáróNévRouter172.16.1.1255.255.0.0-Router_FoirodaRouter (FE)192.168.1.1255.255.255.0--Router (Serial)10.10.10.2255.255.0.0--Switch---Switch_FoirodaPC172.16.1.2255.255.0.0172.16.1.1Foiroda_PCLaptop172.16.1.3255.255.0.0172.16.1.1Foiroda_LaptopNyomtató172.16.1.4255.255.0.0172.16.1.1Foiroda_NyomtatoIP Telefon---Telefon_FoirodaOkostelefonDHCP kliens-192.168.50.1Okostelefon 4TabletDHCP kliens-192.168.50.1Tablet 3WIFI Router192.168.1.2255.255.255.0192.168.1.1Ugyintezo_WIFIA helységben lévő router futó config-ja:Plaintexthostname Router_Foiroda

```
 !
interface FastEthernet0/0
 ip address 172.16.1.1 255.255.0.0
 duplex auto
 speed auto
!
interface FastEthernet0/1
 ip address 192.168.1.1 255.255.255.0
 duplex auto
 speed auto
!
interface Serial0/0/0
 ip address 10.10.10.2 255.255.0.0
 clock rate 2000000
!
router rip
 network 10.0.0.0
 network 172.16.0.0
 network 192.168.1.0
 network 192.168.10.0

```
</details><details><summary>📂 <b>Titkárság - IP Táblázat</b></summary>Az IP címek statikusan vannak kiosztva. A router a fő irodában található routerrel RIP protokollon keresztül kommunikál, valamint a router a szerverszobában lévő fő switch-en keresztül van rákötve a hálózatra. A helységben egy PC is megtalálható, ami az IP Telefonon keresztül van rákötve a hálózatra.Eszközök és IP kiosztás 
 
```
:EszközIP-címAlhálózati maszkAlapértelmezett átjáróNévRouter192.168.10.1255.255.255.0-Router_TitkarRouter (FE)100.100.100.5255.255.255.0--Router (Serial)10.10.10.1255.255.0.0--Switch---Switch_TitkarPC192.168.10.5255.255.255.0192.168.10.1PC_TitkarLaptop192.168.10.3255.255.255.0192.168.10.1Laptop_TitkarNyomtató192.168.10.4255.255.255.0192.168.10.1Nyomtato_TitkarIP Telefon---Telefon_Titkar
</details>

```






















 network 192.168.10.0 0.0.0.255 area 0
 network 192.168.20.0 0.0.0.255 area 0
 network 192.168.30.0 0.0.0.255 area 0
