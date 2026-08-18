# IPv6 Lab — 3 Routers, Dual Serial Links

## Opis

Własne ćwiczenie adresacji IPv6, wykonane poza kursem CCNA, w oparciu
o zdobytą wiedzę z VLSM i adresacji IPv6.

## Topologia

![Topologia sieci](topology.png)

- 3 routery (Router_1, Router_2, Router_3)
- Router_1 połączony łączem Serial z Router_2 oraz Router_3
- Każdy router ma własną sieć LAN (switch + komputery)

## Adresacja IPv6

Prefiks bazowy: `2001:db8:acad::/48`

| Segment                      | Podsieć              |
| ---------------------------- | -------------------- |
| Router_1 ↔ Router_2 (Serial) | 2001:db8:acad:4::/64 |
| Router_1 ↔ Router_3 (Serial) | 2001:db8:acad:5::/64 |
| LAN przy Router_2            | 2001:db8:acad:1::/64 |
| LAN przy Router_3            | 2001:db8:acad:3::/64 |

## Status

- [x] Połączenia Serial skonfigurowane i przetestowane (ping OK)
- [ ] Adresacja sieci LAN
- [ ] Routing między podsieciami

---

# DNS Lab — Basic DNS Resolution

## Opis

Proste ćwiczenie konfiguracji DNS w Cisco Packet Tracer, wykonane
na podstawie wiedzy z kursu CCNA.

Celem ćwiczenia jest skonfigurowanie serwera DNS, dodanie rekordów DNS
oraz sprawdzenie rozwiązywania nazw z poziomu komputera i routera.

## Topologia

![Topologia sieci](topologia_DNS.png)

- 1 router (R1)
- 1 switch (SW1)
- 1 komputer (PC1)
- 1 serwer pełniący funkcję DNS Server

## Adresacja IPv4

Sieć: `192.168.10.0/24`

| Urządzenie | Interfejs / rola | Adres IP       |
| ---------- | ---------------- | -------------- |
| R1         | Gateway          | 192.168.10.1   |
| PC1        | Host             | 192.168.10.10  |
| Server     | DNS Server       | 192.168.10.100 |

### DNS Records

| Nazwa              | Adres IP       |
| ------------------ | -------------- |
| `www.lab.local`    | 192.168.10.100 |
| `router.lab.local` | 192.168.10.1   |

## Konfiguracja DNS

Na serwerze włączono usługę DNS i skonfigurowano rekordy:

- `www.lab.local` → `192.168.10.100`
- `router.lab.local` → `192.168.10.1`

Na PC1 skonfigurowano adres DNS Server:

`192.168.10.100`

Na R1 skonfigurowano korzystanie z serwera DNS:

```cisco
ip name-server 192.168.10.100
ip domain-name lab.local
```

## Testy

Rozwiązywanie nazw zostało przetestowane z poziomu PC1:

```text
ping www.lab.local
ping router.lab.local
```

Test `router.lab.local` zakończył się poprawnie:

```text
Pinging 192.168.10.1 with 32 bytes of data:

Reply from 192.168.10.1: bytes=32 time<1ms TTL=255
Reply from 192.168.10.1: bytes=32 time=1ms TTL=255
Reply from 192.168.10.1: bytes=32 time=1ms TTL=255
Reply from 192.168.10.1: bytes=32 time<1ms TTL=255

Ping statistics for 192.168.10.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

## Status

- [x] Topologia skonfigurowana
- [x] Adresacja IPv4 skonfigurowana
- [x] DNS Server skonfigurowany
- [x] Rekordy DNS dodane
- [x] PC1 skonfigurowany z adresem DNS Server
- [x] Rozwiązywanie `router.lab.local` przetestowane — ping OK
- [ ] Test `nslookup`
- [ ] Test DNS z poziomu R1
