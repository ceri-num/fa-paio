
# Propriétés recherchées d'une heuristique

Il est essentiel de comprendre et d'étudier le comportement de vos heuristiques pour savoir si le problème est correctement abordé, et aussi si elles sont optimales. Différentes propriétés viennent coroborer cet état de fait.

## Optimiste
Lorsqu'une heurisitique estime que le coût pour résoudre un problème est moins important que le coût réel, l'on dit alors qu'elle est optimiste.

{% hint style="info" %}
Cette propriété est une composante nécessaire à l'admissibilité d'une heuristique.
{% endhint %}

Il s'agit bien du coût global. Aussi, même si localement le coût pour résoudre une étape peut être plus important que le coût réel, la globalité est toujours inférieure.

{% hint style="warning" %}
Une conséquence de cela est que le coût estimé pour résoudre un problème quelconque peut être (grandement) inférieur au coût réel : la politique pour résoudre le problème est donc biaisé.
Dans certains problèmes d'optimisations, cela peut s'avérer problématique.
{% endhint %}

## Admissibilité
Si $$\forall n, h(n)$$ ne surestime jamais le coût, alors $$h$$ est une heuristique admissible. Par définition, une heuristique admissible est également optimiste.

Un exemple évident d'une heuristique adimissible est celle de distance en vol d'oiseaux (ligne droite) entre deux points. On sait que c'est la distance la plus petite qui existe dans un plan en 2D, et qu'elle ne peut jamais occasionner une **surestimation** du coût.

En reprenant **A*** (cf. [Études des heuristiques](heuristic_def_4.md)), puisque $$g(n)$$ est le coût actuel pour avoir atteint le noeud $$n$$, et que $$f(n) = g(n) + h(n)$$, la conséquence directe est que $$f(n)$$ ne surestime jamais le coût réel de la solution en suivant un chemin passant par $$n$$.

## Consistence
La consistence, appelée aussi **monocité**, est une propriété des heuristiques qui consiste à conserver une certaine cohérence *vis-a-vis* du problème lors de la recherche d'une solution raisonnable. Cette propriété s'applique particulièrement à certains types de problèmes, comme **A***.

Par exemple, pour **A***, l'idée est que, quelque soit $n$ et son successeur $$n'$$ obtenu par une action $$a$$, le coût estimé pour attendre l'objectif ne peut pas être plus élevé pour $$n$$ que pour $n'$ plus le coût pour aller de $$n$$ à $$n'$$. Formellement, on a une inégalité triangulaire, tel que :

$$
h(n) \leq c(n,a,n') + h(n')
$$

Cela paraît naturel et évident, car, s'il existait un chemin passant par $$n'$$ plus efficace pour aller vers l'objectif, cela violerait le principe que $$h(n)$$ est la plus petite valeur pour atteindre l'objectif. Dit autrement, on aurait pris $$n'$$ plutôt que $$n$$.

{% hint style="info" %}
Un constat également : une heuristique consistence est aussi admissible.
{% endhint %}

## Optimalité
L'optimalité consiste à montrer qu'une heuristique permet de guider la résolution du problème vers un **maximum global**, et non plus seulement vers un maximum local.

C'est une propriété complexe à observer et à étudier, en cela qu'elle est intrinsèquement liée au problème.

{% hint style="info" %}
Bien souvent, définir $$h(n)$$ de telle sorte qu'elle soit optimale requiert d'étudier le problème directement.
{% endhint %}

Dans le cas d'une exploration dans un graphe, une définition de l'optimalité peut s'exprimer comme : une heuristique admissible (ou *a fortiori* consistente), à chaque itération, sélectionne, parmi plusieurs candidats, le chemin avec le plus petit coût à chaque fois, atteint son objectif et surtout n'élague jamais les chemins optimaux (ceux qui mènent aux résultats optimaux), alors l'algorithme ne peut que finir dans un état golbalement optimal. 

{% hint style="valid" %}
Il s'agit là d'une preuve de la complexité, que l'on peut facilement construire par contradiction. L'intuition d'une telle preuve est de se dire que l'on termine l'algorithme avec un vrai coût $$T$$ supérieur à l'optimal $$S$$, et de regarder les évaluations de ces états juste avec la terminaison.
{% endhint %}

<!-- ## Exemple d'optimalité pour A*

admissibilité et consistance p96

dominance
ce que c'est
 
composition d'heurisitiques

Et si aucune ne domine ? Pas besoin d'en choisir une, il est possible de choisir la plus opti au moment opportun en créeant une heuristique dite composite. h(n)=max(h1...hm). Par transitivité, l'heuristique composite est elle aussi transitive et consistante. Enfin, en toute logique, h est dominante. -->