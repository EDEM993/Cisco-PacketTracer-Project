# Cisco-PacketTracer-Project
PacketTracer-School-Project

A projektfeladatunk témájának a bank főépületében található irodák hálózatának újratervezését és dokumentálását választottuk. A bank 2025-ben ünnepelte 60. születésnapját, de a mai napig nem található részletes és pontos leírás az épületben használt hálózatokhoz. Ez nagyon megnehezíti az itt dolgozó rendszergazdák dolgát, és a felmerülő problémák kezelése is sokkal hosszadalmasabb emiatt.
A projektünkben az irodákat, az ügyintézőt, a szerverszobát, a várót, a titkárságot és a fő irodát terveztük meg. Az itt található hálózati eszközök és PC-k, laptopok cseréje is része a projektnek, amely ezáltal akár egy kivitelezési ajánlathoz tárgyalási alapként is szolgálhatna.
A tervezéshez a Cisco Packet Tracer szimulációs programot használtuk, amely a hálózati topológiák tervezését segítő és megjelenítő program.

[BEB-Portfólió.pdf](https://github.com/user-attachments/files/26458990/BEB-Portfolio.pdf)


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
```text
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
</details>





















 network 192.168.10.0 0.0.0.255 area 0
 network 192.168.20.0 0.0.0.255 area 0
 network 192.168.30.0 0.0.0.255 area 0
