# Priorisation PTE — par quoi commencer pour atteindre 2030

Outil de priorisation et d'arbitrage du parc immobilier de l'État pour le programme de la
transition écologique (OCBA, loi 13210). Il répond à une question : **par quoi commencer pour
atteindre les objectifs 2030, au meilleur coût ?**

## Utilisation

1. Ouvrir `priorisation-pte.html` dans un navigateur (aucune installation requise).
2. Cliquer **Importer** et choisir `Plan_PTE_optimise.xlsx` (ou `Plan_PTE.xlsx`). Un seul
   import alimente les six onglets.
3. Au premier usage, une **visite guidée** de 19 étapes se lance ; elle est relançable à tout
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

- **Vue d'ensemble** — sept indicateurs sur une ligne : CO₂, thermique, électricité, eau,
  renouvelable, photovoltaïque, développement durable. Chaque tuile porte la
  valeur mesurée du parc, la cible 2030 et le chemin parcouru depuis la référence 2005 ; le
  segment clair de la barre est ce que le portefeuille arrêté ajouterait. Cliquer une tuile
  ouvre sa trajectoire.
- **Classement** — objectif par objectif, du **coût de l'unité gagnée** le plus faible au plus
  élevé (CHF par kg de CO₂, par kWh, par m³…), sur la durée de vie retenue. Chaque ligne montre
  l'agent de chauffage actuel **et la substitution prévue** — c'est cette bascule qui produit le
  gain CO₂. La ligne encadrée
  de vert est le **rang de franchissement** : celui où le cumul des gains atteint la cible 2030
  si l'on finance dans cet ordre. Cliquer une ligne déplie la fiche du bâtiment.
  La colonne « **% de l'écart comblé** » dit, à chaque rang, quelle part de l'écart **restant**
  le cumul a couverte. Ce n'est pas le pourcentage de la tuile, qui mesure le chemin parcouru
  **depuis 2005** — voir « Deux pourcentages, deux dénominateurs » ci-dessous.
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

## Deux pourcentages, deux dénominateurs

La tuile de la Vue d'ensemble et la colonne du classement affichent toutes deux un « % », et ils
ne coïncident pas : sur le CO₂, la tuile dit **65 %** quand le classement plafonne à **37 %**.
Ce n'est pas une erreur, ce sont deux mesures différentes.

| | ce qu'il mesure | dénominateur |
|---|---|---|
| tuile | chemin parcouru depuis la référence 2005 | réf 2005 − cible 2030 |
| classement | part de l'écart **qui reste** que le cumul comble | mesuré − cible 2030 |

Les deux se composent : 65 % du chemin fait, puis 37 % des 35 % restants — **78 % du chemin
total**, ce que le panneau de trajectoire affiche par ailleurs.

L'outil ne l'explique pas par une phrase, il le **montre**. Les trois quantités sont trois
segments de la même règle, alors elles sont dessinées comme telles :

- un **ruban vertical** à droite de chaque graphique de trajectoire, calé sur l'axe des valeurs
  du graphique lui-même : la bande verte va du niveau 2005 au point mesuré, la bande foncée
  couvre la part de l'écart que les bâtiments classables comblent, les hachures le reste. Les
  repères « réf. 2005 / aujourd'hui / cible 2030 » tombent en face des frontières ;
- une **jauge horizontale** au-dessus du classement, les mêmes trois zones à plat ;


**Chaque zone se survole** et donne alors son chiffre, son dénominateur et sa phrase. Un chevron
« × 3,8 » signale un potentiel qui dépasse l'écart, un ⚠ une zone que rien ne couvre faute de
donnée.

Trois cas particuliers, tous dits explicitement :

- **Électricité et eau affichent 0 %** non parce qu'il n'y a rien à gagner, mais parce
  qu'**aucun bâtiment n'est classable** : les colonnes `Gain Electricité (Max) - kWh` et
  `Gain Eau (Max) - m3` sont vides. Une donnée absente, pas un gain nul.
- **Renouvelable et photovoltaïque** dépassent 100 % (381 % et 367 %) : leur tuile n'affiche pas
  un chemin mais un **niveau atteint** — il n'y a pas de référence 2005 pour une part — et le
  potentiel repéré vaut près de quatre fois l'écart restant. La colonne est plafonnée à 100 %
  ligne à ligne, la note donne le total.
