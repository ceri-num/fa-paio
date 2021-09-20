# Model-Based Learning

On souhaite maintenant apprendre un modèle de l'évolution de notre système, de façon à pouvoir résonner dessus et planifier les actions à réaliser.

<!--

* [Q-Learning on 421](https://raw.githubusercontent.com/ceri-num/module-DUU/master/notions/qlearning421.pdf)

-->

## Apprendre le Modèle :

On va chercher à apprendre l'évolution au 421:

Il faut dans un premier explorer l'environnement, ie tester toutes les actions suffisamment de foi pour générer une connaissance statistique de l'évolution du système et ceux depuis chaque état atteignable.

Bref c'est laborieux, ici vous pouvez utiliser la trace suivante: [log de 1000 transitions par couple états-actions au 421](https://raw.githubusercontent.com/ceri-num/module-DUU/master/codes/transition-log.txt) (attention fichier de 45 Mega).

Le fichier est structuré par ligne : "état-de-départ action état-atteint récompense" séparé donc par des espaces.

Sur la base de ce fichier:

- Générer la fonction de récompense - une structure qui stocke la valeur moyenne d'exécuter une action depuis un état donné.
- Générer la fonction de transition - une structure qui stocke une structure avec la liste des états atteignables couplée à la probabilité de les atteindre (dictionnaire de dictionnaires de dictionnaires par exemple).

*Notez qu'il s'agit ici d'expérimenter, et non pas de réfléchir un code efficace.*

## Planifier :

Le plus dur est fait. Il faut maintenant faire tourner un algo de résolution de MDP ('value iteration par exemple') pour calculer une politique et enfin l'exécuter dans des parties de 421.

Notez que vous pouvez stocker dans une fichier lisible votre politique implémenté comme un dictionnaire avec la librairie python 'json' :

```python
f = open("policy.json", "w")
f.write( json.dumps( policy, sort_keys=True, indent=2) )
f.close()
```

Et la recharger tout aussi simplement: 

```python
f = open("policy.json", "r")
policy= json.loads( f.read() )
f.close()
```

<!--
## Retour sur l'apprentissage au 421

Analyse du Q-Learning sur cet exemple et présentation de l'apprentissage basé modèle.

* [Model Based Learning](https://raw.githubusercontent.com/ceri-num/module-DUU/master/notions/model-based-learning.pdf)
-->
