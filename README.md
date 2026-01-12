# netpractice - Network Protokolleri ve IP Subnetting

## 📚 Proje Açıklaması

**netpractice**, OSI modelini, TCP/IP protokollerini ve IP subnetting'i öğreten etkileşimli bir network eğitim projesidir. Sanal ağ topolojileri kurarak network'ün nasıl çalıştığını pratik olarak öğrenirsiniz.

## 🎯 Network Temelleri

### OSI Model (7 Layers)

```
Layer 7: Application    (HTTP, FTP, SSH, DNS)
Layer 6: Presentation   (SSL/TLS, Encryption)
Layer 5: Session        (Session management)
Layer 4: Transport      (TCP, UDP)
Layer 3: Network        (IP routing)
Layer 2: Data Link      (Ethernet, MAC)
Layer 1: Physical       (Cables, signals)
```

### TCP/IP Stack

```
Application: HTTP, HTTPS, SSH, FTP, DNS, SMTP
Transport:   TCP (connection-based), UDP (connectionless)
Internet:    IP (IPv4, IPv6), ICMP, ARP
Link Layer:  Ethernet, Wi-Fi
```

## 📖 IP Adresler ve Subnetting

### IPv4 Adresi Yapısı

```
192.168.1.100

192    .    168    .    1     .    100
Octet1 .  Octet2  .  Octet3  .  Octet4
(0-255) . (0-255) . (0-255) . (0-255)
```

### Subnet Mask

```
Subnet Mask: 255.255.255.0
Binary:      11111111.11111111.11111111.00000000
Network:     192.168.1.0
Broadcast:   192.168.1.255
Hosts:       192.168.1.1 - 192.168.1.254 (254 adresi)

CIDR Notation:
192.168.1.0/24   (1 ile başlayan 24 bit)
/24 = 255.255.255.0
/16 = 255.255.0.0
/8  = 255.0.0.0
```

### Subnetting Örneği

```
Network:      192.168.1.0/24
Netmask:      255.255.255.0
Hosts:        192.168.1.1 - 192.168.1.254
Broadcast:    192.168.1.255
Total IPs:    256

/25 ile subnet divided:
- 192.168.1.0/25     (1-126)
- 192.168.1.128/25   (129-254)
```

## 🛠️ Network Protokolleri

### ARP (Address Resolution Protocol)

```
MAC adresi bulma:
PC A: "192.168.1.100 IP'si hangi MAC'e ait?"
Switch: "Tüm portlara broadcast gönder"
PC B: "O benim! MAC adresim XX:XX:XX:XX:XX:XX"
PC A: "Teşekkürler, ARP cache'e kaydediyorum"
```

**ARP Tablo:**
```bash
ip neigh show
# 192.168.1.1 dev eth0 lladdr a4:11:22:33:44:55 REACHABLE
```

### ICMP (Internet Control Message Protocol)

```
PING örneği:
1. ICMP Echo Request gönder
2. Hedef ICMP Echo Reply döndür
3. Time bilgisi göster

TTL (Time To Live):
- Her router'dan 1 azalır
- 0 olunca packet drop olur
- Infinite loop'tan korur
```

### TCP vs UDP

**TCP (Transmission Control Protocol)**
```
- Connection-based
- Reliable delivery (retry mekanizması)
- In-order delivery
- Flow control
- Örnek: HTTP, HTTPS, SSH, FTP
```

**UDP (User Datagram Protocol)**
```
- Connectionless
- Unreliable (best effort)
- No ordering guarantee
- Low overhead (fast)
- Örnek: DNS, VOIP, Online games
```

## 🔧 Pratik Örnekler

### Network Configuration (Linux)

```bash
# IP adresi görmek
ip addr show
# veya
ifconfig

# Route tablolarını görme
ip route show
# veya
route -n

# Gateway'i kontrol et
netstat -r

# DNS servers görmek
cat /etc/resolv.conf
# veya
systemctl status systemd-resolved
```

### Network Troubleshooting

```bash
# Bağlantı kontrolü (ICMP)
ping 8.8.8.8

# DNS çözümleme
nslookup google.com
dig google.com
host google.com

# Port taraması
nc -zv host port
# veya
netstat -tlnp

# Trace route (hop-by-hop)
traceroute google.com
# veya
tracert google.com (Windows)

# Network interface istatistikleri
ip -s link show
```

### Static IP Konfigürasyonu (Debian)