- **Végétalisation** couvre 120 % de la cible : objectif cumulatif, rien n'est encore réalisé.

## Un même montant, plusieurs objectifs

Une rénovation CECB+ produit d'un coup un gain thermique, un gain CO₂ et une substitution
renouvelable. L'outil impute à chacun de ces trois classements le **montant complet de
l'intervention** — le même franc, compté trois fois. C'est une convention homogène, donc le tri
reste valide, mais elle a deux conséquences que l'outil affiche désormais au lieu de les laisser
découvrir.

**Le bâtiment polyvalent paraît plus cher qu'il ne l'est.** Celui qui achète trois bénéfices
porte le même coût que celui qui n'en achète qu'un, dans chacun des trois classements. Sur le
parc de test : 0,658 contre 0,402 CHF/kWh thermique, dix-sept rangs d'écart. Une pastille
**⊕n** signale ces bâtiments, ligne à ligne.

**Les montants ne s'additionnent pas d'un objectif à l'autre.** 278 + 508 + 502 = 1 288 MCHF
affichés pour 649 MCHF réellement engagés — un facteur 1,99. Un bandeau permanent le dit sous
les filtres, avec les deux chiffres et le facteur, recalculés sur le fichier chargé. Pour
raisonner à budget, l'onglet **Arbitrage** compte chaque bâtiment une seule fois.

La **végétalisation** échappe à tout cela : elle a sa propre colonne de coût dans le classeur,
donc son CHF/m² est un vrai coût par m². Le **photovoltaïque** aussi, dans l'autre sens : son
montant n'est pas isolable du coût de rénovation, d'où un classement à la puissance sans coût
unitaire. Ni l'un ni l'autre ne porte le bandeau.

Le problème porte un nom — **coûts joints**, comme la cogénération chaleur-électricité. Il n'existe
pas d'allocation « juste » : c'est un résultat démontré, pas une lacune. La seule sortie conforme à
la hiérarchie d'ISO 14044 est de **subdiviser** le montant, pas de le répartir par une clé.

### La subdivision par lot

Trois colonnes de `Plan_PTE` portent cette subdivision :

| Colonne | Alimente |
|---|---|
| `Coût lot enveloppe [CHF]` | Thermique, et la part enveloppe du CO₂ |
| `Coût lot chaufferie [CHF]` | Renouvelable, et la part substitution du CO₂ |
| `Coût lot technique [CHF]` | Électricité et Eau |

Un bâtiment qui les porte cesse d'avoir un coût partagé : son montant est celui du lot qui produit
ce gain-là, sa pastille passe au vert **⊟**, et il est comparable sans réserve. Un bâtiment qui ne
les porte pas garde le montant complet et la pastille ⊕n. La précision arrive **bâtiment par
bâtiment** : rien n'attend que le classeur soit complet, et le bandeau dit à tout moment combien de
bâtiments sont subdivisés.

## Ce que les chiffres ne voient pas

Choix politique, urgence, vente prévue, contrainte patrimoniale : la fiche de chaque bâtiment
porte un bloc **Facteur non mesurable** qui permet de le remonter, de le descendre, de
l'imposer en tête ou de l'exclure, **avec motif obligatoire**. L'ajustement ne modifie jamais
la donnée — il déplace le bâtiment dans le classement, le rang arithmétique d'origine reste
affiché à côté du nouveau.

### Exclure sans perdre de vue

`⛔ Exclu — hors programme` retire le bâtiment de tous les classements, du classement de repli,
de la vue d'ensemble et de l'arbitrage. Il ne disparaît pas pour autant : un bandeau
**⛔ Exclus du programme** s'affiche au-dessus du tableau du Classement et les rassemble tous.

Une exclusion vaut pour le **programme entier**, pas pour un objectif : le bandeau montre donc
les mêmes bâtiments quel que soit le classement à l'écran, et **aucun filtre de la barre ne peut
l'amputer** — un bâtiment qu'un filtre pourrait cacher serait de nouveau introuvable. Chaque
ligne y porte :

- le **motif** écrit au moment de la décision — c'est lui qui rend l'exclusion explicable ;
- le **rang arithmétique** que le bâtiment tenait avant d'en sortir, et sa contribution, pour
  mesurer ce qu'on laisse de côté (en « Tous les objectifs » : sur combien d'objectifs il était
  classable) ;
