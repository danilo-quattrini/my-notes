---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - Math
  - AI
author: Danilo Quattrini
---
# Standard Deviation
---
## Definition
>[!info] What's Standard Deviation
>Is a statistical measure that quantifies the amount of variation or dispersion in a set of values around the mean.

before going to see what's a **standard variantion** we should see what's the **variance**
# Variance
>[!info] Variance
>The average of the **squared** differences from the Mean.

For instance in this example we have five dogs with different heights and we want to calculate the variance for from all of them. To do so we need to first calculate the mean (average) of all the dogs.

Let's say we have five different dog which each of them different sizes 600 mm, 470 mm, 170 mm, 430 mm and 300 mm.
![[Pasted image 20260806163437.png|790]]

To calculate the mean it's easy we just sum the number of element we have in the set and divide by the number of them:
$$
\bar{x} = \frac{\sum_{i=1}^{n}{x_{i}}}n 
$$
The formula of the mean above it's necesary to calculate the mean of the heights:
$$
600 + 470 + 170 + 430 + 300 = 1970 
$$
Then divide by then number of dogs that are $5$
$$
1970 / 5  = 394
$$
## Standard Variation formula
The formula below it's used to calculate the standard deviation
$$
\sigma = \sqrt{ \frac{ \sum_{i=1}^{n}(x_{i} - \bar{x})^{2}}{N} }
$$
Where we have the:
- $\omega$ that's the standard variation result
- $x_{i}$ elements in the population
- $\bar{x}$ the population mean (media)
- $N$ The size of the set
# Reference
---

