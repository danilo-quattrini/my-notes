---
created: 2026-11-03
tags:
  - baby
topics:
  - Microprocessors
  - ARM
  - Architecture 
author: Danilo Quattrini
---
# Introduction
---
**A**dvanced **R**isc **M**achine (ARM) è un'architettura RISC che viene utilizzato nei dispositivi mobile ed embedded.

Si divide in 3 categorie diverse che sono:
- ARM architecture embedded in System on Chip (SoC)
- ARM Operating System
- ARM compile - support - debug tools

Qui sotto abbiamo le 3 macro famiglie dei processori ARM:
![[IMG-ARM Legenda-20261103.png]]

### System On Chip (SOC)
![[IMG-ARM Legenda-20261103-1.png]]
Sono composti da diversi elementi non solo da processore e sono composti interamente in silicio, sono composti da diversi moduli chiamati embedded. 
## Tool chain
![[IMG-ARM Legenda-20261103-2.png]]

Si avrà un tool che farà una **cross-compilation**, che può eseguire il codice che scriviamo in assembly o C. Questo ci permette anche di eseguire un debug del codice, andando a guardare ogni singolo stato dei registri e controllare ogni singola istruzione per volta.

Ci è possibile anche vedere **il valore reale dei registri**.

Quello che si andrà a vedere in questa parte sarà i seguenti argomenti:
- ARM assembly principles
	- [[ARM Instruction Set Architecture|Instruction Set Architecture]] (ARM)
	- C++, ASM programming con gli standard ABI
	- System-on-Chip level programming including

-  Internal, SW and HW interrupts management
	- Gestione delle Eccezioni 
	- Software (SW) Interrupts in base alle chiamate del sistema
	- Hardware (HW) interrupts
	  
- Extended system on-board features