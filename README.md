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
