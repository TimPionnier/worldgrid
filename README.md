# 🌍 WorldGrid

Le mini-jeu géographique **quotidien** sur les pays du monde, inspiré de [hexagrid.fr](https://hexagrid.fr/) et [geogridgame.com](https://geogridgame.com).

**➡️ Jouer : https://timpionnier.github.io/worldgrid/**

## Règles

Chaque jour à minuit (heure de Paris), une nouvelle grille 3×3 — la même pour tout le monde. Remplissez-la avec **9 pays** (parmi 195) : chaque case doit respecter le critère de sa ligne **et** celui de sa colonne. Un pays ne peut servir qu'une seule fois, et on ne joue qu'une partie par jour. La progression est sauvegardée automatiquement (localStorage).

### Score (max 1000 pts)

Une **règle du jour** est tirée parmi 20 (pays le plus vaste, le moins peuplé, le plus au nord, le plus proche de Paris, le plus de langues officielles, le drapeau le moins coloré…).

- **Bonne réponse** : 100 pts pour la meilleure réponse selon la règle, décroissance linéaire jusqu'à 40 pts. Ex æquo = mêmes points.
- **Bonus** : +10 pts par ligne ou colonne complétée, +40 pts pour la grille entière.
- **Erreur** : −10 pts.
- Un **score parfait de 1000 pts est toujours possible** : le générateur garantit qu'il existe 9 pays distincts valant chacun 100 pts.

Chaque case vide affiche le nombre de réponses encore possibles (2 à 25) — commencez par les cases les plus contraintes. Les solutions détaillées (valeur, points, carte du monde par case) ne sont révélées qu'en fin de partie, et un bouton **Partager** copie le résultat en emojis (🟩🟨⬛) sans divulgâcher les réponses.

## Critères (68)

Continents, hémisphères, pays traversés par l'équateur, enclavés ou insulaires, littoraux (Méditerranée, Atlantique, Pacifique, Indien), superficie, population, membres de l'UE, monarchies, capitales, drapeaux (couleurs, armoiries, soleil/étoile), noms…

### Conventions

- **Océans** : les mers fermées ou semi-fermées (Caraïbes, mer du Japon, mer de Chine méridionale, mer Rouge, golfe Persique, Baltique…) sont distinctes des océans ; les mers marginales ouvertes (mer de Corail, mer d'Arabie, mer du Nord…) en font partie. La Jamaïque ne borde donc pas l'Atlantique, ni le Vietnam le Pacifique.
- **Distances** : mesurées de Paris au point le plus proche du pays (frontière ou côte). **Latitudes** : au point le plus extrême du pays (France limitée à la métropole).
- **Drapeaux** : versions couramment affichées (règle trivia) — le Pérou est uni, la Bolivie porte ses armoiries.

## Technique

- **Un seul fichier** : `index.html` (~250 Ko), aucun backend, aucune dépendance. La grille quotidienne est dérivée de la date (seed déterministe), donc identique pour tous sans serveur.
- Données : [world-countries](https://github.com/mledoze/countries) (ODbL) + population ([country-json](https://github.com/samayo/country-json)).
- Couleurs des drapeaux : analyse pixel des SVG officiels ([flag-icons](https://github.com/lipis/flag-icons)) — pixels solides uniquement (anticrénelage exclu), validée contre une liste de référence.
- Carte du monde : [world-atlas](https://github.com/topojson/world-atlas) 110m projeté en Natural Earth (d3-geo), micro-États en points.
- Distances/latitudes : calculées sur les polygones réels (arêtes sous-échantillonnées tous les 0,25°).
- Génération : tirage de critères + double validation par couplage (grille solvable **et** 1000 pts atteignable), max 25 réponses par case.

### Sources de build (optionnelles)

`builddata.py` (dataset pays) → `computegeo.js` (distances/latitudes) → `build.py` (assemblage de `index.html` depuis `template.html` + `gamelogic.js` + `gamedata.json` + `mapdata.json`).

## Déploiement

```bash
git init && git add index.html README.md
git commit -m "WorldGrid"
git branch -M main
git remote add origin https://github.com/TimPionnier/worldgrid.git
git push -u origin main
```

Puis **Settings → Pages → Source : branche `main`, dossier `/ (root)`**.

## Licence

Code libre d'utilisation. Données pays sous licence [ODbL](https://opendatacommons.org/licenses/odbl/1-0/) (world-countries).