```bash
sudo nano /etc/network/interfaces

# Örnek:
auto eth0
iface eth0 inet static
    address 192.168.1.100
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-nameservers 8.8.8.8 8.8.4.4
```

## 📚 Öğrenme Çıktıları

✅ OSI model anlaşıldı  
✅ TCP/IP stack'i mastered  
✅ IP adresleme ve subnetting öğrenildi  
✅ ARP, ICMP, TCP, UDP protokolleri anlaşıldı  
✅ Network troubleshooting becerileri geliştirildi  
✅ Linux network configuration yapıldı  
✅ Routing ve forwarding konsepti öğrenildi  

## 🎯 Önemli Kavramlar

### MAC Adresi
```
Format: XX:XX:XX:XX:XX:XX (48 bit)
Örnek: a4:11:22:33:44:55

First 3 octets: OUI (Organizationally Unique Identifier)
Last 3 octets: Network Interface Controller (NIC)

Scope: Lokal network içinde (IP gibi global değil)
```

### Gateway
```
Router'ın IP adresi
Paketleri başka network'e yönlendirir

Örnek network: 192.168.1.0/24
Gateway: 192.168.1.1 (genellikle)
```

### Default Route
```
IP route: 0.0.0.0/0 via 192.168.1.1
Başka route'ta eşleşmeyen tüm traffic gateway'e gider
```

## 🚀 Network Topoloji Örnekleri

### Star Topology (En Yaygın)
```
    Router (Gateway)
    /    |    \
   PC1  PC2  PC3
```

### Switch'li Network
```
Router -- Switch -- PC1
         |      -- PC2
         |      -- PC3
```

### Multi-subnet Network
```
Internet -- Router -- Switch -- Subnet1 (192.168.1.0/24)
                   |         
                   ---- Switch -- Subnet2 (192.168.2.0/24)
```

## 💡 Pratik Laboratuvar Egzersizleri

### Örnek 1: Simple Network

```
PC A: 192.168.1.10/24
PC B: 192.168.1.20/24
Switch: Onları bağla

Testle:
ping 192.168.1.20 (A'dan)
-> PC B'den reply gelmelidir
```

### Örnek 2: Two Subnets

```
Subnet1: 192.168.1.0/24 (PC A)
Subnet2: 192.168.2.0/24 (PC B)
Router'ı ortada bağla

PC A'dan PC B'ye:
ping 192.168.2.20
-> Router aracılığıyla ulaşmalı
```

### Örnek 3: Internet Connection

```
ISP -- Modem (Gateway)
       |
       Router
       |
       Computers

Internet'e çıkış:
route: 0.0.0.0/0 via [Modem IP]
```

## 📊 Subnet Tablosu

```
/32 : 1 host          (256^4 / 256^4 = 1)
/31 : 2 hosts         (256^4 / 256^3 = 256)
/30 : 4 hosts         (256^4 / 256^2 = 65536)
/29 : 8 hosts
/28 : 16 hosts
/27 : 32 hosts
/26 : 64 hosts
/25 : 128 hosts
/24 : 256 hosts       (Sık kullanılan)
/23 : 512 hosts
/22 : 1024 hosts
/21 : 2048 hosts
/20 : 4096 hosts
/19 : 8192 hosts
/16 : 65536 hosts
```

## 📝 Önemli Portlar

```
22   : SSH
25   : SMTP
53   : DNS
80   : HTTP
110  : POP3
143  : IMAP
443  : HTTPS
465  : SMTP-TLS
993  : IMAP-TLS
3306 : MySQL
5432 : PostgreSQL
```

## 🔧 Network Debugging Toolları

```bash
# Packet capture
sudo tcpdump -i eth0 -n

# Network statistics
netstat -an
ss -an  (modern)

# DNS queries
dig @8.8.8.8 google.com

# HTTP request tracing
curl -v https://example.com

# Throughput testing
iperf3
```

## 💡 Key Learning Points

1. **OSI Model**: 7 layer'ın ne işe yaradığını anlamak
2. **IP Subnetting**: Network'leri böl ve yönet
3. **Routing**: Paketler nasıl hedefe ulaşır
4. **Protocols**: TCP, UDP, ICMP, ARP
5. **Network Tools**: Troubleshooting ve monitoring
6. **Security**: Firewall, NAT, VPN basics

Bu proje, network yönetimi ve Linux system administration temelleri için kritik bilgi sağlar.
