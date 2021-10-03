# Passer à l'échelle

Passer à l'échelle qui sous-tend l'application d'une approche dans un cadre concret est le nerf de la guerre.
Il passe nécessairement par la factorisation de modèle notamment dans le cadre du Q-Learning.

* [Le fléau de la dimension](https://raw.githubusercontent.com/ceri-num/module-DUU/master/notions/the-curse.pdf)

# Passer à l'échelle

Tenter d'appliquer QLearning sur le jeu [ZombieDice](../games/zombie.md).

- **1** - accélérer l'apprentissage en réduisant fortement l'espace d'état dans `qvalues`, sur la base de l'implémentation d'un arbre de décision.

[gameZombie.py (1 players)](https://raw.githubusercontent.com/ceri-num/module-DUU/master/codes/gameZombies.py)

*Astuce :* décomposer l'état:

```python
def stateDico( self, state ):
    stVector= state.split("-") # [ "1", "2", "Hard(gun)" .... ]
    stDico= {
        "Brain":  (int)(stVector[0]),
        "Shot":   (int)(stVector[1]),
        "D1":     stVector[2],
        "D2":     stVector[3],
        "D3":     stVector[4],
        "Easy":   (int)(stVector[5]),
        "Medium": (int)(stVector[6]),
        "Hard":   (int)(stVector[7])
    }
    return stDico
```

*Astuce :* recomposé une clé pour le dictionnaire:

```python
    key= str(stDico["Brain"]) + "-" + str(stDico["Brain"])
```

- **2** - opérer un transfert de connaissance en complexifiant l'arbre d'une itération à l'autre.

- **3** - aller plus loin en passant sur la version 2 joueurs

Deux joueurs s'affrontent:

```python
gameEngine= game.System()
player= game.HumanAgent()
gameEngine.run(player)
```

Attention, l'état est complété avec les scores des deux joueurs, et la fonction de récompense ne communique une valeur qu'en fin de partie.

[gameZombie2.py (2 players)](https://raw.githubusercontent.com/ceri-num/module-DUU/master/codes/gameZombies2.py)

## Modélisation factorisé

Et maintenant passons à l'échelle dans un cadre `Model-Based`.

* [Passer à l'échelle](https://raw.githubusercontent.com/ceri-num/module-DUU/master/notions/scaling.pdf)
