# La poule qui chante — Ciblage de pays pour l'export international

Analyse exploratoire visant à identifier des groupements de pays pertinents pour orienter la stratégie d'export de poulets de l'entreprise La poule qui chante.

---

## Contexte / besoin métier

Patrick, PDG de La poule qui chante et ancien Data Analyst, souhaite engager l'entreprise dans une stratégie d'expansion à l'international. La première étape de cette démarche consiste à proposer une analyse des groupements de pays qui pourraient être ciblés pour l'export de poulets. Une étude de marché plus approfondie sera menée dans un second temps, une fois des pays ou groupes de pays prioritaires identifiés.

La mission est menée en autonomie complète : choix des données à mobiliser, choix du langage (R ou Python) et de la méthode d'analyse sont laissés à l'appréciation du Data Analyst.

## Données (source, qualité, limites)

**Sources :** 9 variables collectées et fusionnées à partir de plusieurs fichiers open data (FAO et autres) : population, disponibilité en volaille, PIB par habitant, stabilité politique, inflation, index d'ouverture commerciale, index logistique, balance commerciale, distance à la France.

**Couverture par source avant fusion (nombre de pays renseignés) :**

| Source | Pays couverts |
|---|---|
| PIB par habitant | 266 |
| Inflation | 266 |
| Ouverture commerciale | 265 |
| Population | 246 |
| Distance à la France | 225 |
| Stabilité politique | 218 |
| Disponibilité en volaille | 206 |
| Balance commerciale | 187 |
| Index logistique | 174 |

**Qualité :** après fusion des 9 sources, l'échantillon exploitable en analyse (lignes sans valeur manquante sur l'ensemble des variables) se réduit à **106 pays** — l'objectif de 100 pays est atteint de justesse, mais la couverture en % de la population mondiale n'a pas été vérifiée dans le notebook et reste à confirmer.

**Limites :**
- Le seuil de « 60 % de la population mondiale » fixé au départ n'a pas été explicitement recalculé sur l'échantillon final de 106 pays.
- Le cadre PESTEL n'est que partiellement couvert par les 9 variables retenues : les dimensions Politique, Économique, Technologique et Sociale sont représentées, mais aucune variable Environnementale ou Légale n'a été intégrée.
- La combinaison de 9 sources différentes implique un risque d'hétérogénéité (années de référence, définitions) qui n'est pas explicitement documenté dans le notebook de nettoyage.

## Démarche (choix, outils, étapes)

1. Collecte et fusion des 9 variables issues de plusieurs fichiers open data, sur la base d'une clé pays commune (`Zone`/`ISO3`).
2. Cadrage PESTEL des variables retenues : Politique (stabilité politique), Économique (disponibilité volaille, PIB/habitant, inflation, balance commerciale), Technologique (index logistique), Sociale (population, PIB/habitant, disponibilité volaille).
3. Nettoyage des données : transformation logarithmique (log1p) des variables à distribution asymétrique (population, PIB/habitant, stabilité politique, inflation, distance, ouverture, disponibilité volaille), suppression des lignes incomplètes → échantillon final de 106 pays.
4. **Exploration des données** dans un premier notebook dédié au nettoyage.
5. **ACP** (notebook séparé) : standardisation des variables, réduction à **4 composantes** retenues sur les 9 variables initiales, analyse du cercle des corrélations et de la projection des individus (pays).
6. **Choix du nombre de clusters** via la méthode de la silhouette, testée de k=2 à k=11.
7. **Clustering k-means** à k=4, puis caractérisation de chaque cluster par ses moyennes sur les variables d'origine.
8. Construction d'un score composite (variables centrées-réduites) pour classer les pays candidats des clusters les plus intéressants, et sélection finale de 3 pays selon des critères métier (proximité géographique, niveau de développement, stabilité politique, risque).

**Outil :** Python (pandas, scikit-learn, seaborn/matplotlib), dans deux notebooks séparés (nettoyage, puis ACP/clustering).

## Résultats + impact / recommandations

- **ACP** : les 9 variables sont réduites à 4 composantes principales, expliquant environ **80,3 %** de la variance totale (D1 : 38,2 %, D2 : 21,3 %, D3 : 11,5 %, D4 : 9,3 %).
  - **D1** est structuré par le PIB/habitant, la stabilité politique, l'index logistique et l'ouverture commerciale — un axe de « développement/attractivité économique ».
  - **D2** est dominé par la population.
  - **D3** est presque exclusivement porté par la balance commerciale.
  - **D4** est presque exclusivement porté par l'inflation.
- **Méthode de la silhouette** : le meilleur score est obtenu à k=2 (0,357), mais l'analyse retient finalement **k=4 clusters** (score 0,268) pour une lecture plus fine des groupes de pays — un choix qui mériterait d'être justifié explicitement dans le rendu final.
- **4 clusters obtenus**, contrastés notamment sur le PIB/habitant moyen : environ 3 400 $ (cluster 1) à 45 550 $ (cluster 3), et sur la disponibilité en volaille moyenne (de 170 000 à plus de 3,8 millions selon le cluster).
- **Pays candidats les mieux notés** (score composite combinant PIB/habitant, stabilité politique, ouverture, index logistique, balance commerciale et proximité) : Luxembourg, Suisse, Allemagne, Singapour, Irlande, Danemark, Autriche, Suède, Norvège, Émirats arabes unis.
- **3 pays retenus au final**, parmi deux clusters jugés les plus intéressants, sur la base de critères combinés : proximité géographique avec la France, niveau de développement et pouvoir d'achat élevés, stabilité politique, risque faible — les mieux placés sur ces critères parmi le top 10 étant Luxembourg, Suisse et Allemagne.
- **Impact attendu :** fournir à Patrick une base analytique objective pour orienter le choix des pays sur lesquels concentrer l'étude de marché approfondie à venir.

## Limites + prochaines pistes

- Cette analyse reste exploratoire et macro (niveau pays) ; elle ne remplace pas l'étude de marché plus fine prévue dans un second temps (acteurs locaux, réglementation import spécifique, concurrence).
- Le choix de k=4 clusters plutôt que k=2 (suggéré par le score de silhouette) reste à documenter/justifier pour la présentation finale.
- La couverture en % de la population mondiale de l'échantillon final (106 pays) n'a pas été vérifiée ; à calculer pour confirmer que l'objectif initial de 60 % est bien atteint.
- Le cadre PESTEL pourrait être complété par des variables environnementales et légales (ex. réglementation sanitaire à l'import, empreinte carbone du transport) pour une lecture plus complète du risque pays.

---

*Projet réalisé dans le cadre de la mission Data Analyst chez La poule qui chante, sous la responsabilité de Patrick, PDG.*
