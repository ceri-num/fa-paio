# Rappel (2/2)

Les critères souvent utiliser pour évaluer la performance d'un algorithme
* Complétude : Sommes nous sûr de toujours obtenir la meilleur réponse (la **solution optimale**) lorsqu'elle existe avec l'algorithme ?
* Optimalité : Trouvons-nous lors de la résolution la solution optimale ?
* Complexité en temps : Quel est le temps nécessaire pour trouver une solution ?

{% hint style="info" %}
La complexité en temps concerne une solution, quelle qu'elle soit.
{% endhint %}

{% hint style="warning" %}
La complexité en temps est toujours considérée par rapport à une mesure de difficulté du problème ! Sinon, elle n'a aucun sens.

Généralement, le problème peut être projeté dans un graphe (ou en est un) et la manière de le modéliser se fait par la description d'états, de l'état initial, des actions, du modèle de transition et de la fonction de successeur. Aussi, l'on considère le **branching factor** (*i.e.* nombre max de successeurs d'un noeud n), la profondeur maximal pour atteindre le noeud objectif le moins éloigné et la longueur maximal du chemin dans l'espace des états.
{% endhint %}

D'autres critères peuvent cependant être utilisés, par exemple si le matériel est une considération forte la mémoire peut vite devenir un critère important (*e.g.* drones véhiculaire autonomes spatiaux) : **la complexité en espace**.

Ces critères permettent de calculer le coût de l'algorithme, notamment le **coût de l'exploration**. Il est typiquement dépendant de la complexité en temps (bien qu'il peut introduire d'autres critères comme la complexité spatiale).

Si l'on souhaite interfacer le coût encore un peu plus avec le réel, il est possible d'introduire la fonction de **coût total**, qui combine le coût d'exploration avec des propriétés du problème, notamment le coût du chemin pour la solution trouvée.

{% hint style="info" %}
Cela peut engendrer une incohérence au niveau des unités qu'ils convient alors d'homogénéiser. Par exemple, le coût d'exploration fournit un résultat en seconde, et le chemin de la solution des grammes, ou encore des mètres.
{% endhint %}