- un formulaire pour **rejuger sur place** — remplacer l'exclusion par un autre ajustement, ou
  **↩︎ Réintégrer**, qui la lève entièrement. Le motif effacé est répété dans le message de
  confirmation, pour qu'un clic malheureux ne l'emporte pas en silence.

Le bâtiment reste par ailleurs visible sur la carte et dans sa fiche, et l'exclusion part dans
l'export des notes, motif compris.

Ces ajustements et les notes s'exportent dans un **même fichier CSV**, qui s'ouvre dans Excel :
on peut le compléter hors de l'outil, l'envoyer à un collègue, récupérer le sien, fusionner les
deux, puis le réimporter. C'est ainsi qu'on partage sans droit d'écriture sur le classeur.

## L'indice développement durable

Il vaut **la somme des pondération × min(1, réalisé ÷ cible)** sur les volets décrits dans la
feuille `Objectifs PTE`. Chaque volet s'y écrit sur deux lignes : le libellé porte la **cible**
en colonne B et la **pondération** en colonne C, la ligne suivante porte le **réalisé**.

| volet | cible 2030 | pondération | réalisé |
|---|---|---|---|
| Végétalisation | 350 000 m² | 60 % | 0 |
| Toitures vivantes | 20 000 m² | 20 % | 250 |
| Déchets et tri | 6 000 points de tri | 20 % | 2 500 |

Ni les volets, ni leurs poids, ni leurs cibles ne se règlent dans l'outil : ce sont des décisions
du programme, elles vivent dans le classeur avec les autres objectifs. Le plafond est **volet par
volet** — un volet dépassé ne rachète pas un volet en retard, faute de quoi la végétalisation,
qui pèse 60 % et dont rien n'est réalisé, se ferait compenser par des points de tri. L'indice
vaut donc **8,6 / 100** aujourd'hui malgré 42 % des points de tri déployés.

À côté du réalisé, chaque volet porte le **projeté** : la somme, bâtiment par bâtiment, de ce que
les projets repérés au plan ajouteraient — colonnes `Surface végétalisée ajoutée (m2)`,
`DD Toiture végétalisée projetée [m2]` et `DD Points de tri projetés [nb]` de `Plan_PTE`. Le
réalisé dit où en est le parc, le projeté ce qu'il atteindrait si tout se faisait : **68,6 / 100**.
L'écart entre les deux est ce qu'il y a à arbitrer.

La **végétalisation n'a plus de tuile propre** : elle est devenue le volet le plus lourd de cet
indice, et le détail de la tuile porte sa courbe d'achat — les projets financés du m² le moins
cher au plus cher, et le rang où la cible est atteinte. Son classement dédié, lui, reste dans
l'onglet Classement.

## Dépendances externes

Les bibliothèques de rendu viennent de deux CDN. Elles portent depuis le 03.09.2026 leur
empreinte **SRI** (`integrity` + `crossorigin`) et une **politique de sécurité de contenu** en
balise `meta` limite ce que la page peut aller chercher. Si un CDN sert un octet différent de
celui attendu, la ressource est refusée et le bandeau d'avertissement existant s'affiche — c'est
le comportement voulu, et il est visible.

Les pièces qui comptent ne dépendent d'aucune bibliothèque : la **trajectoire**, la **jauge**, le
**ruban**, la **courbe d'achat**, le **Top 20**, la **matrice urgence × faisabilité** et la
**répartition par état SIA** sont dessinés en SVG par l'outil lui-même et survivent à un réseau
coupé. Il ne reste que l'histogramme de distribution et le fond de carte à dépendre de l'extérieur.

## Ce qui ne sort pas du navigateur

Le classeur est lu **dans le navigateur**, par un lecteur XLSX intégré : aucune donnée du parc
n'est envoyée nulle part, et aucune n'est embarquée dans le fichier HTML.

Une exception, explicite depuis le 03.09.2026 : les sous-sites dépourvus de coordonnées peuvent
être géolocalisés via **OpenStreetMap**, service tiers. Cet appel ne part **que sur clic** d'un
bouton de l'onglet Carte, qui nomme l'hôte et le nombre d'adresses concernées. Pour l'éviter
entièrement, ajoutez deux colonnes `Latitude` et `Longitude` au classeur.

