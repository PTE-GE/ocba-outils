# Trombinoscope OCBA

Annuaire visuel et organigramme de l'Office cantonal des bâtiments (OCBA, État de Genève) :
photos, fonctions, structure hiérarchique, notes personnelles.

**➡️ Ouvrir l'outil : [index.html](index.html)**

---

## ⚠️ Cette copie est vide, et c'est voulu

Le fichier publié ici ne contient **aucune donnée nominative** : ni nom, ni fonction, ni photo.
C'est un outil vierge, et il le restera.

Les données de l'OCBA sont des données personnelles de collaborateurs de l'État : elles ne sont
diffusées que par les canaux internes. Le fichier `trombinoscope_data.json` se récupère
**sur l'intranet**, jamais ici.

## Premier usage

1. Ouvrir [index.html](index.html) — rien à installer.
2. Récupérer `trombinoscope_data.json` sur l'intranet OCBA.
3. Dans l'outil : **🔧 Admin** (mot de passe fourni avec le fichier de données) →
   **📥 Importer → 💾 JSON** → déposer le fichier.
4. C'est tout. Les données restent sur votre poste : rien n'est envoyé nulle part.

Une fois importées, elles sont conservées le temps de la session. Pour éviter de réimporter à
chaque fois, la façon la plus simple est d'utiliser la copie complète distribuée sur l'intranet
plutôt que celle-ci.

## Ce que fait l'outil

| | |
|---|---|
| **Chercher** | plein texte sur nom, fonction, service, unité, code UO, site, responsable |
| **Filtrer** | par direction, par service, par site |
| **Voir** | quatre vues : grille, compact, liste, **organigramme** dépliable |
| **Organigramme** | Office → directions → services → secteurs → équipes, avec les codes CR/UO et les responsables |
| **Fiche** | photo, hiérarchie complète, responsable cliquable, collègues de la même unité, téléphone, courriel |
| **Annoter** | une note libre et vos propres étiquettes sur chaque personne |
| **Mémoriser** | un quiz photo → nom pour apprendre les visages, service par service |
| **Exporter** | annuaire CSV, notes CSV, données JSON, impression |

## Vos notes vous appartiennent

Chaque fiche comporte un bloc « Ma note personnelle » : un texte libre et des étiquettes que vous
définissez vous-même (renommer, supprimer, créer).

- Elles sont enregistrées **dans le navigateur de votre poste** (`localStorage`, avec repli sur
  `window.name` pour Safari en ouverture par double-clic).
- Elles ne sont **jamais transmises**, ne figurent dans **aucun** export de l'annuaire et ne sont
  visibles par personne d'autre — pas même par l'administrateur du trombinoscope.
- Elles sont rattachées au **nom** de la personne : une mise à jour de l'annuaire ne les efface pas.
- Elles s'exportent et se réimportent en CSV, pour les transporter d'un poste à l'autre ou les
  sauvegarder. À l'import, une note existante n'est jamais écrasée.

## Fonctionnement technique

Un seul fichier HTML. Aucune librairie externe, aucun CDN, **aucune requête réseau** : ouvrez la
page, coupez le réseau, tout continue de fonctionner. L'import CSV, le rapprochement des photos,
le redimensionnement des images et la construction de l'organigramme se font intégralement dans
le navigateur.

L'organigramme n'est pas codé en dur : il est reconstruit à l'exécution depuis une colonne
`hierarchie` du CSV, dont les segments sont séparés par ` › `. Il se maintient donc dans Excel.

## Pour l'administrateur

Le cycle de mise à jour, en cinq gestes :

1. **Exporter → Annuaire complet (CSV)**, l'ouvrir dans Excel ;
2. y porter les arrivées, départs, changements de fonction, téléphones, courriels ;
3. nommer les nouvelles photos **« Prénom Nom.jpg »** ;
4. **Importer → CSV** (un aperçu annonce arrivées et départs avant d'appliquer),
   puis **Importer → Photos** (dépôt multiple, rapprochement automatique sur le nom) ;
5. **Exporter → Outil complet (HTML)** et **Exporter → Données + photos (JSON)** → intranet.

Colonnes du CSV :
`nom · fonction · direction · service · unite · uo · chef · affectation · tel · email · sexe · statut · hierarchie`

Seule `nom` est obligatoire. Un modèle vierge est téléchargeable depuis l'onglet CSV de la fenêtre
d'import. Les notes personnelles des utilisateurs ne sont jamais touchées par ces opérations.

Le bouton **🗑 Vider** ramène n'importe quelle copie à l'état vierge — c'est ainsi qu'a été produit
le fichier publié ici.

## Charte graphique

Charte OCBA / DPTE du 09.08.2026 : Arial, bandeau dégradé violet → jaune-vert, blocs de titre
turquoise → vert, en-têtes de tableau `#005F73`, lignes alternées `#E8F4F7`, chiffres clés
`#1A8554`. Le rouge `#C0392B` est réservé aux postes vacants, le violet `#856EBE` à ce qui
appartient à l'utilisateur : ses notes, ses étiquettes.
