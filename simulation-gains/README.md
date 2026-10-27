# Simulation des gains énergétiques — PTE

Outil de simulation de mesures d'amélioration énergétique pour un bâtiment ou groupe de
sous-sites du programme de la transition écologique (OCBA). Remplace la
`Matrice_et_calcul_complet.xlsx`.

## Utilisation

1. Ouvrir `pte-simulation.html` dans un navigateur (aucune installation requise).
2. Glisser `Plan_PTE.xlsx` (ou `Plan_PTE_optimise.xlsx`) dans la zone d'import.
3. Chercher un bâtiment, ajouter des mesures (poste, action, curseur prudent → optimiste,
   investissement), lire le résultat dans le panneau permanent : investissement, économie,
   retour, CO₂, IDC avant → après, coût du kWh économisé, coût de la tonne de CO₂.
4. Trois variantes **I / II / III** (numérotées ainsi pour ne pas les confondre avec les
   variantes A / B / C d'un CECB+) et un bouton **Comparer**.
5. Trois sorties : **Copier pour Plan_PTE**, **Exporter en Excel**, **Imprimer / PDF**.
6. La **corbeille**, à côté de l'état des données, efface les données de l'outil dans ce
   navigateur (le classeur commun de Pilotage PTE fait l'objet d'une seconde question).

## Fonctionnement

Tout le calcul se fait **dans le navigateur**. Le classeur est lu par le lecteur Excel commun
aux outils PTE, intégré à la page : aucune bibliothèque externe, aucun CDN. Aucune donnée n'est
envoyée à un serveur, aucune donnée métier n'est intégrée au fichier HTML lui-même. Le fichier
peut donc être stocké publiquement (GitHub) sans exposer de données de bâtiments.

Le classeur importé est gardé dans le stockage du navigateur (IndexedDB, à défaut
`localStorage`) pour éviter de le réimporter à chaque ouverture — il reste sur la machine de
l'utilisateur et n'est jamais transmis. Un classeur déposé sur la page Pilotage PTE s'ouvre ici
tout seul.

La page lit les colonnes de `Plan_PTE` **par leur nom**, jamais par leur position. Les
cellules en erreur sont comptées : un classeur enregistré sans recalcul est signalé, au lieu de
passer pour un classeur vide.

## Le référentiel

Facteurs CO₂ et d'énergie primaire, prix, matrice des gains, clés de répartition de
l'électricité, valeurs SIA, correspondances agent thermique et affectation → typologie : neuf
tableaux livrés avec l'outil. S'il existe un onglet « Référentiel PTE » dans le classeur
importé, la page l'utilise à sa place et le signale dans la barre de source.

## Source des données

Fichier `Plan_PTE.xlsx` (ou `Plan_PTE_optimise.xlsx`), onglets « Plan_PTE » et « Consommation
par site ». Ce fichier source reste dans `01_Donnees` — il n'est jamais copié dans ce dossier.

## Limites connues

- Les consommations sont relevées au niveau du **site**, la SRE au niveau des **sous-sites**.
  Si le périmètre sélectionné ne couvre pas tout le site, l'IDC est surestimé — l'outil
  l'affiche.
- Les clés de répartition de l'électricité sont des profils types, pas des mesures.
- Une simulation n'est pas un audit CECB+. En présence d'un CECB+, c'est lui qui fait foi.
