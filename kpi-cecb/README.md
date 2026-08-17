# KPI CECB+ — Dashboard de suivi des projets PTE

Tableau de bord de pilotage pour le suivi des projets CECB+ du programme de la transition écologique (OCBA).

## Utilisation

1. Ouvrir `kpi-cecb-dashboard.html` dans un navigateur (aucune installation requise).
2. Glisser le dernier fichier **« MDS_suivi projets et KPI »** (`.xlsm` ou `.xlsx`) dans la zone d'import, ou cliquer pour le sélectionner.
3. Le tableau de bord se met à jour automatiquement à partir de la feuille « Tbl suivi ».
4. Pour actualiser avec un fichier plus récent : bouton **« Mettre à jour avec un nouveau fichier »** dans la barre de source.
5. Avant de partager ou de committer ce fichier (dépôt Git, envoi par mail) : bouton **« Purger les données »**, qui efface tout ce qui a été importé et remet l'outil à l'état vierge.

## Fonctionnement

Tout le calcul se fait **dans le navigateur** (JavaScript, librairie SheetJS chargée depuis un CDN). Aucune donnée n'est envoyée à un serveur, aucune donnée n'est intégrée au fichier HTML lui-même. Le fichier peut donc être stocké publiquement (GitHub) sans exposer de données métier — tant qu'il n'a pas été utilisé sans purge préalable, ou si l'on committe une version fraîchement purgée.

Une copie locale des dernières données importées est conservée dans le stockage du navigateur (`localStorage`) pour éviter de réimporter le fichier à chaque ouverture — elle reste sur la machine de l'utilisateur et n'est jamais transmise.

## Contenu du tableau de bord

- Indicateurs globaux : projets suivis, répartition par état, avancement moyen, surface SRE, mandataires actifs, engagement financier
- État d'avancement et répartition par affectation
- Respect des délais contractuels (visite, réunion post-visite, 1er rendu, rendu final) avec repérage des projets les plus en retard
- Énergie & CO₂ : gain IDC et réduction CO₂ estimée selon la variante retenue
- Charge par mandataire (projets, ETP, montant, facturation, délais)
- Détail exhaustif des projets, filtrable et triable

## Source des données

Fichier `MDS_suivi projets et KPI_AAAAMMJJ.xlsm`, feuille **« Tbl suivi »** (une ligne par site/sous-site). Ce fichier source reste dans `01_Donnees` — il n'est jamais copié dans ce dossier.

## Limites connues

- Les indicateurs financiers et de délai ne portent que sur les lignes renseignées (ex. un projet « en attente » n'a pas encore de date réelle de visite).
- Le champ « Avt » (avancement) est une estimation discrète (0 / 30 % / 60 % / 100 %) saisie manuellement — des écarts ponctuels avec le champ « État » sont possibles et signalés par l'outil (alerte de cohérence).
- Comparaison entre deux exports : l'outil affiche l'état du **dernier fichier importé**, pas un historique. Le nombre de projets peut varier d'un export à l'autre (ajouts, retraits, doublons de saisie côté source).
