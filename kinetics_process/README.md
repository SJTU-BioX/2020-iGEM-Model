## Kinetics Process

We have applied Markov process to fitting the kinetics process of binding and cleavage of CRISPR/Cas9. 

![](https://2020.igem.org/wiki/images/d/d9/T--SJTU-BioX-Shanghai--kinetic_process.png)

In our kinetics model, we consider the binding process of Cas9/dCas9 consists of finite states from the unbound stage, PAM recognition to base pairing. Previous study has proposed that the probability of cleavage on a target site or transcriptional regulation once the substrate is bound is equivalent to the stationary probability of a Birth-Death process.
$$
P_{off-target} = (1+\sum_{n=0}^N\prod_{i=0}^n\gamma_i)^{-1} = \left[1+\sum_{n=0}^N\exp\left(\frac{\Delta T_n}{RT}\right)\right]^{-1},\Delta T_n = T_{n+1,n}-T_{-1,0} 
$$
Where $T_{i,i+1}$ means the free energy of transition state between $i$ and $i+1$
$$
\Delta T_n = -\Delta_{PAM} - n_c(n)\Delta c + (n-n_c(n))\Delta I + \delta_{n,N}\Delta_{clv/reg}
$$

| Symbol             | Meaning                                            |
| ------------------ | -------------------------------------------------- |
| $\Delta_{PAM}$     | Energy change when PAM recognition                 |
| $\Delta c$         | Energy change when correctly matching              |
| $\Delta I$         | Energy change when incorrectly matching            |
| $\Delta_{clv/reg}$ | Energy change when cleavage or regulation happens  |
| $n_c(n)$           | numbers of correct matches within first n position |
| $\delta_{n,N}$     | Indicator variable, equals 1 when n=N else 0       |

We fit our model with several target sequences （SpCas9 vs xCas9）to infer the difference in the binding process. We use genetic algorithm to approach the optimal fitting result and obtain the approximate kinetics parameters about PAM recognition, R-loop formation and cleavage. 

|  Target   |   Cas9    | $\Delta_{PAM} /k_BT$ | $\Delta c /k_BT$ | $\Delta I /k_BT$ | $\Delta_{clv} /k_BT$ |
| :-------: | :-------: | :------------------: | :--------------: | :--------------: | :------------------: |
|   VEGFA   |  SpCas9   |        -0.483        |      -0.270      |      1.713       |        1.779         |
|   VEGFA   | xCas9 3.7 |        -1.288        |      -0.456      |      4.946       |        0.098         |
| HEK site1 |  SpCas9   |        -1.528        |      -0.543      |      3.028       |        1.031         |
| HEK site1 | xCas9 3.7 |        -4.302        |      -0.522      |      6.332       |        0.494         |

We have visualized the alteration of transition state energy when targeting on a off-target site and evaluate the off-target effect caused by the mismatch of two positions. We can see xCas9 relieves the off-target effect on both VEGFA site and HEF site1 evidently.

![](https://2020.igem.org/wiki/images/9/90/T--SJTU-BioX-Shanghai--targeting_progression.png)

![](https://2020.igem.org/wiki/images/a/a9/T--SJTU-BioX-Shanghai--multi_mismatch.png)