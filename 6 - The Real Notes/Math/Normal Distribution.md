---
created: 2026-02-14T15:43:00
tags:
  - baby
topics:
  - Math
  - AI
  - BigData
author: Danilo Quattrini
---
# Normal Distribution
---
## Population Vs Sample
They are all the data that we get from a **population**, like a set or a group of people, and a **sample** that's a sub-set of the population, the size of the sample it's the **Sample Size**.
![[population-vs-sample.png]]

> [!info] Example
> if the population is all students in a school, a sample could be 50 students randomly chosen from different classes to participate in a survey.

### Statistic vs Parameter
From the concept of population and sample we can define two different types of value that can be describe each of them:

- **Parameter**: it's a number that describe a characteristic of the population, that could be the height, weight or some other number that we can define for a group of object or people.
- **Statistic**: It's always a number that describe a characteristic of something, but in this case it's related to a sub-set of the population.

>[!info] Example
>In our school there are 10000 students that we want to know how tall they are, but in our studies we just want to know the height of the students from the field of Computer Science. In this scenario the whole school it's the **Population** where they have **Parameters** as numbers. Beside the Computer Science sector it's considered the **Sample** with their **Statistic** value (a sub-set of the school)

![[statistic-vs-parameter.png]]

That's how we describe the data of a **Sample** and a **Population**, if we want to describe data that are mean to the sample we use the $\bar{x}$ to represent the mean the $s$ for the [[Standard Deviation]].

When instead we handle to the Population we have different parameter names, the **Mean** it's the greek letter $\mu$ (miu) and the **Standard Deviation** $\sigma$ (sigma).

## What's a Normal Distribution?
Is a bell shape graph that describe how data are tend to cluster (avvicinarsi) in the center, where we have the mean $\mu$ (miu) that's always in the center of the graph.
![[Screenshot 2026-08-18 at 22.26.17.png|800]]

With this graph we can say that most of the data are located in the mean, other value are in the end of the graph and others in the end of it. This graph it's used for measure different types of data like: weight, height, volume or blood pressure.
### Characteristics of the Normal Distribution
With the variable we have been talk before, $\mu$ and $\sigma$ we can shape our bell curve normal distribution in two different ways.

With the $\mu$ (the mean) we **define the position of the normal distribution**, where it's located the bell shape graph.
![[Screenshot 2026-08-18 at 22.31.30.png]]

As we can see from the image if we increase or decrease the mean $\mu$ then the **normal distribution** will follow the value of the mean, that's because the data are all cluster in the center of the mean. The value of the mean determinate the position of the normal distribution.

With the $\sigma$ (Standard Deviation) we **define the spread of the normal distribution**, if the standard deviation it's small than the curve it's more narrow in the the center, whereas if the value of the $\sigma$ it's large then it will be bigger.

![[Screenshot 2026-08-18 at 22.36.35.png|767]]

### What to remember about the normal distribution?
There are several things to remember about the normal distribution that are relevant to remember.
1. The normal distribution is unimodal ([unimodale](https://www.treccani.it/vocabolario/unimodale/)), that means it has only one peak.
2. The normal distribution is symmetric about its mean, that's where the mean divide the curve in two equal curve.
3. The parameters $\mu$ and $\sigma$ characterize completely the normal distribution graph, where *miu* define the position of the graph and the *sigma* the spread of the data in the normal distribution.
# Reference
---
[Population Vs Sample](https://www.geeksforgeeks.org/maths/population-and-sample-statistics/)
