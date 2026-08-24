# Priorisation PTE — par quoi commencer pour atteindre 2030

Outil de priorisation et d'arbitrage du parc immobilier de l'État pour le programme de la
transition écologique (OCBA, loi 13210). Il répond à une question : **par quoi commencer pour
atteindre les objectifs 2030, au meilleur coût ?**

## Utilisation

1. Ouvrir `priorisation-pte.html` dans un navigateur (aucune installation requise).
2. Cliquer **Importer** et choisir `Plan_PTE_optimise.xlsx` (ou `Plan_PTE.xlsx`). Un seul
   import alimente les six onglets.
3. Au premier usage, une **visite guidée** de 18 étapes se lance ; elle est relançable à tout
   moment par le menu **☰ → Visite guidée**.
4. Avant de partager ou de committer ce fichier (dépôt Git, envoi par mail) : menu
   **☰ → Réinitialiser les données**, qui efface tout ce qui a été importé et remet l'outil à
   l'état vierge.

## Fonctionnement

Tout le calcul se fait **dans le navigateur** : lecture du `.xlsx` comprise, par un lecteur
ZIP + XML écrit à la main et intégré au fichier — aucune librairie externe n'est nécessaire
pour importer, classer ou arbitrer. Aucune donnée n'est envoyée à un serveur, aucune donnée
métier n'est intégrée au fichier HTML lui-même.

Deux librairies sont chargées depuis un CDN pour l'**affichage seul** : Plotly (quatre
graphiques de l'onglet Classement) et Leaflet (fond de carte). Si le réseau les bloque,
l'outil le signale par un bandeau et **tout le reste continue de fonctionner** — import,
classements, arbitrage, phasage et graphiques de trajectoire, qui sont dessinés en SVG natif.

Une copie locale de la dernière donnée importée est conservée dans le stockage du navigateur
(`localStorage`) pour éviter de réimporter le fichier à chaque ouverture — elle reste sur la
machine de l'utilisateur et n'est jamais transmise.

Les données d'exemple affichées avant tout import sont **entièrement fictives** (« Château
Courant d'Air », « Villa Passoire Thermique »…) : aucun bâtiment, aucune adresse et aucun nom
de collaborateur réels ne figurent dans le fichier.

## Les six onglets

- **Vue d'ensemble** — huit indicateurs sur une ligne : CO₂, thermique, électricité, eau,
  renouvelable, photovoltaïque, végétalisation, développement durable. Chaque tuile porte la
  valeur mesurée du parc, la cible 2030 et le chemin parcouru depuis la référence 2005 ; le
  segment clair de la barre est ce que le portefeuille arrêté ajouterait. Cliquer une tuile
  ouvre sa trajectoire.
- **Classement** — objectif par objectif, du **coût de l'unité gagnée** le plus faible au plus
  élevé (CHF par kg de CO₂, par kWh, par m³…), sur la durée de vie retenue. La ligne encadrée
  de vert est le **rang de franchissement** : celui où le cumul des gains atteint la cible 2030
  si l'on finance dans cet ordre. Cliquer une ligne déplie la fiche du bâtiment.
  La **végétalisation** fait exception : une cour d'école n'a pas de durée de vie au sens
  énergétique, on n'y achète pas un flux annuel mais une surface, une fois. Elle se classe donc
  au **coût du m² créé**, du moins cher au plus cher, sans actualisation ; le rang de
  franchissement garde le même sens.
- **Arbitrage** — ce qu'une enveloppe permet réellement : portefeuille optimisé sous contrainte
  d'enveloppe et de plafond annuel, étalé année par année, prix de la tonne de CO₂ évitée par
  tranche et par politique publique, comparateur A/B de deux portefeuilles.
- **Carte** — localisation des sous-sites, filtres du classement appliqués.
- **Données** — ce qui manque et ce que cela empêche de calculer : anomalies détectées dans les
  séries annuelles, colonnes qui bloquent les classements, alertes bâtiment par bâtiment, taux
  de remplissage, liste des sous-sites retenus et écartés.
- **Méthode** — d'où vient chaque chiffre, comment il est calculé, et ce que l'outil ne peut
  pas dire.

## Ce que les chiffres ne voient pas