Ce que l'outil garde dans le navigateur — le fichier importé, les notes, les ajustements et
leurs motifs, les instantanés, le portefeuille validé — reste sur le poste jusqu'à effacement.
Le menu ☰ porte **« Effacer les données de ce navigateur »**, qui purge l'ensemble.

## Le CEE n'est plus un objectif

Vérifié sur le parc réel : le classement CEE portait exactement les **mêmes 97 bâtiments** que le
Thermique, dans **exactement le même ordre**, avec les mêmes coûts unitaires à quatre décimales —
écart de rang maximal **zéro**. C'est mécanique : les deux divisent le même montant par le même
gain en kWh et ne diffèrent que par un paramètre de durée de vie, réglé à 40 ans des deux côtés.
Le CEE n'était que le classement Thermique lu au mètre du CO₂.

Il a donc été retiré des objectifs le 03.09.2026. Le **CHF/kWh reste une mesure** : il note le
critère « coût de l'énergie » du score composite de repli — celui qui range les bâtiments non
mesurables pour un objectif donné — et alimente l'histogramme de distribution de l'onglet
Arbitrage. La durée de vie correspondante reste réglable dans ⚙️, sous le libellé
**Coût du kWh évité**.

## Ce qui compte comme substitution

Une substitution est un **agent**, pas une phrase. La colonne `Chauffage de subsitution prévu` du
classeur porte aussi du texte libre — « ??? », « Décision à prendre par COPIL », « OUI, projet DRT
à clarifier avec X. Chéron ». Ces valeurs passaient autrefois le test « n'est pas fossile » et
produisaient donc un gain renouvelable, l'une pour 643 275 kWh. Une décision qu'on n'a pas prise ne
se compte pas comme un gain : depuis le 03.09.2026, seul ce qui **commence par un agent connu**
(Bois, PAC, CAD, El. SIG, Solaire, Gaz, Mazout…) ouvre droit à une contribution renouvelable. Le
reste remonte dans l'onglet Données comme saisie à compléter.

**CADIOM est renouvelable.** Il figurait parmi les agents fossiles du moteur des objectifs alors
que le filtre « Fossiles » de l'onglet Classement l'excluait déjà : le même bâtiment était fossile
ici et non fossile là. Conséquence assumée de la mise en cohérence : sortir d'un CADIOM n'est plus
une substitution.

## Réglages

Menu **☰ → Paramètres de calcul**, en trois sections repliables : durée de vie, cibles
d'intensité thermique, productible photovoltaïque. Rien n'est figé dans le code ; les valeurs
actives sont rappelées dans l'onglet Méthode et mémorisées dans le navigateur. Les pondérations
du développement durable, elles, ne s'y règlent pas — elles viennent du classeur.

Les **cibles d'intensité thermique** s'expriment en kWh/m²·an — l'unité des audits — et il y en
a deux : **97 kWh/m²·an pour 2030** (350 MJ) et **63 kWh/m²·an pour 2050** (227 MJ). Le classement
Thermique affiche les deux colonnes « % cible comblé » et met en évidence les deux rangs de
franchissement : vert pour 2030, bleu pour 2050. La note du classement dit laquelle des deux
cibles est la plus exigeante — sur le parc actuel, c'est celle de 2030, la baisse de −60 % depuis
2005 descendant plus bas que l'intensité visée pour 2050.

La durée de vie se règle aussi **objectif par objectif** — une isolation d'enveloppe, une pompe à
chaleur et une robinetterie ne s'amortissent pas sur la même durée, et imposer 40 ans partout
avantage mécaniquement les objectifs dont les mesures durent le plus longtemps. Une case laissée
vide reprend la valeur générale, et la durée réellement appliquée est écrite en tête de colonne de
chaque classement.

## Filtrer le périmètre

Le filtre **Portefeuille** de la ligne de contexte accepte un **choix multiple** : cocher trois
ou quatre responsables sans les autres, pour préparer une séance commune. Aucune case cochée =
tout le parc. Le filtre restreint l'affichage de tout l'outil — classement, arbitrage, carte,
indicateurs — mais **jamais les rangs**, calculés sur l'ensemble du parc : on voit la place de
ses bâtiments dans le tout, pas un classement interne. Dans l'onglet Données, le bouton
« Filtrer » de chaque portefeuille bascule dessus ; **Maj+clic** l'ajoute à la sélection en cours.

