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
*(−2 weil: 1× Netzadresse + 1× Broadcast)*

---

### Subnetting – Das 4-Schritte-System

**Schritt 1: Den "Tatort" finden**  
Von links nach rechts schauen – wo steht die erste Zahl die NICHT 255 ist?
```
255.192.0.0     → Tatort: Block 2
255.255.240.0   → Tatort: Block 3
255.255.255.248 → Tatort: Block 4
```

**Schritt 2: Sprungweite berechnen**  
`256 − Tatort-Zahl = Sprungweite`  
Bsp: 256 − 240 = **16** → Sprünge in 16er-Schritten

**Schritt 3: Netzadresse**  
Sprünge durchgehen (0, 16, 32 ...) bis kurz VOR der IP-Zahl.  
- Blöcke **links** vom Tatort → bleiben gleich  
- Blöcke **rechts** vom Tatort → werden **0**

**Schritt 4: Broadcast**  
Direkt die Adresse VOR dem nächsten Sprung.  
- Blöcke **rechts** vom Tatort → werden **255**

---

### Magische Zahlen (häufige Masken)
| Maske | Sprungweite | Schritte |
|---|---|---|
| .128 | 128 | 0, 128 |
| .192 | 64 | 0, 64, 128, 192 |
| .224 | 32 | 0, 32, 64, 96, 128 ... |
| .240 | 16 | 0, 16, 32, 48 ... |
| .248 | 8 | 0, 8, 16, 24 ... |
| .252 | 4 | 0, 4, 8, 12 ... |

> Je höher die Zahl in der Maske → desto kleiner das Netz

---

### Beispiel komplett: 192.168.32.10 / 14

Maske: 255.**252**.0.0 → Tatort: Block 2  
256 − 252 = **4** → Sprünge: 0, 4, 8 ... 164, 168, 172 ...  
168 liegt in Sprung **168**  

- **Netzadresse:** 192.**168**.0.0  
- **Broadcast:** 192.**171**.255.255  
- **Hosts:** 2^(32−14) − 2 = **262142**

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
Client        Server
  → SYN         "Kannst du mich hören?"
  ← SYN-ACK     "Ja! Kannst du mich hören?"
  → ACK         "Ja! Wir können reden."
```

**Verbindungsabbau:**
```
Client        Server
  → FIN         "Ich bin fertig, tschüss."
  ← FIN-ACK     "Ok, ich auch gleich."
  → ACK         "Alles klar, ciao."
```

> **ACK** = Bestätigung ("Angekommen!") · Ohne ACK → Paket wird neu gesendet

**Anwendung:** Webbrowsing · E-Mail · Remote-Zugriff · Dateitransfer

---

### UDP

**Header-Felder:**  
Quell-Port | Ziel-Port | Header-Länge | Prüfsumme

| | |
|---|---|
| ✅ Vorteile | wenig Overhead, geringe Belastung, schnell |
| ❌ Nachteile | unzuverlässig, keine Fehlerkontrolle, kein ACK |

**Anwendung:** VoIP · Online-Gaming · DNS · Videostreaming

---

### TCP vs. UDP

| Merkmal | TCP | UDP |
|---|---|---|
| Zuverlässig | ✅ | ❌ |
| Schnell | ❌ | ✅ |
| Verbindungsaufbau | Ja (Handshake) | Nein |
| Fehlerkorrektur | Ja | Nein |
| ACK | Ja | Nein |
| Overhead | Hoch | Gering |
