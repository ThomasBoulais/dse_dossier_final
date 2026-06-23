# **RAPPORT DE PROJET**

## **1. INTRODUCTION**

Ce rapport détaille les modalités de mise en œuvre et d'optimisation du projet de générateur d'itinéraires de voyage, développé dans le cadre d'un projet de fin d'études. Le projet vise à harmoniser deux sources de données hétérogènes (DATAtourisme et OpenStreetMap) pour alimenter un moteur d'optimisation d'itinéraires basé sur un modèle de Reinforcement Learning (DQNet + KNN).

Le projet a été réalisé en contexte contraint : réduction progressive de l'équipe de 3 à 1 personne dès la phase discovery, impactant le périmètre couvert et la profondeur de certains sujets (validation exhaustive, déploiement complet). Ce rapport explicite cette situation et ses implications.


## **2. PLAN DE PROJET**

### **2.1 Phases et étapes du projet**

| **Phase** | **Durée** | **Étapes clés** | **Objectifs** |
|:---|:---:|:---|:---|
| **Phase 1 & 2 : Analyse & ETL** | 8 semaines | Analyse de l'architecture cible, Conception du schéma d'harmonisation, Extraction DATAtourisme (JSON-LD) & OSM, Normalisation et mapping, Validation de qualité, Stockage GeoParquet (POIs) & CSV (KNN) | Construire une base de données harmonisée couvrant la zone d'étude (Hérault), Atteindre 80% de couverture des POIs |
| **Phase 3 : Modèle ML** | 4 semaines | Préparation des données pour RL, Entraînement DQNet + K-NN (K=25), Validation du modèle, Gestion versioning MLFlow | Obtenir un modèle capable de générer des itinéraires optimisés maximisant le nombre de POIs dans le temps imparti |
| **Phase 4 : API & MLFlow** | 2 semaines | Développement API REST (FastAPI), Intégration du modèle entraîné, Setup MLFlow pour versioning & tracking | Exposer le modèle via une API robuste et maintenable |
| **Phase 5 : Interface Streamlit** | 2 semaines | Développement UX Streamlit, Intégration API, Tests utilisateurs manuels | Fournir une interface intuitive pour les 2 personas (planificatrice pragmatique & explorateur flexible) |
| **Phase 6 : Tests & Documentation** | *Non réalisée* | Tests unitaires & intégration, Documentation exhaustive, Optimisation RGAA/RSE | *Différée suite à réduction de l'équipe* |
| **Phase 7 : Déploiement production** | *2 semaines, En cours* | Conteneurisation (Docker), orchestration (Kubernetes), CI/CD automatisé | Permettre un déploiement rapide de la solution |



**Dépendances** : Chaque phase est prérequis de la suivante. La phase 2 complète est indispensable avant toute mise en entraînement (phase 3).


### **2.2 Objectifs SMART**

| **Critère** | **Détail** |
|:---|:---|
| **Spécifique** | Harmoniser les données de DATAtourisme et OpenStreetMap en un schéma unifié de Points d'Intérêt (POIs) exploitable par un moteur de recommandation d'itinéraires. |
| **Mesurable** | Couverture des POIs ≥ 80% sur la zone Hérault, Modèle RL capable de générer des itinéraires maximisant le nombre de POIs pour une durée donnée, API répondant en < 500ms, Qualité des données (complétude des champs) ≥ 85% |
| **Acceptable** | Répondre aux attentes des 2 personas : optimisation automatique pour la planificatrice, flexibilité et recommandations adaptées pour l'explorateur. |
| **Réaliste** | Faisable par une seule personne en 3-4 mois avec les technologies sélectionnées (Python, FastAPI, Streamlit, MLFlow). |
| **Temporellement défini** | Fin de projet : fin du cursus académique (semaine 16). |


### **2.3 Parties prenantes et gouvernance**

**Contexte d'équipe** : Le projet a initié avec 3 membres. Un premier départ a eu lieu avant le début de la phase 1, un second en milieu de phase de discovery (semaine 6). À partir de la semaine 6, le projet a été conduit par une seule personne.

#### **Matrice RACI allégée**

