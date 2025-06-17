---
marp: true
style: |
    section.centered {
        display: flex;
        flex-direction: column;
        justify-content: center;
        text-align: center;
        width: auto;
    }
---

<!-- _class: centered -->

# Graph coloring

plus five words about myself

---

## Table of contents

1. Who am I? 
    A fast introduction to myself.


2. My master's thesis
    An overview of the work I did for my thesis.


3. Graph coloring
    Literature review for the topic I am interested in.

---

<!-- _class: centered -->

# 1. Who am I?

---

## Hallo! I'm

<div class="colwrap">
<div class="left">
Alessandro Biagiotti, 

I just completed my Master's degree in computer science. I studied mostly: algorithms, parallel and distributed computing, ML and physics.
</div>
<div class="right inverted">
<img width="60%" src="./img/pfp.jpg">
</div>
</div>

---

## My academic life

- 2018: Began my bachelor in Computer Engineering, couldn't finish due to Covid19 struggles.


- 2020: Changed my bachelor to computer science.


- 2022: Graduated with a thesis on Web Application development in team. In September I started my Master's.


- 2023: Did my Erasmus in Heidelberg I attended a mix of courses in Computer Science, Scientific Computing and Physics.


- 2025: Graduated in Computer Science with a thesis on Machine Learning applied to Superconductor behavior.

---

## Three things I love and one I hate

1. I love trekking and climbing.


