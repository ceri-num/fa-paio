# The Curse of Dimensionality

## Support PDF

* [Le fléau de la dimension](https://bitbucket.org/imt-mobisyst/lecture-d2u/raw/master/30-the-curse/fa32-factorized-model.pdf)

## To-Do

Tenter d'appliquer QLearning sur le jeu **Risky**.

### Version 'board-4'

- Comprendre le jeu (ie. jouer).
- Réfléchir (sur papier) à une première réduction du nombre d'actions (les moves)
- Implémenter le Q-Learning

### Version 'board-4'

- Tester le jeu (ie. jouer).
- Réfléchir (sur papier) à un premier arbre de décision
- Implémenter une première version de Q-Learning factoriser

<!--
* sur [replit.com](https://replit.com/repls/@ChefProjetIA21/jeu-ZombieDice)

1. Appréhender le jeu en jouant.
2. Lancer QLearning avec des paramètres cohérents...
3. chercher à accélérer l'apprentissage.

Astuce: il est possible de sauver et recharger simplement un dictionnaire avec `json`

```python
import json
f = open("qvalues.json", "w")
f.write( json.dumps( qvalues, sort_keys=True, indent=2) )
f.close()

f = open("qvalues.json", "r")
qvalues= AgentPi( json.loads( f.read() ) )
f.close()
```
-->

