# Produire des heuristiques de manière avancée

Outre l'approche "naturelle" pour définir des heuristiques qui consiste bien souvent à étudier le problème ou exploiter la connaissance experte que l'on peut avoir/obtenir dudit problème, il existe d'autres méthodes de production d'heuristiques. Ces méthodes, lorsque correctement réalisée, peuvent produire des résultats très efficace quant à la résolution du problème.

## Composition d'heuristiques
Bien souvent lorsque l'on produit des heuristiques, il est rare qu'une soit définie comme étant nettement la meilleure et qu'elle domine toute les autres ; à la place, certaines heuristiques fonctionnent mieux dans certains espaces du problème par rapport à d'autres.

L'avantage avec la nature des heuristiques est qu'il n'est pas besoin d'en choisir qu'une. Il est tout à fait possible de définir une fonction $$h_{max}(n)$$ qui choisit l'heuristique la plus précise pour le noeud $$n$$, tel que 

$$
h_{max}(n) = max{h_1(n),\dots,h_m(n)}
$$

Si les heuristiques de l'ensemble sont admissibles, alors $$h_max$$ l'est aussi. De plus, elle est aussi dominante de toutes les heuristiques qui la compose.

## Production d'heuristiques admissibles pour les problèmes relaxés
Soit $$P$$ un problème donné, et $$C_P$$ un ensemble de contraintes (règles) qui régissent le problème. On considère $$P'$$ comme un problème relaxé si, pour les règles $$C'_{P'}$$ de $$P'$$, on a $$C_P \subset C'_{P'}$$. Autrement dit, que le graphe de l'espace des états du problème relaxé est un sur-graphe de l'espace des états original.

{% hint style="info" %}
Par exemple, pour le taquin classique, on ne peut bouger une pièce que s'il y a une case vide. Une version relaxée du problème serait de pouvoir bouger une pièce sans restriction.
{% endhint %}

Le fait de réduire les contraintes sur le problème a pour effet de créer des arêtes supplémentaires dans l'espace des états (*i.e.* des choix supplémentaires). Conséquemment, toute solution optimale du problème d'origine est aussi une solution du problème relaxé. Pour le taquin, cela revient à créer des instances du problème avec, par exemple, la possibilité de déplacer une pièce n'importe où, ou encore si une pièce est adjacente.

{% hint style="warning" %}
Attention toutefois, même si une solution optimale du problème d'origine est aussi une solution, il peut exister de meilleurs solutions au problème relaxé.
{% endhint %}

La conséquence de tout cela est que le **coût d'une solution optimale à un problème relaxé est une heuristique admissible pour le problème original**, et vue qu'elle donne un coût exact pour le problème relaxé, elle est aussi **consistante**.

Aussi, s'il nous est possible de produire automatiquement des problèmes relaxés à partir d'un problème, il devient envisageable de produire des heuristiques admissibles -- et donc peut-être dominante -- pour le problème qui est relaxé. L'exemple le plus connus est le programme "ABSOLVER" qui trouvas la première heuristique utile pour le problème du Rubik's cube en utilisant principalement cette méthode. Si vous êtes curieux, c'est [ici que ça se passe](http://web.mit.edu/6.034/wwwbob/absolver.pdf).

## Production d'heuristiques admissibles à partir de sous problèmes: bases de données de motifs
Dans cette situation, nous partons d'un sous-problème du problème originel que nous allons résoudre. En faisant cela, on obtient une limite inférieur du coût du problème originel.

L'idée derrière les bases de données de motifs est de stocker le coût de chacun de ces sous-problèmes et de toutes les instances possibles de chacun de ces sous-problèmes.

Ensuite, il suffit de produire une heuristique admissible $$h$$ simplement en recherchant la configuration correspondante du sous-problème que l'on rencontre dans le problème que l'on tente de résoudre.

{% hint style="danger" %}
Attention toutefois au recouvrement des motifs que vous stocker dans votre base de motifs. Ils ne doivent pas être dépendant d'autres instances. Par exemple pour le taquin, l'on ne veut pas stocker à la fois des motifs concernant un sous problème où il faut bien mettre les pièces 1-2-3-4 et un autre sous problème où il faut bien mettre les pièces 6-7-8-9. En effet, il y a de grande chance que le déplacement des pièces 1-2-3-4 affectent les autres pièces : cela serait au final contre productif.
{% endhint %}

{% hint style="info" %}
Les bases de motifs disjoints apportent une solution à ce problème. Rapidement, il s'agit de créer un sous-problème qui n'est pas effecter par le recouvrement. Soit par la construction, soit par l'évaluation.
{% endhint %}

## Apprentissage d'heuristique à partir de l'expérience
L'idée ici est de partir du postulat qu'à chaque résolution du problème, chaque instance résolue contient, ou peut contenir, plus ou moins de connaissances pour aider aux résolutions subséquentes. À partir de ces exemples produits, on utilise un algorithme d'apprentissage qui pour construire une fonction $$h(n)$$ qui pourra peut être prédire des coûts de solution.

Ces méthodes d'apprentissages inductifs fonctionnent bien quand le problème dispose de caractéristiques saillantes permettant de prédire la valeur de l'état, plutôt qu'une description brute de l'état.

{% hint style="info" %}
Par exemple, le nombre de tuiles mal placées au taquin est une caractéristique intéressante, *a contrario* de la position de toute les tuiles et de l'état but.
{% endhint %}

Chaque caractéristique $$x$$ intervient ainsi dans la fonction heuristique, et peut avoir un poids plus ou moins important, qui se retrouve affiné au fur et à mesure de l'expérience de l'algorithme. Une approche classique consiste à avoir recourt à une combinaison linéaire des caractéristiques, tel que :

$$
h(n) = \omega_1 x_1(n) + \dots + \omega_m x_m(n)
$$

Attention toutefois, une telle heuristique n'est pas forcément admissible, ni consistante.

<!-- composition d'heuristique

p113 + un peu d'histoire Un peu d'actualité (le pb des N reines et la nouvelle borne mathématique, principe de compartimentation d'espace, etc)
Production automatique d'heuristique
    ABSOLVER p112
    BIBI'S idea? Avec Jérémie, nous réfléchissons à des approches logiques pour créer de nouvelles heuristiques représentatives du domaine.
Apprentissage d'heuristique à partir de l'expérience
    p 114 -->