2. I love cinema and movies (one of my whole time favourites is Ivan's childhood).


3. I love to interact with people.


I am not the biggest fan of football.

---

<!-- _class: centered -->

# 2. My master's thesis

---

## Superconductors

A superconductor is a material allowing the passage of electrical current having electrical resistance $R = 0$.

Superconducting material can be of the first type (top image) or of the second type (bottom image). Superconductors of the second type are usually employed in the field of high energy physics.

---

## Large Hadron Collider

<div class="colwrap">
<div class="left" style="margin-top:60px">

- Operational since 2009.

- Uses two counter-rotating proton beams that meet in one of the interaction regions (CMS, ATLAS, LHC-b, ALICE) at circa 14 TeV.

- Used for fundamental physics experiments.

</div>
<div class="right inverted">
<img width="80%" src="./img/lhc.jpg">
</div>
</div>

---

## High order correctors

Span the information

Developed by INFN/LASA, to be installed on LHC for the high luminosity upgrade.

Designed to correct field errors introduced by the new Focusing quadrupoles.

<br>

<div class="himg">
    <img width="800px" src="./img/HighOrders3.jpg">
</div>

---

## The quench phenomenon

A superconductor quenches whenever it unpredicatbly transitions from the superconducting state to the normal conducting state. This change leads to an important change in the material's behavior which, in the field of accelerator physics, can lead to:

- Material destruction,

- Important economical and temporal losses,

- Beam loss,

- Potential damage to experiments.

---

## My contribution

Using explainable machine learning models we tried to solve the following problems:

- Quench recognition: Identifying whether the magnet has quenched or not.

- Quench localization: If the magnet has quenched find an explainable machine learning model capable to identify the coil the has quenched.

- Quench recognition +: A variation of QRP that has been used to provide the first solutions for QLP.

---

## The data

- The data consisted of $4$ different datasets describing the magnetic field quality measured after
a quench event or after the magnet discharge.

- Each dataset consisted of $279$ data points divided in $15$ harmonics.

- The data describes the magnet behavior as a whole.

- The data was split in two sets: one of $250$ samples for experiments and one of $29$ points for
testing.

---

## Performance evaluation

- Accuracy (Acc), fraction of correct predictions.

- Precision (Prc), number of true positives over number of positive predictions.

- Recall (Rec), number of true positives over the number of expected positives.

- Inverse recall (Irec), number of true negatives over the number of expected negatives.

- F1 score (F1), harmonic mean of Precision and recall.

- ROC AUC (RAUC), a good indicator of the quality of the model found.

---

## Decision trees for QRP

<div class="colwrap">
<div class="left" style="margin-top:150px">

- High explainability,

- High degree of performance,

- Highly customizable structures.

</div>

<div class="right inverted vimg">
    <img width="500px" src="./img/An_dt.png">
    <img width="500px" src="./img/best_trees.png">
</div>


---

## Performance for aggregate models

Decision trees already performed well, but we decided to look into different models to see if we
could unlock better performing models. Thus we started looking into models aggregating trees.

- Random Forests were our first guess but they didn't provide a good enough performance improvement
compared to the structure's complexity.

- Making informed choices regarding which model would go in the forest (instead of sampling randomly
from the set of available features for splits) provided better performance.

---

## Performance for aggregate models (cont'd)
<div class="colwrap">
<div class="left">

- We compared the performance of the other models against an unexplainable model (SVC), which is characterized by a very high level of performance.

- Our 'informed-sampling' model proved to have very good performance in experiments and the final
blind test proved that the performance actually hold.

</div>

<div class="right inverted vimg">
    <img width="550px" src="./img/model_comparison.png">
</div>

---

## Solutions for QLP

-  We tried doing an extension of QRP solvers to QLP with little success (due to the complex nature of the multiclass problem).

- Our solution was to have a tree constructed on every coil to solve the QRP+ problem for that specific coil. Thus it was very important to make sure that the submodels were as easy as possible (the final model contains $4$ different submodels, one per coil).

- The results obtained using the scorer defined below were modest 
Experiments: $0.952 \pm 0.002$
Final test: $0.96 \pm 0.09$

$$
\mathcal{H}(y, \hat{y}) = 1 - \frac{h(y, \hat{y})}{4}
$$

---


## Conclusions

##### What we achieved
We found explainable ML models for the problem of quench recognition and localization in superconducting magnets.

##### The limitations of our results
1. The scarsity of the available data is an important limitation for our results.
2. The results only applied to the particular family of High Order Correctors.

##### What we want to see in the future
1. Clustering approach,
2. High speed QRP and QLP models for online settings,
3. Fuzzy description of the quench event.

---

## Clustering example

<div class="himg">

![w:1000](./img/Clustering.png)

</div>

---

<!-- _class: centered -->

# Graph coloring problem

---

## What is the graph coloring problem?

Given an undirected and unlabelled graph $G = (V, E)$, we say that a function $f$ is a *correct* coloring for $G \iff f(v) \neq f(u)$ for all $u$ and $v$ neighbouring vertices.

The minimum number of colors required to obtain a correct coloring for $G$ is known as the *chromatic number* for $G, \chi(G)$.

---

## GCP is a complex problem

- Deciding whether a graph is $k$ colorable is NP-complete.

- Finding the chromatic number $\chi(G)$ for a graph is NP-hard.

- Variations of the problem are also \#P complete (e.g. count the number of $3$-colorings in the graph).

---

## Some applications of GCP

1. Resource allocation tasks:

    - Assigning frequencies in networks,

    - Timetabling in problems (e.g. assigning rooms to exams),

    - Register allocations in compilers <a href="#footnote-1">\[1\]</a>.

2. Parallelising factorization steps (e.g. ILU factorization \[\]).

<br></br><br>


<h4></h4>
<sub><sub><sub>
<div id="footnote-1"></div>
1. For more information about how this could be used check out Moritz's slides.
</sub></sub></sub>

---

<!-- _class: centered -->

# Landscape of available CPU solutions

---

## Dsatur \[Bre79\]

<div class="colwrap">
<div class="left">
Despite its age Dsatur has been proven solid and I consistently found it as a reference technique in the literature.

This method finds an exact coloring for bipartite graphs. It can be used as a lower bound on the Chromatic number.
</div>
<div class="right inverted">
<code>
1. <u>Sort</u> all vertices in decreasing degree order.
<br>
<br>
2. <u>Color</u> a vertex of maximal degree with 1.
<br>
<br>
3. <u>Choose</u> a vertex of maximal saturation <a href="#footnote-2">[2]</a>.
<br>
<br>
4. <u>Color</u> the vertex with the least possible number.
<br>
<br>
5. <u>Loop</u> until all vertices are colored.
</code>
</div>
</div>

<h4></h4>
<sub><sub><sub>
<div id="footnote-2"></div>
2. We define saturation of a vertex  the amount of neighbours that have been colored.
</sub></sub></sub>

---

## Hybrid Evolutionary Algorithm \[Hao99\]

<div class="colwrap">
<div class="left">
HEA for GCP was ideated by Galiner and Hao in 1999 and proved to be a successful algorithm to solve the problem.

The local optimization step is what sets it apart from more classical EA <a
    href="#footnote-3">[3]</a>.
</div>
<div class="right inverted">
<code>
1. <u>Generate</u> the initial population with a variant of <u>Dsatur</u>.
<br>
2. While there is no convergence or we are within a certain number of iterations:
<br></br>
3. Choose the parents from the population.
<br>
4. Perform crossover.
<br>
5. Perform L iterations of <u>Tabu Search</u>.
<br>
6. Update the population by removing the worse parent.
</code>
</div>
</div>

<h4></h4>
<sub><sub><sub>
<div id="footnote-3"></div>
3. A study [Glass03] highlights the fact that the algorithm remains a strong performer even if the TS component is removed.
</sub></sub></sub>

---

## Crossover in \[Hao99\]

<div class="himg" style="margin-top:100px">
    <img width="90%" src="img/crossover.png">
</div>

---

## Hill climbing heuristic \[Rhyd09\]

<div class="colwrap">
<div class="left">
The Hill Climbing Heuristic combines Dsatur, local search and the first fit heuristic in a single package and tries to provide performance close to the ones obtained by HEA. 
</div>
<div class="right inverted">
<code>
1. <u>Generate</u> the initial solution for the problem &pi;.
<br>
2. Put a small part of the classes of &pi; in a new permutation &rho;.
<br>
3. Utilize a <u>local search technique</u> to make sure that both &pi; and &rho; remain feasible and do not increase the number of classes used.
<br>
4. <u>Append</u> &rho; to &pi;.
<br>
5. Do a <u>shuffle</u> of the obtained solution.
<br>
6. Run the <u>first fit heuristic</u> and go back to 2
</code>
</div>
</div>

---

<!-- _class: centered -->

# Landscape of available GPU solutions

---

## Jones Plassmann Luby \[Plmn93\]

<div class="colwrap">
<div class="left">
JPL is a classical coloring algorithm ideated in 1993 by Jones and Plassman, they interpreted the coloring as an independent set to use Luby's Monte Carlo approach capable of identifying an independent set in a graph in parallel.
</div>
<div class="right inverted">
<code>
1. Associate a random number to the vertices in the graph.
<br></br>
2. Construct an independent set I <u>in parallel</u>.
<br></br>
3. Color I <u>in parallel</u>.
</code>
</div>
</div>

---

## The JPL problem \[Bor23\]

<div class="himg" style="margin-top:50px">
    <img width="700px" src="./img/problem_JPL.jpeg">
</div>

---

## Cohen Castonguay \[Coh12\]

The Cohen-Castonguay algorithm is a different spin of the JPL that modifies the procedure used to construct the independent set.

Instead of using memory to store the random number associated to each vertex we identify a set of $k$ different hash functions.

This approach is much faster than accessing memory, but increases the complexity of the algorithm because it's now necessary to identify a good value for $k$ and then the coloring information needs to be combined, to do so we can use many different heuristics (e.g. embewing an ordering in the hash function list).

---

## Atos framework \[Yux22\]

Atos is a task-parallel GPU dynamic scheduling framework that offers a solution to the three main performance bottlenecks of working with graphs:

- Small frontier problem,

- Load imbalance,

- Loss of concurrency opportunities.

The key aspects leveraged by Yuxin et al. are: Barrier relaxation, worker size, balancing data and task parallelism and kernel strategy (with either persistent or discrete kernel calls).

---

## Atos vs Gunrock \[Yux22\]

Atos is compared to the BSP framework Gunrock (which was first revealed in 2018), and the performance can be quite a bit better, despite the drawbacks of the reuse approach required by the speculative behavior of the algorithms.

In the images below we see the compute time of different configurations for the Atos framework compared with a simulation of Gunrock (left), in ms, and the amount of repeated calculations due to speculation on the right.

<div class="himg" style="margin-top:30px">
    <img width="50%" src="img/runtimes_atos.png">
    <img width="50%" src="img/replication_atos.png">
</div>

---

## Atos (right) vs Gunrock (left)

<div class="himg" style="margin-top:50px">
    <img width="50%" src="img/bsp.png">
    <img width="60%" src="img/atos.png">
</div>

---

## Sources

**\[Bre79\]** :: Brélaz, Daniel; *New methods to color the vertices of a graph* April 1979 Commun. ACM pp 251 - 256 [doi](https://doi.org/10.1145/359094.359101)

**\[Hao99\]** :: Galiner, Philippe; Hao, Jin-Kao; *Hybrid Evolutionary Algorithms for Graph Coloring* 1999 Journal of Combinatorial Optimization pp 379 - 397 [springer](https://link.springer.com/article/10.1023/A:1009823419804)

**\[Glass03\]** :: Glass, Celia A.; Prügel-Bennett, Adam; *Genetic Algorithm for Graph Coloring: Exploration of Galinier and Hao's Algorithm* September 2003 Journal of Combinatorial Optimization pp 229 - 236 [doi](https://doi.org/10.1023/A:1027312403532)

**\[Rhyd09\]** :: Rhydian, Lewis; *A general-purpose hill-climbing method for order independent minimum grouping problems: A case study in graph colouring and bin packing* 2009 Computers & Operations Research pp 2295-2310 [doi](https://doi.org/10.1016/j.cor.2008.09.004)

---

## Sources (cont'd)

**\[Plmn93\]** :: Jones, Mark T.; Plassmann, Paul E.; *A Parallel Graph Coloring Heuristic* 1993 SIAM Journal on Scientific Computing pp 654 - 669 [doi](https://doi.org/10.1137/0914041)

**\[Bor23\]** :: Borione, Alessandro; Cardone, Lorenzo; Calabrese, Andrea; Quer, Stefano; *An Experimental Evaluation of Graph Coloring Heuristics on Multi- and Many-Core Architectures* 2023 IEEE Access pp 125226-125243 [ieee](https://ieeexplore.ieee.org/document/10304117)

**\[Coh12\]** :: Cohen, J.; Castonguay, P.; *Efficient Graph Matching and Coloring on the GPU* 2012 GPU Tech., GTC on-demand

**\[Yux22\]** :: Chen, Yuxin; Brock, Benjamin; Porumbescu, Serban; Buluc, Aydin; Yelick, Catherine; Owens, John; *Atos: a task-parallel GPU scheduler for graph analytics* 2023 Proceedings of the 51st international conference on parallel processing, Association for Computing Machinery [doi](https://doi.org/10.1145/3545008.3545056)

---

<!-- _class: centered -->

# Thank you for your time

Any questions?
