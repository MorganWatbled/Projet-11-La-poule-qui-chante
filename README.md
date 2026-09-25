# La poule qui chante — Ciblage de pays pour l'export international

Analyse exploratoire visant à identifier des groupements de pays pertinents pour orienter la stratégie d'export de poulets de l'entreprise La poule qui chante.

---

## Contexte / besoin métier

Patrick, PDG de La poule qui chante et ancien Data Analyst, souhaite engager l'entreprise dans une stratégie d'expansion à l'international. La première étape de cette démarche consiste à proposer une analyse des groupements de pays qui pourraient être ciblés pour l'export de poulets. Une étude de marché plus approfondie sera menée dans un second temps, une fois des pays ou groupes de pays prioritaires identifiés.

La mission est menée en autonomie complète : choix des données à mobiliser, choix du langage (R ou Python) et de la méthode d'analyse sont laissés à l'appréciation du Data Analyst.

## Données (source, qualité, limites)

**Sources :**
- Données de la FAO (Food and Agriculture Organization), fournies en point de départ.
- Données complémentaires en open data à rechercher sur la FAO, la Banque mondiale, et données mondiales, guidées par une analyse **PESTEL** (Politique, Économique, Socioculturel, Technologique, Environnemental, Légal) pour identifier les variables pertinentes.
- Objectif de constitution du jeu de données : au minimum **8 variables**, couvrant au minimum **100 pays**, représentant au moins **60% de la population mondiale**.

**Qualité :**
[À compléter : après collecte — complétude par pays et par variable, année(s) de référence des différentes sources, cohérence des unités entre FAO/Banque mondiale/données mondiales]

**Limites :**
- La combinaison de plusieurs sources open data implique un risque d'hétérogénéité (années de référence différentes, définitions de variables non alignées) à contrôler avant fusion.
- Le seuil de 100 pays / 60% de la population mondiale est un objectif à atteindre : [À compléter : préciser si atteint et les pays éventuellement exclus faute de données]
[À compléter : autres limites constatées lors de la préparation des données]

## Démarche (choix, outils, étapes)

1. Exploration des données FAO fournies comme point de départ.
2. Analyse **PESTEL** pour identifier des familles de variables complémentaires pertinentes pour l'export de poulets (ex. politique commerciale, PIB, habitudes de consommation, infrastructures logistiques, réglementation sanitaire, enjeux environnementaux).
3. Recherche et collecte des données open data correspondantes (FAO, Banque mondiale, données mondiales), jusqu'à obtenir au moins 8 variables.
4. Regroupement des différentes sources dans un fichier unique, avec harmonisation des clés pays et des formats.
5. Nettoyage des données (valeurs manquantes, doublons, cohérence des unités) pour maximiser la couverture en pays tout en visant le seuil de 100 pays / 60% de la population mondiale.
6. **Exploration des données** dans un premier notebook (Python ou R) : statistiques descriptives, distributions, premières corrélations.
7. **Analyse en composantes principales (ACP)** dans un notebook séparé, dédié à la partie analytique :
   - réduction des dimensions,
   - analyse du cercle des corrélations,
   - analyse de la projection des individus (pays).
8. **Clustering** des pays, à partir des résultats de l'ACP ou des données brutes :
   - classification ascendante hiérarchique (CAH) en premier lieu,
   - puis un k-means pour consolider/affiner les groupements obtenus.

**Outil :** [À compléter : Python ou R — choix retenu et bibliothèques utilisées, ex. scikit-learn/scipy ou FactoMineR]

## Résultats + impact / recommandations

- Un jeu de données consolidé, multi-sources, couvrant au moins 8 variables sur un large panel de pays.
- [À compléter : variables PESTEL finalement retenues et justification de leur pertinence pour l'export de poulets]
- [À compléter : lecture du cercle des corrélations — variables les plus structurantes, axes principaux de l'ACP]
- [À compléter : groupements de pays obtenus via la CAH et le k-means, avec caractérisation de chaque cluster]
- [À compléter : recommandation des groupements de pays à cibler en priorité pour l'export]
- **Impact attendu :** fournir à Patrick une base analytique objective pour orienter le choix des pays sur lesquels concentrer l'étude de marché approfondie à venir.

## Limites + prochaines pistes

- Cette analyse reste exploratoire et macro (niveau pays) ; elle ne remplace pas l'étude de marché plus fine prévue dans un second temps (acteurs locaux, réglementation import spécifique, concurrence).
- La stabilité des clusters obtenus dépendra du choix final des variables et pourra être sensible à l'ajout ou au retrait de certains pays peu documentés.
[À compléter : pistes complémentaires, ex. comparaison des résultats CAH vs k-means, test d'autres méthodes de réduction de dimension, ajout de nouvelles variables PESTEL après premiers résultats]

---

*Projet réalisé dans le cadre de la mission Data Analyst chez La poule qui chante, sous la responsabilité de Patrick, PDG.*