Choix politique, urgence, vente prévue, contrainte patrimoniale : la fiche de chaque bâtiment
porte un bloc **Facteur non mesurable** qui permet de le remonter, de le descendre, de
l'imposer en tête ou de l'exclure, **avec motif obligatoire**. L'ajustement ne modifie jamais
la donnée — il déplace le bâtiment dans le classement, le rang arithmétique d'origine reste
affiché à côté du nouveau.

Ces ajustements et les notes s'exportent dans un **même fichier CSV**, qui s'ouvre dans Excel :
on peut le compléter hors de l'outil, l'envoyer à un collègue, récupérer le sien, fusionner les
deux, puis le réimporter. C'est ainsi qu'on partage sans droit d'écriture sur le classeur.

## Réglages

Menu **☰ → Paramètres de calcul** : durée de vie retenue (40 ans par défaut), productible
photovoltaïque, cible d'intensité thermique, poids des cinq volets de l'indice développement
durable. Rien n'est figé dans le code ; les valeurs actives sont rappelées dans l'onglet
Méthode et mémorisées dans le navigateur.

Menu **☰ → Affichage** : mode nuit, mode présentation (chiffres agrandis pour la projection).

## Source des données

Classeur `Plan_PTE_optimise.xlsx` (ou `Plan_PTE.xlsx`), cinq onglets :

| Onglet | Ce qu'il apporte |
|---|---|
| `Plan_PTE` | une ligne par sous-site : SRE, IDC actuel et projeté, variante CECB+, agent de chauffage actuel et prévu, montants, patrimoine, portefeuille, surface végétalisée à créer et son coût TTC |
| `Objectifs PTE` | références 2005 et pourcentages de réduction, la cible de végétalisation 2030, puis la série annuelle du suivi officiel |
| `Consommation par site` | totaux recalculés bâtiment par bâtiment, 2017 → dernière année fiable, surfaces comprises |
| `Data` | facteurs d'émission CO₂ par agent énergétique |
| `Tableau_de_suivi_CECB` | IDC, IDE et CO₂ projetés de la variante retenue |

Ces fichiers restent dans `01_Donnees` — ils ne sont jamais copiés dans ce dépôt.

## Limites connues

- **Deux séries annuelles coexistent et ne disent pas la même chose.** `Objectifs PTE` porte le
  suivi officiel depuis 2005 : c'est lui qui fixe la référence, donc la cible. `Consommation par
  site` donne le total recalculé bâtiment par bâtiment depuis 2017 : c'est lui qui mesure
  l'écart restant. Les deux ne coïncident pas exactement — périmètres et méthodes de relevé
  diffèrent. Sur les graphiques, la courbe pleine est le suivi officiel, le cercle isolé le
  total recalculé, et le trait pointillé qui les relie signale un **changement de source**, pas
  une évolution mesurée. Aucune des deux n'est corrigée par l'autre.
- **Certaines années sont écartées automatiquement** quand une colonne annuelle est identique à
  celle de 2017 (série recopiée) ou polluée par une autre série. L'écart est signalé dans
  l'onglet Données plutôt que noyé dans un total.
- **Électricité et eau ne reposent pas sur la même qualité de donnée** que le CO₂ et le
  thermique : ceux-ci viennent du calcul CECB+ complet, celles-là d'une contribution chiffrée
  héritée de l'ancienne méthode par familles, jamais recalculée depuis un audit.
- **Le montant retenu dépend du référentiel choisi** dans le menu « Montants » (Estim PTE,
  Invest ImmOBA, GE-Invest). Les trois n'ont ni le même nombre de bâtiments chiffrés ni les
  mêmes montants : en changer recalcule tous les classements, et l'ordre n'est pas le même.
- **Un bâtiment sans coût n'est pas classable.** Ce n'est pas l'argent qui limite le résultat
  2030 mais la donnée : l'onglet Données indique quelles saisies débloqueraient le plus de
  bâtiments.
- **Les surfaces végétalisées sont à créer, pas créées.** La colonne du classeur porte ce que
  les projets ajouteraient ; rien n'y est compté comme réalisé. L'écart à combler est donc
  l'objectif entier, et le pourcentage affiché sur la tuile dit seulement quelle part de la
  cible les projets déjà repérés couvriraient s'ils étaient tous financés.
- L'indice **développement durable** est en place mais la plupart de ses colonnes sources ne
  sont pas encore renseignées ; il affiche donc une couverture de données partielle.
