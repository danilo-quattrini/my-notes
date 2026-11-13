---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - Architecture 
  - "[[School]]"
author: Danilo Quattrini
---
# Exames Examples
---
- Primo esempio sarà un programma nella quale calcolare i cicli di clock, completando una tabella di riferimento 
	- Il forwarding sarà sempre attivo.
	- I calcoli con i floating point sono sempre disponibile.
	- Dati in cui l'architettura può variare.
	- Di solito le unità dei Floating Point cambiano e sono più colpi di clock (multiplier possono essere 6 stage e arithmetic 2 stage), dove il divisore non è pipelined.
Vedere l'esempio della pipeline completa del professore [qui](https://docs.google.com/document/d/17v-xf-Me5gGGavqsdmnKQGpHeIWLWplr7dsWYhese0U/edit?pli=1&tab=t.0)

## Esempio Pipelined + SuperScalare
```c
for(i = 0; i < 100; i++) {
	 Y[i] = X[i]^2 + X[i] / Z[i]
}
```

Si dovrà vedere come si comporta il programma si comporta in una pipeline e come si comporta il programma si comporta nel superscalare