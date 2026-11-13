---
created: 2026-11-06
tags:
  - baby
topics:
  - Architecture 
  - Microprocessors
  - ARM
author: Danilo Quattrini
---
# ARM ALU
---
## Introduzione
Partiamo prendendo per esempio questo codice
```asm
// r4 = 21, r3 = 12
SUBS r5, r4, r3
BEQ cond_r1

cond_r2
	mov r0, r2
	b fine

cond_r1 mov r0, r1
```

- `SUB{S} rd, rn, rm`: faccio una sottrazione tra due registri, attivando i flag, questo perché davanti all'operando abbiamo messo la `S`.

- `BEQ cond_r1`: questa condizione si avvera se e solamente se il flag `Z` nel [[ARM Cortex M3#PSR - Program Status Register|xPSR]] è impostato ad `1` (cioè se la sottrazione precedente ha ritornato come risultato della sottrazione `0`)

Il flag che si attiva dalla sottrazione è il `C`-arry flag, che sarà il (riporto) dalla sottrazione / addizione, che vuol dire riporto? 

Per riporto intendo che il risultato dell'operazione supera la dimensione dei 32 bit del registro.

## `C` - arry Flag
Il carry flag si attiva come visto precedentemente con una sommatoria nella quale va a creare un riporto.
![[IMG-ARM ALU-20261106.png]]

Oppure si può attivare quando si svolge una sottrazione (carry borrow), e **si prende in prestito il bit più significativo sottratto**, che sarà 1 meno il flag `C`
![[IMG-ARM ALU-20261106-1.png]]

Un ultimo caso in cui si può attivare il flag `C` sarà quando si svolge un'operazione di shift dei bit di un numero.

>[!example]
>`1101 0000 0000 0000 0000 0000 0000 0000`
>Se svolgo un operazione di shift verso sinistra `<< 1`, avremmo questo risultato:
>`1010 0000 0000 0000 0000 0000 0000 0000`
>Notiamo che il bit che è uscito dalla linea dei bit è andato via e viene messo nel flag `C` che diventerà `C = 1`

>[!info] Utilità?
>Il Carry flag può essere utilizzato nelle operazioni **aritmetiche senza segno**, serve per identificare degli errori. Mentre nell'**aritmetica con segno** viene utilizzato per fare delle comparazioni con altri flag.

## `N` - egative Flag
Il flag `N` identifica il bit più significativo del numero che è un valore negativo, questo perché noi stiamo lavorando in [[Calculator Arithmetic#Two's Complement|complemento a due]],  vediamo un esempio facendo la "sottrazione" tra $-4 + (-3) = -7$ 
```
1111 1111 1111 1111 1111 1111 1111 1100 +
1111 1111 1111 1111 1111 1111 1111 1101 =
----------------------------------------
N = 1 111 1111 1111 1111 1111 1111 1111 1001
    ^
	|
Se l'ultimo bit è uno allora il risultato dell'operazione è negativo
```

## `V`- Overflow Flag
L'overflow flag avviene se e solamente se se la somma tra due operandi dello stesso segno andranno a superare la dimensione dei 32 bit, indica se ci sono dei problemi.![[IMG-ARM ALU-20261106-2.png]]

## `Z`- Zero flag
![[IMG-ARM ALU-20261106-3.png]]
Quando l'operazione ritorna come risultato 0.

# Istruzioni di Comparazione
Le operazioni di comparazione sono utili per comparare e testare dei bit, dove si vanno ad attivare dei flag, senza però cambiare il valore del registro.
```
compare / test <Rd>, <operand>
```

## `CMP`, `CMN`
- L'istruzione `CMP` (compare) svolge una sottrazione tra un registro `Rn` e un `operand` e aggiorna i flag `Rn - Operand2`
- L'istruzione `CMN` (compare negative) svolge una sottrazione tra valori negativi tra un `Rd`e un `operand` aggiornando sempre i flag.

>[!example] Esempio
>Prendiamo un registro `r0 -> #12`, che ha come valore 12, le varie operazioni di comparazione andranno ad attivare i seguenti flag:
>```
>CMP r0, #10 ;N = 0, Z = 0, C = 1, V = 0
>CMP r0, #12 ;N = 0, Z = 1, C = 1, V = 0
>CMP r0, #14 ;N = 1, Z = 0, C = 0, V = 0
>```

Il compilatore può convertire l'istruzione `CMP` a `CMN` se mettiamo come secondo operando un valore negativo.
## `TST`, `TEQ`
- L'istruzione `TST` (test) svolge un AND logico (`&`) tra un registro `Rn` ed un `operand`, aggiornando tutti i flag tranne`V`
- L'istruzione `TEQ` (test equivalence) svolge un operazione di XOR tra due operandi, aggiornando sempre i flag tranne il `V`

# Accessing Program Status Register
- `MRS <Rn>, <Sreg>` : scrive nel registro di destinazione il valore del registro speciale
- `MSR <Sreg>, <Rn>` : scrive nel registro special il valore del registro general purpose

![[IMG-ARM ALU-20261106-4.png]]

# ALU Internal Data Path
![[IMG-ARM ALU-20261106-5.png]]

Un semplice datapath della ALU, che prende due operandi in input e svolge le operazioni

# Arithmetic instructions
- Addizione
- Sottrazione
- Moltiplicazione
- Divisione
## Addizione
```
ADD <Rd>,<Rn>,<op2> Rd= Rn+ op2
```
Semplice addizione tra due registri

```
ADC <Rd>,<Rn>,<op2> ; Rd= Rn+ op2 + C
```
Addizione tra due registri con il `C` Carry flag

## Sottrazione
```
SUB <Rd>,<Rn>,<op2> ; Rd= Rn - op2
```
Semplice sottrazione

```
SBC <Rd>,<Rn>,<op2> ; Rn -op2 + C -1
```
Sottrazione tra due registri con il Carry flag

C'è anche l'operazione di **Reverse Subtraction**:
```
RSB <Rd>,<Rn>,<op2> ; Rd= op2 - Rn + C –1
```

>[!done] Vantaggio
>Uno dei due operandi possono essere shiftati prima di svolgere l'operazione
>```
>SUB r0, r1, r2, LSL #2 ;r0 = r1 – r2 * 4
>RSB r0, r2, r1, LSL #2 ;r0 = r1 * 4 –r2
>```
>Dove un registro si può sottrarre con una costante.

## Moltiplicazione
## Divisione
## Istruzioni Logiche
![[IMG-ARM ALU-20261106-6.png]]

# Istruzioni di Shift
![[IMG-ARM ALU-20261106-7.png]]
`LSL`(Logical Shift Left): Shift a sinistra dove il `C` sarebbe il [[#`C` - arry Flag|carry flag]], viene generato dal MSB

![[IMG-ARM ALU-20261106-8.png]]
`LSR`(Logical Shift Left):Shift a destra dove il `C` sarebbe il [[#`C` - arry Flag|carry flag]], viene generato dal LSB.

>[!warning] Importante
>Questi sopra citati **sono shift logici cioè che non mi importa il segno**, non manterrò il segno!!


![[IMG-ARM ALU-20261106-9.png]]
`ASR` (Arithmetic Shift Right): Shift a destra che però mantiene il segno, questo perché ci importa il segno

# Rotate Instructions
![[IMG-ARM ALU-20261106-10.png]]

# Reference
---
- [ALU Instructions](https://www.dropbox.com/home/Danilo%20Quattrini/2027%20-%2002GOLYG%20-%20Architetture%20dei%20sistemi%20di%20elaborazione%20-%20306840/00_MATERIAL/ARM?preview=04_ALUinstructions.pdf)
