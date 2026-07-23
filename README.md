# 🌍 WorldGrid

Le mini-jeu géographique sur les pays du monde, inspiré de [hexagrid.fr](https://hexagrid.fr/) et [geogridgame.com](https://geogridgame.com).

**➡️ Jouer : https://timpionnier.github.io/worldgrid/**

## Règles

Remplissez une grille 3×3 avec **9 pays** (parmi 195) : chaque case doit respecter le critère de sa ligne **et** celui de sa colonne. Un pays ne peut servir qu'une seule fois.

### Score (max 1000 pts)

Une **règle de partie** est tirée au sort parmi 16 (pays le plus vaste, le moins peuplé, le plus de langues officielles, le drapeau le moins coloré, la capitale au nom le plus court…).

- **Bonne réponse** : 100 pts pour la meilleure réponse selon la règle, décroissance linéaire jusqu'à 40 pts. Ex æquo = mêmes points.
- **Bonus** : +10 pts par ligne ou colonne complétée, +40 pts pour la grille entière.
- **Erreur** : −10 pts.
- Un **score parfait de 1000 pts est toujours possible** : le générateur garantit qu'il existe 9 pays distincts valant chacun 100 pts.

Chaque case vide affiche le nombre de réponses encore possibles — commencez par les cases les plus contraintes. Les solutions détaillées (valeur et points de chaque réponse) ne sont révélées qu'en fin de partie.

## Critères

70 critères générés à partir des données : continents, pays enclavés/insulaires, pays frontaliers, superficie, population, couleurs des drapeaux, langues officielles, monnaies, initiales des noms et capitales…

## Technique

- **Un seul fichier** : `index.html` (~90 Ko), aucun backend, aucune dépendance.
- Données : [world-countries](https://github.com/mledoze/countries) (licence ODbL) + population ([country-json](https://github.com/samayo/country-json)).
- Couleurs des drapeaux : analyse pixel des SVG officiels ([flag-icons](https://github.com/lipis/flag-icons)), rastérisés puis classés par teinte HSL.
- Génération de grille : tirage de critères + validation par couplage (backtracking) garantissant une grille solvable **et** un 1000 pts atteignable.
- Sauvegarde du meilleur score en `localStorage` uniquement.

## Déploiement

```bash
git init && git add index.html README.md
git commit -m "WorldGrid v1"
git branch -M main
git remote add origin https://github.com/TimPionnier/worldgrid.git
git push -u origin main
```

Puis **Settings → Pages → Source : branche `main`, dossier `/ (root)`**. Le jeu est en ligne 1 à 2 minutes plus tard.

## Licence

Code libre d'utilisation. Données pays sous licence [ODbL](https://opendatacommons.org/licenses/odbl/1-0/) (world-countries).
