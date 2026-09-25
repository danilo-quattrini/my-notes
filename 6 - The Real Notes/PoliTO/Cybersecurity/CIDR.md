---
created: 2026-09-23
tags:
  - baby
topics:
  - "[[School]]"
  - Cybersecurity
author: Danilo Quattrini
---
# CIDR
---
**C**lassless **I**nter **D**omain **R**outing (CIDR) è il modo alternativo e più utilizzato per indirizzare host di rete differenti. Differisce dal fatto che non ci sono più costrizioni di classe, come gli indirizzi Classfull, ma il network ID è di lunghezza variabile. 

## Formato di un IP nel CIDR
Solitamente un IP nel formato CIDR è il seguente![[Screenshot 2026-09-23 at 16.08.39.png]]
Il formato come vediamo dall'immagine è composta da *prefix length* + *netmask*, cioè le seguenti parti si rappresentano in questo modo:
- *prefix length*: /$x$,  dove $x$ è il numero di bit che sono riservati alla rete
-  *netmask*: dove ci sono tutti i bit ad $1$ sono quelli della rete, mentre quelli degli host sono a $0$.
>[!example] Netmask
>Esempio:
>$$(255.255.254.0)_{10} = (11111111.11111111.11111110.00000000)_{2}$$
>La netmask con i bit a $1$  si rappresenta la parte della rete, mentre gli $0$ sono riservati agli host.

# Reference
---