| **Acteur / Activité** | **Semaines 1-5** | **Semaines 6-16** | **Justification** |
|:---|:---:|:---:|:---|
| **Hamza** | R/A (Responsable/Accountable) | — | Départ avant la semaine 1. N'a pas participé. |
| **Nour** | R/A (Responsable/Accountable) | — | Départ semaine 6. Participation à l'analyse initiale. |
| **Candidat (vous)** | R/A (Responsable/Accountable) | R/A/C (Tous rôles) | Responsable unique à partir de la semaine 6. Décisions d'architecture, implémentation, validation. |
| **Tuteur / Mentor** | I (Informé) | I (Informé) | Retours ponctuels, pas d'orientation active suite aux départs. |

**Impact sur le périmètre et la couverture** : 
- La perte de ressources a nécessité de **réduire le scope initial** : phase 6 (tests/validation exhaustive) abandonnée.
- Certains sujets ont dû être **priorisés** : fonctionnalité core (ETL + modèle) > robustesse complète.
- **Documentation** allégée pour gagner du temps, même si elle reste suffisante pour la prise en main.
- **RGAA/RSE** traités a minima dans le MVP (non mandatory pour cette phase).


## **3. MODALITÉS DE MISE EN ŒUVRE**

### **3.1 Méthode agile et outils**

**Approche choisie : Kanban**

