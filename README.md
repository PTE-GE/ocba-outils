# ocba-outils

Outils de l'OCBA (État de Genève) en accès libre. Aucune donnée réelle n'est embarquée : chaque outil lit, dans le navigateur, le fichier que l'utilisateur y dépose. Rien n'est chargé depuis un autre site.

| Adresse | Outil |
|---|---|
| [`index.html`](index.html) | **Pilotage PTE** : tableau de bord, priorisation, suivi des projets et simulation des gains, en une page |
| [`Trombinoscope/`](Trombinoscope/) | Trombinoscope et organigramme (copie vierge) |

Les anciennes adresses `priorisation/`, `revue-projets/` et `simulation-gains/` renvoient vers la page unique.

Chaque page porte sa politique de sécurité (CSP à empreintes) : un script modifié sans que son empreinte soit recalculée ne s'exécute plus. Le tableau de bord KPI CECB+ (`kpi/`) a été retiré le 14.11.2026.
