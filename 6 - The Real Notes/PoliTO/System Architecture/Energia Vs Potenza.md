---
created: 2026-09-23
tags:
  - baby
topics:
  - Architecture 
  - "[[School]]"
author: Danilo Quattrini
---
# Energia Vs Potenza
---
>[!quote] Definizione Di Energia
>Per energia viene intesa quanta scarica elettrica server per poter svolgere un'operazione all'interno di un computer, l'unità di misura dell'energia è in *[^1]joule*, che spesso nei processori sono in *microjoule* o *nanojoule* ed è ciò che **scarica la batteria** nel tempo

>[!quote] Definizione Di Potenza
>La potenza viene intesa come la quantità di energia che si consuma per un'unità di tempo. Si misura con il *watt*, che equivale a 1 [joule](https://it.wikipedia.org/wiki/Joule "Joule") al [secondo](https://it.wikipedia.org/wiki/Secondo "Secondo") (1 J/s). È ciò che **scalda il chip** e determina quanto deve dissipare il sistema di raffreddamento.

>[!example]
>Relazione:
$$\text{Potenza} = \frac{\text{Energia}}{\text{Tempo}}​$$
Se fai un compito in 1 secondo consumando 1 *joule* → potenza = 1 W.  
Se lo fai in 10 secondi consumando sempre 1 *joule* → potenza = 0,1 W.
## Consumo di Energia / Potenza
Con l'incremento dei sistemi e l'integrazione di nuovi dispositivi che portano spesso al consumo di energia e potenza. Questo consumo può essere di due aspetti differenti:
-  **Potenza**: (statica e dinamica)
- **Energia** (principalmente per i dispositivi portatili)

### Potenza 
Potenza lo associamo a $P$ quindi la formula sarà
$$P_{dn} = \frac{1}{2} * cl * V^{2} * frq$$
$cl$: che sta per capacitive 
$V$: inteso come voltaggio
$frq$: frequenza 
$$P_{st} = V * I$$
### Energia
E' data dalla formula 

>[!note]
>$$E_{dn}=cl*V^{2}$$
>- $cl$: che sta per **Capacitive Load**, cioè la capacità di energia che può caricare un transistor 
>- $V$: sta per il voltaggio che lo eleviamo al quadrato

# Reference
---

[^1]: Un joule può essere anche definito come il lavoro svolto per erogare la potenza di un watt per un secondo [WikiPedia](https://it.wikipedia.org/wiki/Joule)
