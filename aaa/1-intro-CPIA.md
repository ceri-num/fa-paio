# Notion d'action en IA

Appréhender le modèle agent et les problématiques de prise de décision sous incertitude.


## Prise de décision sous incertitude

L'intelligence artificielle cherche par des modèles et des algorithmes à reproduire des comportements d'intelligence naturels.
Le champ de recherche en IA est extrêmement large (neuroscience, langage, sociologie, apprentissage, optimisation...), ici in s'intéresse à l'individu et aux processus rationnels lui permettant de prendre les bonnes décisions.

- [Support (PDF)](https://bitbucket.org/imt-mobisyst/lecture-d2u/raw/master/10-intro-d2u/intro-paio.pdf)


### Mise en pratique:

Les problématiques de planification et de prise de décision sous incertitude s'intéressent au système séquentiel discret.
Des systèmes décrits par un état qui évolue dans le temps, en tentant d'influencer aux mieux cette évolution.

Pour appréhender un tel système, l'idée est d'étudier un jeu simple le 421 dans une version à $1$ joueur.

**Outils**

- Sur ça propre machine avec : spyder(Anaconda), VisualStudioCode, Atom ... 
  * S'approprier une table dans la salle de TD virtuelle Discord.
  * Y inviter son binôme.
  * partager son écran (ou son espace de travail VisualStudioCode)
- Via une interface web: [replit.com](https://replit.com)
  * Créer un compte.
  * Se logger, créer un groupe et y inviter son binôme.
  * S'installer dans Discord et partager son écran.

**Comprendre le code**

Une version python du jeu est disponible via [HackaGames](https://bitbucket.org/imt-mobisyst/hackagames).
Un [tuto](https://bitbucket.org/imt-mobisyst/hackagames/src/master/doc/tuto-replit.md) vous aide a initialiser votre environnement sous _repl.it_.

Le fichier [README]() du jeu `421` vous guide ensuite pour prendre la main, apprendre à jouer et développer votre propre IA.

L'objectif ici est de générer une IA heuristique qui gagne la première IA (`firstIA.py`), avec un résultat moyen plus fort sur 1000 parties.
