# Notion d'action en IA

Appréhender le modèle agent et les problématiques de prise de décision sous incertitude.

## Introduction à la prise de décision sous incertitude

L'intelligence artificielle cherche par des modèles et des algorithmes à reproduire des comportements d'intelligence naturels.
Le champ de recherche en IA est extrêmement large (neuroscience, langage, sociologie, apprentissage, optimisation...), ici in s'intéresse à l'individu et aux processus rationnels lui permettant de prendre les bonnes décisions.

- [Support (PDF)](https://raw.githubusercontent.com/ceri-num/module-DUU/master/notions/intro-paio.pdf)


### Mise en pratique:

Les problématiques de planification et de prise de décision sous incertitude s'intéressent au système séquentiel discret.
Des systèmes décrits par un état qui évolue dans le temps, en tentant d'influencer aux mieux cette évolution.

Pour appréhender un tel système, l'idée est d'étudier un jeu simple le 421 dans une version à $1$ joueur.

Une version python du jeu est disponible [ici](https://raw.githubusercontent.com/ceri-num/module-DUU/master/codes/game421.py) que vous pouvez enregistrer sur votre machine (click droit - enregistrer sous).

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

Ouvrir le fichier *game421.py* et identifier les deux classes principales
La première **HumanAgent** implémente une interface pour un joueur humain...
La seconde **System** implémente le jeu *421*.

Idéalement, vous ne travaillez pas directement dans *game421.py*, mais dans un fichier à vous, à côté.
Dans votre fichier de travail, il vous suffit d'importer `game421.py`, et de lancer une partie (`run`) avec une interphase `HumanAgent`:

```python
import game421 as game

gameEngine= game.System()
player= game.HumanAgent()
gameEngine.run( player )
```

- Tester le jeu à travers 4 ou 5 parties.

**Joueur autonome**

L'étape suivante consiste à mettre en oeuvre une IA qui jouera de façons autonome. 
Pour ce faire, il nous faut créer notre propre joueur `MyPlayer` est redéfinir sont comportement lorsqu'il perçoit un état du jeu et surtout au moment de décider d'une action à réaliser.

Il est possible de partir de cet exemple qui chasse un *421*: 

```python
import game421 as game

# Agent as a very simple UI
class MyPlayer(game.AbsAgent) :

    def perceive(self, reachedStateStr, reward):
        self.state= reachedStateStr

    def decide(self, isValidAction ):
        stateDico= self.stateDico()
        if stateDico["D3"] == 1 :
            if stateDico["D2"] == 2 :
                if stateDico["D1"] == 4 :
                    self.action= "keep-keep-keep"
                else: 
                    self.action= "roll-keep-keep"
            else: 
                self.action= "roll-roll-keep"
        else: 
            self.action= "roll-roll-roll"

        print( "State: " + str(stateDico) )
        print( "Action: " + self.action )
        return self.action

gameEngine= game.System()
player= MyPlayer()
gameEngine.run( player )
print( "Score: " + str(player.score) )
```

- Modifier cette IA pour la rendre plus efficace (ou proposez en une autre).
- Mettre ne place une boucle pour tester 1000 fois votre IA.