## « Hors chiffrage » : voir où est la matière

Le classement par coût unitaire a un effet secondaire lourd — **un bâtiment sans montant saisi
n'est pas classable du tout**. Sur le CO₂, 43 bâtiments sur 582 franchissent ce filtre : l'ordre
obtenu ne dit rien des 539 autres, dont plusieurs pèsent lourd.

Le menu **Montants** porte donc un quatrième choix qui n'est pas un référentiel : **Hors
chiffrage** déclare le **coût unitaire identique pour tous les bâtiments**, sans lire aucune
colonne du classeur. Le coût cesse alors de départager quoi que ce soit, et le seul critère qui
subsiste est la **contribution** : le classement va du plus gros contributeur au plus petit, et
le rang de franchissement y devient le **nombre minimal de bâtiments** qui comblent l'écart. Les
colonnes Montant et CHF/unité n'ont plus de contenu (« — » et « = »). La végétalisation n'est pas
concernée, son coût du m² venant de sa propre colonne.

Sur le CO₂ la population classable passe de 43 à 65 bâtiments, sur le thermique de 97 à 151, sur
le renouvelable de 101 à 158.

C'est la lecture « **où est la matière** », à mettre à côté de « où est le meilleur franc », pas à
la place. L'onglet Arbitrage est inopérant tant que le mode est actif — sans montants, il n'y a
pas de budget à répartir — et l'outil le signale par un bandeau dans le Classement comme dans
l'Arbitrage, plus une pastille orange dans la ligne de contexte.

**Ce que ce mode ne débloque pas.** Il lève le verrou du **coût**, pas celui de l'**audit**. Un
bâtiment sans CECB+ n'a pas d'IDC projeté, donc aucune contribution calculable, donc aucun rang —
dans ce mode comme dans les autres. C'est pourquoi on passe à 65 bâtiments et non à 582 ; le
bandeau du classement dit à chaque fois combien manquent et pourquoi.

Menu **☰ → Affichage** : mode nuit, mode présentation (chiffres agrandis pour la projection).
Les deux modes respectent le niveau **WCAG 2.1 AA** — 4,5:1 pour le texte courant, 3:1 pour le
grand texte et les éléments d'interface, vérifié automatiquement sur les six onglets.

## Source des données

Classeur `Plan_PTE_optimise.xlsx` (ou `Plan_PTE.xlsx`), cinq onglets :

| Onglet | Ce qu'il apporte |
|---|---|
| `Plan_PTE` | une ligne par sous-site : SRE, IDC actuel et projeté, variante CECB+, agent de chauffage actuel et prévu, montants, patrimoine, portefeuille, surface végétalisée à créer et son coût TTC |
| `Objectifs PTE` | références 2005 et pourcentages de réduction, les volets de l'indice développement durable (cible, pondération, réalisé), puis la série annuelle du suivi officiel |
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
  La colonne « DG (25 %) » a été retirée du menu : ce n'était pas un référentiel saisi mais 25 %
  du montant ImmOBA calculé à la volée, et la proposer à côté de trois colonnes réellement
  renseignées laissait croire à une quatrième source. Le quatrième choix du menu, « Hors
  chiffrage », n'est pas non plus un référentiel : il neutralise le coût au lieu d'en fournir un,
  et ne sert qu'à classer, jamais à budgéter.
- **Un bâtiment sans coût n'est pas classable.** Ce n'est pas l'argent qui limite le résultat
  2030 mais la donnée : l'onglet Données indique quelles saisies débloqueraient le plus de
  bâtiments.
- **Les surfaces végétalisées sont à créer, pas créées.** La colonne du classeur porte ce que
  les projets ajouteraient ; rien n'y est compté comme réalisé. L'écart à combler est donc
  l'objectif entier, et le pourcentage affiché sur la tuile dit seulement quelle part de la
  cible les projets déjà repérés couvriraient s'ils étaient tous financés.
- L'indice **développement durable** ne connaît le **projeté** que pour la végétalisation : les
  colonnes `DD Toiture végétalisée projetée [m2]` et `DD Points de tri projetés [nb]` viennent
  d'être créées dans `Plan_PTE` et sont encore vides. Tant qu'elles le restent, ces deux volets
  n'affichent que leur réalisé.
