# Model-Based Learning

On souhaite maintenant apprendre un modèle de l'évolution de notre système, de façon à pouvoir résonner dessus et planifier les actions à réaliser.

- Model-Based-Learning - [Support (PDF)](https://bitbucket.org/imt-mobisyst/lecture-d2u/raw/master/20-reinforcement/rl-on-421.pdf)


## Apprendre le Modèle :

On va chercher à apprendre l'évolution au 421:

Il faut dans un premier explorer l'environnement, ie tester toutes les actions suffisamment de foi pour générer une connaissance statistique de l'évolution du système et ceux depuis chaque état atteignable.

Bref c'est laborieux, ici vous pouvez utiliser la trace suivante: [log de 1000 transitions par couple états-actions au 421](https://bitbucket.org/imt-mobisyst/lecture-d2u/raw/master/ressources/log1000-421.txt) (attention fichier de 45 Mega).

pour le copier localement: 

```sh
curl https://bitbucket.org/imt-mobisyst/lecture-d2u/raw/master/ressources/log1000-421.txt \
 > log1000-421.txt
```

Le fichier est structuré par ligne : "état-de-départ action état-atteint récompense" séparé donc par des espaces.

Sur la base de ce fichier (et en utilisant les dictionnaires python):

- Générer la fonction de récompense - une structure qui stocke la valeur moyenne d'exécuter une action depuis un état donné.
- Générer la fonction de transition - une structure qui stocke une structure avec la liste des états atteignables couplée à la probabilité de les atteindre (typiquement un dictionnaire de dictionnaires de dictionnaires).

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

```python
def actions(transition, s)
    return list(transition[s].keys())

def valueIteration( transition, reward, gamma= 0.99, epsilon= 0.01):
    pi= { s: actions(transition, s)[0] for s in transition }
    values= { s: 0.0 for s in transition }
    maxDiffValue= epsilon + 1
    while maxDiffValue > epsilon :
        # initialize iteration values
        maxDiffValue= 0.0
        newValues= { s: 0.0 for s in transition }
        # for each state
        for s in transition :
            newValues[s]= BelmanValueOf(transition, reward, s, pi[s], values, gamma)
            # search the best couple action/value
            for a in transition[s] :
                aValue= BelmanValueOf(transition, reward, s, a, values)
                if aValue > newValues[s] :
                    newValues[s]= aValuee
                    pi[s]= a
            # keep the maximal gain
            if abs( bestValue - values[s]  ) > maxDiffValue :
                maxDiffValue= abs( bestValue - values[s]  )
        # end the iteration.
        values= newValues
    # Return the tuple policy and its associated values.
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

<!--
## Correction :

Un agent *model-learner*: [https://raw.githubusercontent.com/ceri-num/module-DUU/master/codes/playerMDP.py](playerMDP.py).

Attention cependant, pour gagner du temps dans le main, il n'apprend pas en jouant, mais en interrogeant le moteur du jeu.
-->
