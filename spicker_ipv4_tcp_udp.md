# Spicker – IPv4 & TCP/UDP

---

## SEITE 1 – IPv4 & Subnetting

### Wichtige IPs
| Adresse | Bedeutung |
|---|---|
| 10.0.0.0/8 | Privates Netzwerk |
| 127.0.0.0/8 | Localhost |
| 172.16.0.0/12 | Privat |
| 192.168.0.0/16 | Privat |
| 255.255.255.255/32 | Limited Broadcast |

### IP-Klassen
| Klasse | Bereich |
|---|---|
| A | 0.0.0.0 – 127.255.255.255 |
| B | 128.0.0.0 – 191.255.255.255 |
| C | 192.0.0.0 – 223.255.255.255 |
| D + E | 224.0.0.0 – 255.255.255.255 |

**IPv4:** OSI Layer 3 · 32 Bit · physisches/virtuelles Interface  
**/xx** = Anzahl der 1en in der Subnetzmaske

---

### Subnetting – Hosts berechnen

**Formel:** `Hosts = 2^(32 - Präfix) - 2`

**Bsp. /16:**  
192.168.32.10/16 → 2^(32-16) - 2 = **65534 Hosts**  
Netzadresse (Hostbits = 0): **192.168.0.0**  
Broadcast (Hostbits = 1): **192.168.255.255**

**Bsp. /14 (unvollständiger Block):**  
192.168.32.10/14 → Maske: 255.252.0.0  
255 - 252 = 3 → Blöcke: 0–3, 4–7, 8–11, 12–15 ...  
168 liegt in Block **168–171**  
→ Netzadresse: **192.168.0.0** | Broadcast: **192.171.255.255**

**Binär-Beispiel (/16):**
```
IP:    11000000.10101000.00100000.00001010
Maske: 11111111.11111111.00000000.00000000
Netz:  11000000.10101000.00000000.00000000
```

---

## SEITE 2 – TCP & UDP / Transportprotokolle

### Übertragungsarten
| Begriff | Bedeutung |
|---|---|
| Unicast | 1 zu 1 |
| Multicast | 1 zu mehreren |
| Broadcast | 1 zu allen |

**Transportprotokolle** = Layer 4 · verbinden Applikation & Interface via Ports

---

### TCP

**Header-Felder:**  
Source-Port | Dest-Port | Sequence-Nr. | Acknowledgement-Nr. | Controlflags

| | |
|---|---|
| ✅ Vorteile | Fehlerkorrektur, erneutes Senden, zuverlässig |
| ❌ Nachteile | hoher Overhead, komplexer Header |

**Verbindungsaufbau (3-Way-Handshake):**
```
Client      Server
  → SYN
  ← SYN-ACK
  → ACK
```

**Verbindungsabbau:**
```
Client      Server
  → FIN
  ← FIN-ACK
  → ACK
```

**Anwendung:** Webbrowsing · E-Mail · Remote-Zugriff · Dateitransfer

---

### UDP

**Header-Felder:**  
Quell-Port | Ziel-Port | Header-Länge | Prüfsumme

| | |
|---|---|
| ✅ Vorteile | wenig Overhead, geringe Belastung, schnell |
| ❌ Nachteile | unzuverlässig, keine Fehlerkontrolle |

**Anwendung:** VoIP · Online-Gaming · DNS · Videostreaming

---

### TCP vs. UDP

| Merkmal | TCP | UDP |
|---|---|---|
| Zuverlässig | ✅ | ❌ |
| Schnell | ❌ | ✅ |
| Verbindungsaufbau | Ja | Nein |
| Fehlerkorrektur | Ja | Nein |
| Overhead | Hoch | Gering |
