---
created: 2026-10-27
tags:
  - baby
topics:
author: Danilo Quattrini
---
# ARM Cortex-A8 & Intel Core i7
---
## ARM Cortex-A8 
Introdotto nel 2005 che supporta l'architettura ARMv7-A,

![[Screenshot 2026-10-27 at 10.14.21.png]]
Esempio di pipeline, se i salti vengono predetti i salti sbagliati **si perdono ben 13 colpi di clock**, dove a sinistra c'è la **fase di fetch**, una **fase di decode nel mezzo** ed una parte di execute, load oppure store.

- **Instruction Fetch**
- **Instruction Decode**![[Screenshot 2026-10-27 at 10.16.34.png]]
  Viene fatta una decodifica in anticipo
- **Instruction Execute**:![[Screenshot 2026-10-27 at 10.18.29.png]]

### Hazard nel processore
Ci sono **hazard di tipo strutturali**, dove 2 istruzioni nella *issue packet* usano la stessa funzionalità, poi ci sono gli **hazard di dato** che è compito del compilatore poter risolverli e invece gli **hazard di controllo** hanno una penalità di ben 13 cicli di clock se si sbagliano le **branch**