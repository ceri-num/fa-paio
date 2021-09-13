# Apprentissage par renforcement

L'apprentissage automatique consiste à rendre un logiciel capable d'apprendre par lui-même. Dans le cadre qui nous intéresse, le logiciel doit apprendre un comportement dynamique à adopter et en renforçant ces connaissances avec sa propre expérience. 

- [Support (PDF)](https://raw.githubusercontent.com/ceri-num/module-DUU/master/notions/reinforcement.pdf)

### Mise en pratique:

Implémenter un "Q-Learning" sur le jeu 421.

- Initialiser un dictionnaire des Q-Valeurs.
- Mettre à jour ce dictionnaire pour chaque état croisé. ('perciece')
- Décider sur une modalité `epsilon greedy`
- Identifier dans votre cadre professionnel une problématique de prise de décision séquentielle.

Plus de détail sur la page de [Q-learning en python](./q-learning.md) proposant une aide pour une implémentation simple.

<!--
## Appréhender un système plus complexe

La difficulté ensuite consiste à d'appréhender des systèmes plus complexes.

Le jeu Zombie Dice par exemple est un autre jeu de dés de type "stop" and "go" ou l'évolution du jeu dépend de dés pris pris dans une réserve de dés. Il y a donc une double combinatoire sur le lancer de dés et sur leur sélection. 

* entrer dans [jeu-ZombieDice](https://replit.com/repls/@ChefProjetIA21/jeu-ZombieDice)
* Faire un **Fork** du projet **ready-ZombieDice**
* Tenter d'appliquer du qlearning sur **ZombieDice**
-->