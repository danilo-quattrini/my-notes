---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
author: Danilo Quattrini
---
# LAB - 01
---
Given the IPv6 prefix :
```
2001:1000::/56 -> 2001:1000:0000:00 | 00:0000:0000 / 56
```

Abbiamo come prefisso di rete:
```
2001:1000:0000:00
```

prendiamo ora la parte della rete e convertirla in binario:
```
2001:1000:0000:0000 0000 0000 0000 0000 1100 : |
2001:1000:0:12::2 / 64
```
![[Screenshot 2026-10-29 at 17.14.15.png]]

Ci sono ben 5 sotto-reti che sono le seguenti
- R1 verso R3 -> `2001:1000:0:13::2 / 64`
- R3 verso R2 -> `2001:1000:0:32::2 / 64`
- R3  verso R4 -> `2001:1000:0:34::2 / 64`
- R2 verso R5 -> `2001:1000:0:25::2 / 64`
- R4 verso R5 -> `2001:1000:0:45::2 / 64`

Quando si devono dare solo due host si può utilizzare sempre la `/64`