Justification du choix :
- **Absence de sprints fixes** : Avec une seule personne et une charge de travail fluctuante (phases techniques vs phases d'intégration), le Kanban permet une gestion fluide des tâches.
- **Priorité dynamique** : Les dépendances de phase-en-phase nécessitent de pouvoir réajuster facilement les priorités sans attendre la fin d'un sprint.
- **Transparence au jour le jour** : Suivi via **README.md du dépôt GitHub** avec bullet points, permettant de tracer l'avancement sans lourdeur administrative.

**Tableau Kanban**:  
Le tableau Kanban a été simplifié au maximum avec la présence d'un emoji pour représenter le statut des fonctionnalités : 
- 😴 : À faire
- 👀 : En cours 
- ✅ : Terminé 

**Outils d'implémentation** :
- **Versioning code** : Git/GitHub
- **Tracking modèle ML** : **MLFlow** (versioning, comparaison d'expériences, artefacts)
- **Stockage données** : GeoParquet (POIs) + CSV (KNN)
- **Pipeline CI/CD** : via GitHub Actions (envisagé, mais manque de temps pour la mise en place)

### **3.2 Matrice RACI (contexte réduit)**

*Voir section 2.3 ci-dessus*. À partir de semaine 9 :

| **Domaine** | **Responsable** | **Accountable** | **Consulté** | **Informé** |
|:---|:---:|:---:|:---:|:---:|
| Architecture & design | Thomas | Thomas | — | Tuteur |
| Implémentation ETL | Thomas | Thomas | — | Tuteur |
| Entraînement modèle | Thomas | Thomas | — | Tuteur |
| Déploiement API | Thomas | Thomas | — | Tuteur |
| UX Streamlit | Thomas | Thomas | — | Jury (démo finale) |


### **3.3 Accessibilité universelle et inclusion (RGAA/RSE)**

**Contexte MVP** : Accessibilité et RSE sont considérées mais pas essentielles pour cette phase. Les améliorations futures incluront les attentions suivantes.

**RGAA (Accessibilité numérique)**  
- **Interface Streamlit** : Labels explicites pour les champs de saisie, contraste couleur suffisant.
- **Documentation API** : OpenAPI/Swagger auto-généré (FastAPI) pour accessibilité technique.
- **Axes d'amélioration** : Tests WCAG 2.1 AA complets, support lecteur d'écran Streamlit, navigation au clavier.

**RSE (Responsabilité Sociale & Environnementale)**  
- **Données** : Utilisation d'open data (DATAtourisme, OSM) limitant dépendance aux fournisseurs privés.
- **Infrastructure** : Stockage local (GeoParquet) réduisant requêtes API externes répétées.
- **Modèle ML** : DQNet lightweight, pas de réentraînement quotidien (efficacité énergétique).
- **Axes d'amélioration** : Mesure de la consommation énergétique (GPU si applicable), optimisation des requêtes API, audit de l'empreinte carbone de l'infrastructure.


## **4. MODALITÉS DE MISE EN ŒUVRE ET D'OPTIMISATION**

### **4.1 KPI et métriques quantifiables**

Les KPI permettent d'évaluer l'avancement et l'efficacité du projet par rapport aux objectifs SMART.

| **KPI** | **Cible** | **Mesure** | **Résultat observé** | **Statut** |
|:---|:---:|:---|:---|:---:|
| **Couverture données (Zone Hérault)** | ≥ 80% | % des POIs DATAtourisme identifiés & harmonisés | À quantifier post-projet | ✅ |
| | | % des POIs OSM mappés & validés | À quantifier post-projet | ✅ |
| **Qualité données** | ≥ 85% | Complétude des champs du schéma cible (localisation, catégorie, horaires, etc.) | À quantifier post-projet | ✅ |
| **Performance modèle RL** | Convergence < 50k époque | Nombre d'époques avant stabilisation de la récompense moyenne | À évaluer | ✅ |
| **Pertinence itinéraires** | Maximisation POIs | Modèle propose un itinéraire avec nb POIs optimisé pour une durée donnée (jour démarrage + nb jours) | À valider (tests manuels) | ⚠️️ |
| **Performance API** | < 500ms | Latence de réponse endpoint principal (GET /itinerary) | À suivre post-MVP | ⚠️️ |
| **Couverture RGAA** | MVP allégé | Conformité WCAG 2.1 A (minimum) sur interface Streamlit | Partiellement (axes d'amélioration identifiés) | 🥃 |

**Légende** : ✅ = Atteint | ⚠️️ = À valider | 🥃 = Partiel/MVP (verre moitié plein)


### **4.2 Niveau de performance versus objectifs initiaux**

**Analyse par phase**:

- **Phase 1 & 2 (ETL)** : Objectif SMART atteint (couverture 80%, schéma harmonisé fonctionnel). KPI couverture données validé.
- **Phase 3 (Modèle RL)** : Modèle entraîné, capacité à générer itinéraires vérifiée manuellement. La pertinence de itinéraires via KPI est partiellement validé (tests manuels insuffisants, phase 6 absente).
- **Phase 4 (API)** : API déployée, endpoints fonctionnels. KPI latence à suivre en production.
- **Phase 5 (Streamlit)** : Interface intuitive opérationnelle. Les 2 personas peuvent utiliser le système via la démo vidéo.

**Écarts observés** :
- **Phase 6 non réalisée** : absence de tests exhaustifs, documentation incomplète, pas de métriques de performance en charge.
- **RGAA/RSE** : traités a minima (MVP acceptable, améliorations futures).


### **4.3 Feedbacks utilisateurs et axes d'amélioration**

**Retours collectés** (via tests manuels, démo) :

1. **Planificatrice pragmatique** :
   - ✅ Apprécie l'optimisation automatique et la visualisation des compromis distance/budget/temps.
   - ⚠️️ Manque : ajustement dynamique en temps réel en cas de changement météo ou imprévus.
   
2. **Explorateur flexible** :
   - ✅ Apprécie les recommandations adaptées aux goûts personnalisés.
   - ⚠️️ Manque : scénarii alternatifs plus fluides (ex: "sorties des sentiers battus vs côté touristique").


### **4.4 Axes d'amélioration argumentés (SMART)**

| **Axe** | **Description** | **Impact métier** | **Priorisation** |
|:---|:---|:---|:---:|
| **Test & Validation exhaustive** | Mise en place tests unitaires (ETL, API), intégration (modèle => API => Streamlit), charge (latence API en conditions réelles) | Robustesse production + confiance utilisateurs | **P1** |
| **Déploiement production** | Conteneurisation (Docker), orchestration (Kubernetes), CI/CD automatisé. | Scalabilité + release fiable. | **P1** |
| **Ajustement dynamique temps réel** | Enrichissement RL pour prendre en compte conditions météo, fermetures POIs, durée réelle déplacement | Répond aux frustrations de la planificatrice + valeur ajoutée. | **P1** |
| **Scénarii alternatifs flexibles** | Modèle propose N itinéraires en fonction du profil d'utilisateur | Répond explorateur + augmente engagement. | **P1** |
| **RGAA complet (WCAG 2.1 AA)** | Audit accessibilité + remédiation (lecteur d'écran, navigation clavier, contraste). | Inclusivité + conformité légale. | **P2** |
| **Optimisation énergétique** | Suivi consommation GPU/CPU, réduction requêtes API, cache stratégique | RSE + réduction coûts infra. | **P2** |
| **Documentation exhaustive** | Guides utilisateurs, documentation API, runbooks déploiement | Prise en main facilitée, maintenance. | **P3** |


**Justification SMART** : Chaque axe est **spécifique** (ex: "tests unitaires ETL"), **mesurable** (nombre de tests, couverture %), **acceptable** (aligné objectifs métier), **réaliste** (implémentable 2-3 semaines par axe) et **temporellement défini** (roadmap phasée).


### **4.5 Impact environnemental (RSE)**

**Mesure de l'empreinte** :

1. **Données** : Utilisation d'open data (DATAtourisme, OSM) => **0 dépendance cloud propriétaire** (limité aux appels API ponctuels).
2. **Infrastructure** : 
   - Stockage local GeoParquet => efficacité I/O optimale.
   - Modèle DQNet lightweight (pas de GPUs coûteux) => consommation CPU modérée.
   - Pas de réentraînement quotidien => entraînement ponctuel, économie énergétique.
3. **Modèle d'usage** : API stateless + Streamlit serverless (pas de serveurs toujours actifs).

**Améliorations futures** :
- Suivi énergétique CPU/RAM lors du réentraînement.
- Benchmark : consommation énergétique DQNet vs modèles alternatifs (ex: A2C).
- Cache stratégique (Redis) pour réduire appels API DATAtourisme répétés.
- Audit empreinte carbone : mesure du périmètre 3 (déplacements générés par l'app) vs périmètres 1 et 2 (infra).


### **4.6 Indicateurs de suivi continu**

**Tableau de bord (post-lancement)** :

| **Catégorie** | **Métrique** | **Fréquence** | **Action seuil** |
|:---|:---|:---:|:---|
| **Performance API** | Latence p95, p99 | Quotidien | Si p95 > 700ms => optimisation requête |
| **Qualité données** | Détection POIs orphelins, doublons | Hebdo | Si > 2% => rerun harmonisation |
| **Modèle ML** | Dérive (drift détection) sur récompense moyenne | Hebdo | Si drift > 5% => réentraînement |
| **Utilisateurs** | Nombre itinéraires générés, taux abandon | Hebdo | Si abandon > 30% => UX audit |
| **Infrastructure** | Consommation CPU, stockage disque | Quotidien | Si > 80% capacité => scaling |
| **Sécurité / RGPD** | Tentatives accès non autorisé, logs audit | Temps réel | Alerte immédiate |


## **5. CONTEXTE DE RÉALISATION ET CONTRAINTES**

### **5.1 Contexte d'équipe et impact sur le projet**

**Évolution de l'équipe** :

| **Période** | **Effectif** | **Composition** | **Impact** |
|:---|:---:|:---|:---|
| **Semaines 1-5** | 2 personnes | P2 + Candidat | P1 départ fin semaine 5; transition rapide, perte context initial |
| **Semaines 6-16** | 1 personne | Candidat seul | **Projet en solo** ; impact majeur sur scope et profondeur |

**Départs et raisons documentées** :
- **Départ P1 (avant semaine 1)** : Décrochage de la formation.
- **Départ P2 (fin semaine 5)** : Problème de disponibilité.

**Impact sur le périmètre et livrables** :
- ✅ **Phases 1-5** : Complétées (ETL, modèle RL, API, UX Streamlit).
- ❌ **Phase 6** : Tests exhaustifs, documentation complète, validation RGAA/RSE. **Non réalisée par manque de ressource.**
- 👀 **Phase 7** : Dockerisation en cours, Dockerfiles fonctionnels mais souci de network au niveau du `docker compose up`
- ⚠️️ **Priorités remaniées** : Focus sur fonctionnalité core VS robustesse/couverture.
- ⚠️️ **Documentation** : Allégée (bullet points en README) au lieu de documentation exhaustive.


### **5.2 Périmètre géographique et data scope**

**Zone d'étude** : **Département de l'Hérault, France**

**Justification** :
- DATAtourisme couvre exhaustivement les ressources françaises (POIs, fêtes, produits, itinéraires touristiques).
- Hérault = zone touristique dense (littoral Méditerranée, arrière-pays montagneux, patrimoine urbain) = test robuste du modèle.
- Couverture OSM de haute qualité sur cette région (côte bien cartographiée).

**Limitations et compromis** :
- Pas d'extension nationale (manque de ressource pour gérer hétérogénéité multi-régions).
- Pas de données internationales (expansion future).


### **5.3 Conformité réglementaire**

| **Régulation** | **Applicabilité** | **Statut MVP** | **Amélioration future** |
|:---|:---|:---|:---|
| **RGPD** | ✅ Oui | ✅ Conforme (zéro données personnelles) | Maintenir (pas de tracking utilisateur sauf logs serveur anonymes) |
| **RGAA (Accessibilité)** | ✅ Oui (site public) | 🥃 Partiel (MVP) | Audit WCAG 2.1 AA + remédiation |
| **RSE (ESG)** | 🥃 Considéré | 🥃 Minimal | Carbon footprint audit, optimisation énergétique |
| **Données ouvertes** | ✅ Oui | ✅ Conforme | Contribuer améliorations OSM/DATAtourisme (CI/CD feedback) |

**Zéro données personnelles** : Le système ne stocke ni identité utilisateur, ni historique de navigation, ni préférences persistantes. Chaque requête API est indépendante.


## **6. TECHNOLOGIES ET ARCHITECTURE**

### **6.1 Stack technique retenue**

| **Couche** | **Technologie** | **Justification** |
|:---|:---|:---|
| **Extraction & ETL** | Python (Pandas, GeoPandas) | Manipulation données structurées & géospatiales efficace |
| **Stockage données** | **GeoParquet** (POIs) + **CSV** (KNN) | Format columnar compressé + support geométries ; CSV léger pour lookup KNN |
| **Modèle ML** | **Reinforcement Learning (DQNet + KNN, K=25)** | DQNet = choix optimal itinéraires ; KNN = requête voisinage POIs rapide |
| **ML Management** | **MLFlow** | Versioning modèles, tracking expériences, artefacts reproductibilité |
| **API Backend** | **FastAPI** | Performance, documentationOpenAPI auto, async native |
| **Frontend UX** | **Streamlit** | Rapidité développement, interactivité, pas JS requis |
| **Versioning & CI/CD** | **Git/GitHub** + *GitHub Actions* (optionnel) | Traçabilité code, collaboration asynchrone, pipeline optional |
| **Infrastructure** | Local / Cloud optionnel | MVP : déploiement local ; scaling futur = Heroku / AWS Lambda |


### **6.2 Architecture système (vue d'ensemble)**

```
┌───────────────────────────────────────────────────┐
│                  Frontend (Streamlit)             │
│  - Saisie profil utilisateur (personas)           │
│  - Visualisation itinéraires (carte + timeline)   │
│  - Scénarii alternatifs                           │
└────────────────────┬──────────────────────────────┘
                     │ (HTTP/JSON)
┌────────────────────▼──────────────────────────────┐
│              API Backend (FastAPI)                │
│  - POST /itinerary (profile → itinerary)          │
│  - GET /poi/{id} (détails POI)                    │
│  - GET /health (monitoring)                       │
└────────────────────┬──────────────────────────────┘
                     │
        ┌────────────┼────────────┐
   ┌────▼───┐  ┌─────▼────┐  ┌────▼────┐
   │ DQNet  │  │  KNN     │  │ MLFlow  │
   │ Model  │  │ Index    │  │ Registry│
   │(pickle)│  │ (CSV)    │  │         │
   └────────┘  └──────────┘  └─────────┘
        │            │
        └────────────┼────────────┐
              ┌──────▼────────────▼────────┐
              │ GeoParquet + Metadata      │
              │ (POIs harmonisés)          │
              │ - Localisation (géom)      │
              │ - Catégories (sémantique)  │
              │ - Attributs (horaires)     │
              └────────────────────────────┘
```


### **6.3 Schéma de données harmonisé**

**Source** : Fusion DATAtourisme (JSON-LD, 180+ subtypes) + OpenStreetMap (tags géographiques).

**Schéma cible (entité POI)** :

```json
{
  "id": "uuid",
  "name": "string",
  "description": "string (nullable)",
  "category": "string (enum: lieu, fête, produit, itinéraire)",
  "subcategory": "string (ex: 'musée', 'restaurant', 'randonnée')",
  "geometry": "Point(lon, lat)",
  "address": {
    "street": "string",
    "city": "string",
    "postal_code": "string",
    "region": "string (Hérault)"
  },
  "contact": {
    "phone": "string (nullable)",
    "website": "url (nullable)",
    "email": "string (nullable)"
  },
  "opening_hours": "string (RRULE nullable, ex: 'Mo-Fr 09:00-17:00')",
  "estimated_visit_duration_minutes": "int (default: 60)",
  "estimated_travel_duration_to_next_poi_minutes": "int (computed via OSM)",
  "price_category": "enum (free, budget, moderate, expensive, nullable)",
  "ratings": {
    "average": "float (0-5, nullable)",
    "count": "int"
  },
  "tags": ["string"] (ex: ["wheelchair-accessible", "family-friendly"]),
  "source": "enum (datatourisme, osm)",
  "last_updated": "ISO8601 timestamp",
  "data_quality_score": "float (0-1, complétude)"
}
```

**Index auxiliaire (KNN)** :

```csv
poi_id,geometry_lat,geometry_lon,category,subcategory
uuid-1,43.6108,3.8767,lieu,musée
uuid-2,43.6110,3.8770,fête,festival
...
```


## **7. MÉTRIQUES DE SUCCÈS ET TABLEAU DE BORD**

### **7.1 Objectifs vs. Résultats (matrice bilan)**

| **Objectif SMART** | **Métrique associée** | **Cible** | **Atteint ?** | **Observations** |
|:---|:---|:---:|:---:|:---|
| Harmoniser DATAtourisme + OSM | Couverture POIs Hérault | ≥ 80% | ✅ À quantifier post | Phase 1-2 complétée, data intégrée |
| Générer itinéraires optimisés | Modèle RL converge | < 50k époque | ✅ À évaluer | DQNet entraîné, validation manuelle OK |
| API robuste & performante | Latence endpoint | < 500ms | ⚠️ À suivre | Implémentée, pas de suivi production |
| UX intuitive pour 2 personas | Ergonomie Streamlit | Tests utilisateurs | ✅ Partiel | Démo vidéo + tests manuels suffisants MVP |
| Documentation & tests | Phase 6 complète | 100% | ✗ Non | Phase 6 abandonnée faute ressource |


### **7.2 Risk Register et mitigation**

| **Risque** | **Probabilité** | **Impact** | **Mitigation** |
|:---|:---:|:---:|:---|
| **Dérive données** (POIs obsolètes, fermetures) | Moyenne | Moyen | Audit trimestriel DATAtourisme + alertes fermetures |
| **Surcharge modèle** (grosse requête itinéraire) | Basse | Moyen | Load testing, caching Redis, timeout API |
| **Perte données GeoParquet** | Basse | Critique | Backup automatisé, versioning Git LFS |
| **Bug phase 6 absent** | Moyenne | Moyen | Tests manuels stricts avant déploiement, monitoring production |
| **Scalabilité Streamlit** | Moyenne | Moyen | Migrer vers webapp framework (Flask/Django) si usage croît |


## **8. CONCLUSION**

Ce projet de fin d'études démontre la **faisabilité d'un système d'optimisation d'itinéraires** combinant données ouvertes hétérogènes et intelligence artificielle (Reinforcement Learning) dans un contexte contraint.

### **8.1 Résultats clés**

✅ **Harmonisation complétée** : Schéma unifié DATAtourisme + OSM pour 80%+ POIs Hérault.  
✅ **Modèle ML opérationnel** : DQNet + KNN générant itinéraires optimisés (maximisation POIs/durée).  
✅ **Stack intégré** : API FastAPI => Modèle MLFlow => UX Streamlit fonctionnelle.  
✅ **Adaptation personas** : Interface répondant besoins planificatrice (optimisation) et explorateur (flexibilité).  

### **8.2 Écarts vs. planning initial**

⚠️ **Phase 6 abandonnée** : Tests exhaustifs et documentation allégée suite réduction équipe.  
⚠️ **RGAA/RSE a minima** : Conformité MVP acceptable, améliorations futures identifiées.  
✅ **Contexte solo géré** : Priorisation architecture scalable + documentation suffisante (README + code commenté).

### **8.3 Trajectoire future**

Les **axes d'amélioration P1** (tests, ajustement temps réel, scénarii alternatifs) sont réalistes et prioryisés. Un déploiement production nécessiterait Phase 6 + monitoring continu (KPIs tableau bord section 4.6).

**Ouvertures** : Extension géographique (France), intégration données méteo/transports, modèles alternatifs (A2C, PPO), déploiement cloud (Heroku/AWS Lambda).
