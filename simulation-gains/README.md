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
6. Avant de partager ou de committer ce fichier (dépôt Git, envoi par mail) : bouton
   **« Purger les données »**, qui efface l'import conservé localement et remet l'outil à
   l'état vierge.

## Fonctionnement

Tout le calcul se fait **dans le navigateur** (JavaScript, SheetJS **intégré** au fichier —
pas de CDN). Aucune donnée n'est envoyée à un serveur, aucune donnée métier n'est intégrée au
fichier HTML lui-même. Le fichier peut donc être stocké publiquement (GitHub) sans exposer de
données de bâtiments.

Une copie locale de la dernière donnée importée est conservée dans le stockage du navigateur
(`localStorage`) pour éviter de réimporter le fichier à chaque ouverture — elle reste sur la
machine de l'utilisateur et n'est jamais transmise.

La page lit les colonnes de `Plan_PTE` **par leur nom**, jamais par leur position, et accepte
indifféremment l'ancien classeur (colonnes « corrigée (temp) ») et le classeur optimisé (où
elles ont été supprimées). Si les colonnes calculées (SRE, IDC, consommation) ne sont pas à
jour dans le fichier ouvert (classeur non réenregistré depuis sa dernière modification), la
page reconstruit les valeurs depuis les onglets sources (`Requete_OCEN_ETAT_IDC`,
`Consommation_SITG`) et l'annonce à l'écran.

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
