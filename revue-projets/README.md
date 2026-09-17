# Revue de projets — Reporting PTE

Outil de revue et de reporting des projets du programme de transition écologique
(DPTE/OCBA). Il répond à une question : **où en sont les projets, d'un seul coup
d'œil, du programme jusqu'au sous-site ?**

## Utilisation

1. Ouvrir `revue-projets.html` dans un navigateur (aucune installation requise).
2. Glisser le classeur `Plan_PTE_optimise.xlsx` dans la zone de dépôt — un seul
   fichier alimente tout l'outil : référentiel des sous-sites, Estim PTE / DG,
   objectifs du programme et, via la feuille `GEI_Suivi`, l'extraction complète
   GE-Invest (projets, suivi, jalons, finances, risques, livrables).
3. Deux CSV optionnels : `decisions.csv` (registre des décisions ré-importé de
   revue en revue) et `priorisation.csv` (rangs exportés par l'outil de
   priorisation, dossier voisin).

## Ce que montre le Reporting

- **Programme → Portefeuille → Sous-site → Projet**, avec fil d'Ariane ; les
  projets sont regroupés par sous-site (bâtiment), dépliables, avec repérage des
  sous-sites portant plusieurs projets à consolider.
- Situation financière pluriannuelle (réalisé, prévisions, crédit voté), chaîne
  **Estim PTE → Devis général → Crédit GE-Invest** avec écarts, performance
  déclarée, **Gantt des jalons** par sous-site et par projet.
- Onglets historiques : tableau de bord sémaphores (calculés **et** déclarés,
  avec écarts), portefeuille, fiche projet imprimable, parc, complétude.

## Fonctionnement

Tout se passe **dans le navigateur** : lecture du `.xlsx` comprise (lecteur ZIP +
XML intégré, aucune librairie externe, aucun CDN). Aucune donnée n'est envoyée à
un serveur ; aucune donnée métier n'est embarquée dans le fichier HTML. Une copie
locale des données importées est conservée dans le stockage du navigateur, à
effacer via « Vider les données importées » avant tout partage du poste.

Construit et testé avec une suite de 320 tests automatisés (dépôt de travail
interne). Version : v0.7 — 16.09.2026.
