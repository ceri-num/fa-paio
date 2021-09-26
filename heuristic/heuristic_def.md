# Heuristique & définition

Mais concrètement ? Qu'est-ce qu'une heuristique ? --> Wooclap

Une heuristique peut être considérée comme une méthode de calcul mathématique ou empirique, spécialement conçue pour apporter des perspectives de résolutions à un problème spécifique. L'on en a recourt principalement lorsque le problème est complexe et ne peut être résolu en un temps raisonnable, ou qu'il est difficilement modélisable.

{% hint style="info" %}
Le concept de temps raisonnable varie d'un contexte d'application à l'autre. Par exemple, prendre plusieurs semaines pour reconstituer l'image d'une coalescence de deux trous noirs est raisonnable, mais prendre le même temps pour calculer quel coup jouer à BloodBowl ne l'est pas.
{% endhint %}

L'objectif d'une fonction heuristique $$h(n)$$ est donc de produire ou d'aider à produire une solution **acceptable** en un temps **raisonnable** à un problème donné, en classant les solutions ou les états au fur et à mesure de l'exploration du problème. C'est une fonction **d'estimation** (de score).

Cela introduit donc la notion de **trad-off**. Autrement dit, puisqu'il ne s'agit plus d'une étude exhaustive du problème, mais qu'on choisit en amont les états à explorer, cela a un effet sur :
* La complexité
* L'optimalité
* La précision
* Le temps d'exécution
 
Concrètement, elles peuvent **aiguiller** la résolution du problème à l'aide des informations et des connaissances supplémentaires, ou **prunner** (*to prune* -> élaguer) des espaces entiers de recherches sur simple calcul. Par exemple, dans le cas du voyageur de commerce, on peut commencer par prendre les distances les plus petites entre les villes, tel que $$min(h(n_1),\dots,h(n_m))$$ (distance en vol d'oiseau).

![Graphe simplifié des villes de Roumanie, avec une distance indiquée sur l'arête, en vol d'oisal.](assets/straightlineheuritic.png)

Attention toutefois, l'on peut avoir recours à la notion d'heuristique même en dehors d'une stratégie informée, c'est simplement qu'elle conditionne l'efficacité même de l'exploration dans le cadre d'une telle approche.

{% hint style="info" %}
De par sa nature, on peut utiliser une fonction heuristique pour résoudre un problème alors qu'on ne connaît pas d'algorithme capable de le résoudre !
{% endhint %}


http://helios.mi.parisdescartes.fr/~bouzy/Doc/IAL3/03_IA_heuristique_BB.pdf
Wow, wow wow, concrètement, qu'est-ce que heuristique, meta-heuristique hyper-heuristique ?

def et intuition, tradoff, pruning
heurisitique : ça estime


wooclap


## Quelques heuristiques courantes
puis listing

* Manhattan (1-distance) : $$d_m=[x_b - x_a] + [y_b - y_a]$$
* Euclidienne (2-distance) : $$d_e=\sqrt{\sum_{i=1}^{n}(x_i - y_i)^{2}}$$
* Tchebychev (∞-distance) : $$d_t=\lim_{p \to \inf}\sqrt[p]{\sum_{i=1}^{n}\vert x_i - y_i \vert^{p}} = \sup_{1\leq i \leq n}\vert x_i - y_i \vert$$

## Différence entre Heuristique, Meta-heuristique et Hyper-heuristique
Wooclap

Now meta-heuristics. As already mentioned, heuristics 1) use domains specific knowledge and therefore cannot be easily used to solve other problems(thought for a specific problem). 2) Heuristics can easily stuck at local optima. Meta-heuristics are proposed both of these two drawbacks. So Genetic Algorithms (GAs) are kind of meta-heuristics which can be used to solve the TSP problem, Scheduling problems,.... and many other problem. This is because Meta-heuristics do not require problem domain knowledge (it is like a general heuristic that fits to many problems). GAs for instance use mutation which helps escaping from local optima. Meta-heuristics can also use heuristics inside them which usually helps but this is not a must. Compared to heuristics. Meta-heuristics converge slower than normal heuristics.
Now we have the idea that meta-heuristics fit many problems and therefore the are general. Example Meta-heuristics are GAs, Ant Colony Optimization, Simulated Annealing.....
Research and experiments indicated that some meta-heristics perform better for some type of problems. In addition, research indicated that for the same problem, different meta-heuristics perform better for different instances. Even, different meta-heuristics perform better at different stages of the solution process for the same instance. So for example, if we are solving and instance of TSP problem, it could result that the best solution is a result of running first GA, then Simulated Annealing then Ant-colony. And here comes Hyper-heuristics. Hyper-heuristics are to tell what sequence of Meta-heuristics to use to solve the problem at hand. Also it can be used to classify what meta-heuristic fits better to which problem.

## Petit playground
Wooclap -> q6

Vous pouvez vous amuser à tester différentes heuristiques pour des algorithmes de *path-findings* [ici](https://qiao.github.io/PathFinding.js/visual/) !