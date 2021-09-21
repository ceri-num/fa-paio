# Model-Based Learning

On souhaite maintenant apprendre un modèle de l'évolution de notre système, de façon à pouvoir résonner dessus et planifier les actions à réaliser.

* [Model-Based-Learning](https://raw.githubusercontent.com/ceri-num/module-DUU/master/notions/mb-learning.pdf)


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

### Proposition d'implémentation:

First: a bellman implémentation at horizon 1 (i.e. non recursive).

```python
def BelmanValueOf( transition, reward, s, a, defaultValues, gamma=0.99 ):
    expectedGains= 0
    for sp in transition[s][a] :
        expectedGains+= transition[s][a][sp] * defaultValues[sp]
    return reward[s][a] + gamma * expectedGains
```

In this implementation:

- `transition` is a dictionary over states of dictionaries over action of dictionaries over states of values between 0 and 1.
- `reward` is a dictionary over states of dictionary over action of values.
- `s` a state, an entrance in `transition` and `reward`
- `a` an action, an entrance in `transition[s]` and `reward[s]`
- `defaultValues` a first estimation of Belleman value (a dictionary over state of values).

Second: Value Iteration:

```Python
def actions(transition, s)
    return list(transition[s].keys())

def valueIteration( transition, reward, gamma= 0.99, epsilon= 0.01):
    pi= { s: actions(transition, s)[0] for s in transition }
    values= { s: 0.0 for s in transition }
    maxDiffValue= epsilon + 1
    while maxDiffValue > epsilon :
        # for each state
        maxDiffValue= 0.0
        values= { s: 0.0 for s in transition }
        for s in transition :
            bestValue= BelmanValueOf(transition, reward, s, pi[s], values, gamma)
            # search the best couple action / value
            for a in transition[s] :
                value= BelmanValueOf(transition, reward, s, a, values)
                if value > bestValue :
                    bestValue= value
                    pi[s]= a
            if abs( bestValue - values[s]  ) > maxDiffValue :
                maxDiffValue= abs( bestValue - values[s]  )
            values[s]= bestValue
        values= values
    return pi, values
```

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
