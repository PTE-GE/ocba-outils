# Revue de projets — Reporting PTE

Outil de revue et de reporting des projets du programme de transition écologique
(DPTE/OCBA). Il répond à une question : **où en sont les projets, d'un seul coup
d'œil, du programme jusqu'au sous-site ?**

## Utilisation

1. Ouvrir `revue-projets.html` dans un navigateur (aucune installation requise).
2. Glisser le classeur `Plan_PTE.xlsx` dans la page. Un seul fichier alimente l'outil :
   référentiel des sous-sites (feuille `Plan_PTE`), objectifs du programme et extraction
   GE-Invest en quatre feuilles reliées par le `Numéro` du projet (`GEI_Projets`,
   `GEI_Jalons`, `GEI_Risques`, `GEI_Livrables` ; l'ancienne feuille `GEI_Suivi` reste lue).
   Un classeur importé dans l'accueil Pilotage PTE est repris, ou proposé quand la revue a
   déjà ses propres données.
3. Deux CSV facultatifs : `decisions.csv` (registre des décisions ré-importé de revue en
   revue) et `priorisation.csv` (rangs exportés par l'outil de priorisation).

## Extraction GE-Invest

- L'extraction est lue comme l'état complet du programme : un projet absent de la
  nouvelle extraction est retiré de la revue. La liste s'affiche à l'import et dans
  l'onglet Données ; les décisions du projet sont gardées et reviennent avec lui. À partir
  de 20 % de projets retirés, l'avis passe en orange : l'extraction est peut-être incomplète.
- Extraction vide, feuille absente, numéro présent dans les jalons, risques ou livrables
  sans ligne dans `GEI_Projets`, numéro en double, colonne clé vide pour tous les projets :
  signalés à l'import. Une extraction dont aucun projet n'est relié à un sous-site
  (`Objet (actif)` vide ou sans numéro d'objet) est refusée. Une extraction non lue ne
  retire rien : l'import précédent est gardé, et la pastille le dit.
- Projets rattachés à aucun sous-site : comptés à l'import et dans l'onglet Données ; au-delà
  de 20 % des projets, l'avis et la pastille passent en orange.
- Année de référence financière absente d'un projet : celle des autres lignes, signalée.

## Ce que montre le Reporting

- **Programme → Portefeuille → Sous-site → Projet**, avec fil d'Ariane ; les projets sont
  regroupés par sous-site (bâtiment), avec repérage des sous-sites qui portent plusieurs
  projets.
- Situation financière pluriannuelle (réalisé, prévisions, crédit voté), chaîne
  **Estim PTE → Devis général → Crédit GE-Invest** avec écarts, performance déclarée,
  jalons par sous-site et par projet, planning par famille d'intervention.
- Fiche projet imprimable (description GE-Invest et commentaires des jalons compris ; le
  N° GE-Invest ouvre la fiche du projet dans GE-Invest, sur l'intranet de l'État),
  portefeuille, parc, complétude des données.

## Fonctionnement

Tout se passe **dans le navigateur**, lecture du `.xlsx` comprise (lecteur commun des
outils, sans bibliothèque externe ni CDN). Aucune donnée métier n'est embarquée dans le
fichier HTML, et aucune n'est envoyée à un serveur, sauf les saisies partagées que la
personne choisit d'envoyer au serveur des saisies. Les données importées restent dans le
navigateur (IndexedDB ; décisions dans le stockage local) ; la corbeille, à côté de l'état
des données, les efface.

Version : v0.37 — 27.10.2026 (historique : lien de version en pied de page). Testée par une
suite de 667 contrôles automatisés (dépôt de travail interne).
