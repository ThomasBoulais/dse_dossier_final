# Cahier des Charges - Itinéraire de voyage

*Rédaction : Thomas BOULAIS*

## Plan du cahier des charges

1. **Phase Discovery**  
*phase de recherche et découverte des besoins à partir de framework de réflexions*  

    1. **Récolte du besoin**  
    *questionnaire auprès de futurs potentiels usagers*  

    2. **Création des Personas**  
    *à partir des résultats du questionnaire*  

    3. **Synthèse Discovery**  
    *idéation autour des problématiques*  

    4. **Experience Map**  
    *idéation du parcours utilisateur à partir des personas*

2. **Périmètre du projet**  
*à partir de l'ensemble des opportunités produit réfléchies plus tôt, on va sélectionner de quoi constituer le MVP pour la V1*  

    1. **Liste de toutes les fonctionalités**  
    *rappel des opportunités & solutions des synthèse Discovery & Experience Map*  

    2. **Tri des priorités**  
    *Méthode MoSCoW must-have / should-have / could-have / won't-have*  


    3. **Définition du MVP**  
    *prise de décision sur le périmètre du MVP*  


---
---

# 1. Phase Discovery

L'objectif de la partie Discovery est de poser les problèmes auxquels on souahite répondre et de le confronter à la réalité via **enquête**, puis de reformuler les problèmes sur lesquels on souhaite agir en définissant des **personas**.  

A ces fins, des documents de cadrages tels que la **Synthèse Discovery** ou l'**Experience Map** sont très utiles en se plaçant dans différentes approches autour du sujet, respectivement la **résolution de problèmes** (le pragmatisme) et **le parcours utilisateur** (l'empathie).

## 1.1 Récolte du besoin

Afin d'avoir une idée générale du public susceptible d'être intéressé par une application de génération d'itinéraire optimisé de voyage, un **questionnaire d'enquête** a été créé et diffusé autour de nous : https://forms.gle/LLqZ1e3ZRSYHQNLJA  

Les 34 réponses ont permis de mettre en évidence les informations suivantes : 
- Les **¾** ont **entre 25 et 34 ans**, et plus d’**⅕** à **plus de 35 ans** pour des **voyages en groupe** (au moins 2)
- Plus des **¾** planifient **à plusieurs**
- Plus des **¾** utilisent soit des **app** soit des **tableurs**, et **15%** en **papier avec des guides touristiques**
- Les principales difficultés rencontrées sont l'**optimisation de l’itinéraire (62%)**, les **activités adaptés (47%)**, la **gestion des imprévus (30%)** et enfin le **manque d’info fiables (24%)**
- **60%** ont le **sentiment d’avoir déjà perdu du temps** pendant un voyage, à cause notamment d’une **mauvaise organisation (48%)**, de **temps de transport trop longs (19%)** ou d’un **temps d’attente entre les activités trop longues (14%)**
- Concernant le temps d’organisation, **60%** des sondés passent **plus de 6h avant de partir**, **21%** entre **4 et 6h** et moins pour le reste 
- Les critères les plus importants pour la planification sont le **budget (71%)**, la **distance entre les lieux (68%)**, le **temps de transport (65%)** et le **nombre de lieux à visiter (59%)**
- Parmi ceux qui utilisent une **app pour organiser leur voyage (68%)**, la vaste majorité utilise *Google Maps*, les autres utilisent *TripIt*, *My Maps*, *Stippl*, *Komoot*, *France Vélo Tourisme*, *Excel*, *Trip Advisor*.  
    - Ils indiquent manquer d'info dans ces app : transports publics disponibles, durée moyenne des activités et des transports, 
    - Ils indiquent aussi d'autres envies : mutualisation des app (activités, lieux, agendas, app trop spécialisée), avoir une option B, sortir des sentiers battus, avoir une garantie de la fiabilité des info
- **53%** des sondés considèrent qu’**un voyage est réussi si l’itinéraire est bien optimisé**, contre **32%** pour un **itinéraire flexible** 
- **91%** seraient **prêts à utiliser** une app d’optimisation d’itinéraire
- Les facteurs de confiance envers l’application sont la **fiabilité des recommandations (59%)**, la **personnalisation (24%)** et la **facilité d’utilisation (15%)**
- Les facteurs de doute sont les **erreurs dans les suggestions (61%)**, la **confusion dans les options proposées (21%)** et le **manque de flexibilité (15%)**

## 1.2. Création des Personas

Un **persona**, ou **archétype d'utilisateurs**, est un profil générique représentant la généralisation d'une partie de la population parmi ceux attendus comme utilisateurs finaux. Leurs *comportements*, *attentes*, *envies*, *besoins* et *contraintes* sont d'autant de **paramètres** qui sont **à considérer dans l'élaboration de la solution**.

A partir des réponses du questionnaire, les 2 personas suivants ont été défini : celui de la **Planificatrice pragmatique** et celui de l'**Explorateur flexible**.

 | Persona | Planificatrice pragmatique | Explorateur flexible
 | :-: | :-- | :--
 | **Profil** |  - 25-34 ans<br>- duo ou petit groupe<br>- à l’aise avec la tech<br>- utilise Excel + Maps |  - 25-45 ans<br>- solo ou duo<br>- cherche des expériences authentiques<br>- sensible aux opportunités, météo, fatigue
 | **Objectifs** |  - veut voir un max sans se fatiguer<br>- veut respecter budget et horaires<br>- veut des trajets optimisés | - veut sortir des sentiers battus<br> - veut garder de la liberté une fois sur place<br> - ne veut pas subir l’itinéraire
 | **Frustrations** |  - faire face aux imprévus<br> - manque d’info /info incomplètes<br> - outils manuels non connectés |  - itinéraire rigide<br> - lieux trop touristiques<br> - pas d’alternatives
 | **Attentes fonctionnelles** |  - optimisation auto de l’itinéraire<br> - ajustement dynamique en temps réel<br> - visualisation claire des compromis (distance vs budget vs temps) |  - recommandations s’adaptant à leurs goûts <br> - proposition d’itinéraire plus “beaux” ou “intéressants”<br> - scénarii alternatifs
 

## 1.3 Synthèse Discovery

Ce document de cadrage, proposé comme template par l'organisme de formation **DATASCIENTEST**, est un framework permettant d'identifier et de définir clairement les problèmes auxquels on souhaite répondre, les personas touchés ainsi que les impacts quantifiés, les solutions de contournement et opportunités pour notre application. 

<center>
<img src='assets/synthese_discovery_part_1.png'>

<i>figure 1: Synthèse Discovery 1/2 </i>
<br>

<img src='assets/synthese_discovery_part_2.png'>

<i>figure 2: Synthèse Discovery 2/2 </i>
</center>


## 1.4 Experience Map

L'**Experience Map** est un document de cadrage suivant le parcours entier d'un utilisateur dans sa réalisation d'un objectif. **Il permet de réfléchir l'application par le prisme de l'empathie** en définissant les objectifs et actions, points de douleur & émotions, **pour en dégager des observations et opportunités produit**.

<center>
<img src="assets/xp_map_part_1.png">

<i>figure 3: Experience Map 1/2 </i>
<br>

<img src="assets/xp_map_part_2.png">

<i>figure 4: Experience Map 2/2 </i>
</center>

# 2. Périmètre du projet

Avec la liste des solutions possibles et opportunités Produit déterminées précédemment, nous avons une **base solide sur laquelle baser l'orientation du produit et définir explicitement le périmètre du MVP à présenter**.  

La présence ou non des fonctionnalités sera basée sur plusieurs critères tels que la *valeur ajoutée auprès d'utilisateurs finaux*, la *complexité à implémenter*, ou les *coûts/blocages technologiques*. Chaque arbitrage sera documenté.

## 2.1 Classement des fonctionnalités

L'ensemble des fonctionnalités précédemment identifiées peuvent être regroupée par bloc.

**⚠️ RELIRE A PARTIR D'ICI ⚠️**

 | Bloc fonctionnel | Fonctionnalités constituantes | Besoins couverts | KPIs clés | Dépendance Data Eng
 | :-- | :-- | :-- | :-- | :--
 | **Import & Gestion des POIs** | - Import multi-sources (Google Maps, TripAdvisor, GPX, CSV)<br>- Standardisation/normalisation des données POI<br>- Scoring & priorisation des POIs (étiquetage incontournable vs optionnel)<br>- Détection de contradictions (horaires, catégories) | 1, 5, 6 | % POIs via import vs saisie manuelle<br>% itinéraires sans conflits à J1 | Connecteurs + schéma POI standardisé<br>Pipeline d'ingestion OSM/Places<br>Moteur de détection d'incohérences
 | **Planification assistée** | - Assistant 1-clic (1er brouillon)<br>- Templates intelligents (1j, 2j, thème)<br>- Moteur d'optimisation multi-critères (rapide/éco/relax/panoramique)<br>- Indicateurs explicites (km, temps marche/transport, coûts, réalisme)<br>- Comparateur de scénarios<br>- Arbitrage visuel (trade-offs) | 1, 3, 6 | Temps pour 1er itinéraire réalisable<br>% utilisateurs adoptant la v2 optimisée<br>% recommandations avec justification lisible | Graphe de mobilité multi-modes<br>Solveur TSP + contraintes horaires<br>Moteur d'explanations
 | **Collaboration & Vue unifiée** | - Dashboard unifié (POI + budget + calendrier)<br>- Carte multi-couche (POIs, transports, météo, pistes)<br>- Collaboration temps réel (commentaires, @mentions, votes)<br>- Historique des modifications<br>- Mode groupe avec préférences partagées<br>- Gestion des droits & audit log | 5, 6 | Score de consensus (votes positifs/total)<br>% export réussi sans reformatage | Webhooks/exports<br>Stockage versionné<br>Journal d'événements
 | **Fiabilité & Validation des données** | - Agrégation multi-sources<br>- Validation croisée<br>- MEP d'un indice de fiabilité<br>- Mise à jour automatique et fréquente<br>- Détection de contradictions (horaires, transferts impossibles) | 2, 3 | % itinéraires générés sans conflits J1<br>Taux d'erreurs détectées | Pipeline temps réel<br>Schéma normalisé horaires/prix/durée<br>Moteur de détection d'incohérences
 | **Adaptabilité en temps réel** | - Recalcul dynamique (trafic, météo, horaires, fatigue)<br>- Proposition systématique d'alternatives<br>- Plan B automatique par étape<br>- Notifications intelligentes (alertes contextualisées)<br>- Mode hors-ligne<br>- Score de flexibilité de l'itinéraire<br>- Gestion spécialisée vélo/transports | 4, 1 | % réussite des recalculs acceptés/utiles<br>Temps gagné VS baseline<br>CSAT live | Ingestion quasi temps réel<br>Modèle d'état "nowcasting"<br>Moteur d'alerting & replanification incrémentale
 | **Apprentissage & Boucle post-voyage** | - Rapport post-voyage (kms, coûts, temps, coups de cœur)<br>- Collaborative filtering pour personnalisation<br>- Boucle d'apprentissage des préférences | 6 | NPS/CSAT post-voyage<br>Courbe d'apprentissage pour V+1 | Schéma de télémétrie<br>Feature store<br>Connecteur check-in/acceptation

Une analyse par bloc de chacune des fonctionnalités constituantes nous permettra d'avoir un regard exhaustif concernant l'**Impact**, l'**Effort** et les éventuels **Blocages technologiques**.

### 2.1.1. Bloc 1 : Import & Gestion des POIs

 | Fonctionnalité | Impact | Effort | Blocage technologique | Justification
 | :-- | :-- | :-- | :-- | :--
 | Connecteurs import (Google Maps, GPX, CSV) | 5 | 3 | Oui : Nécessite reverse-engineering des APIs ou web-scraping fiable pour les sources fermées | Sans ça, les utilisateurs saisissent manuellement → aucune adoption. Effort modéré mais dépend des partenariats (Google Maps API, TripAdvisor)
 | Standardisation/normalisation des données POI | 5 | 4 | Oui : Dépend directement de la qualité des sources et de la couverture des champs (horaires, prix, durée, catégories) | C'est la fondation. Mal fait = tout le reste du produit génère des déchets. Effort élevé = ETL + data cleaning + schéma versionné
 | Scoring & priorisation des POIs | 4 | 2 | Non | Relativement simple une fois que les POIs sont standardisés. Formule de scoring personnalisable mais basique suffit pour MVP. Impact fort car c'est l'interface entre la donnée brute et la décision utilisateur
 | Détection de contradictions | 3 | 3 | Oui : Requires rules engine + savoir ce qui sont les "contradictions" valides par domaine | Important pour la fiabilité (cf Besoin 2) mais pas critique au lancement. Les contradictions ne sont détectées que si vos données sont bonnes → dépendance sur standardisation

**Synthèse Bloc 1** : 2 bloqueurs technologiques (connecteurs + standardisation). Ces deux fonctionnalités doivent être faites en premier, même partiellement. Ne pas les faire bien = MVP mort-né.

### 2.1.2. Bloc 2 : Planification assistée

 | Fonctionnalité | Impact | Effort | Blocage technologique | Justification
 | :-- | :-- | :-- | :-- | :--
 | Assistant 1-clic (1er brouillon) | 5 | 4 | Oui : Dépend d'un solveur TSP opérationnel (même basique) + graphe de mobilité | C'est la "killer feature" promesse du produit. Mais ça repose sur le bloc 1 (POIs fiables) ET sur un moteur d'optimisation fonctionnel. Effort = implémentation solveur + heuristiques
 | Templates intelligents | 3 | 2 | Non | Nice-to-have. Simple à faire (quelques JSON + presets). Impact moyen = accélère les utilisateurs non-techno mais n'est pas fondamental. Peut être V1.1
 | Moteur multi-critères (rapide/éco/relax/panoramique) | 5 | 5 | Oui : Requires solveur multi-objectifs (complexité P-NP), matrice de coûts fiable (temps, distance, coûts), graphe de mobilité | C'est le cœur du produit. Très coûteux (recherche + optimisation). Peut être simplifié en V1 (ex: 2 modes au lieu de 4) mais doit être là
 | Indicateurs explicites (km, temps, coûts, réalisme) | 4 | 2 | Non | Facile si le solveur calcule ça. Impact fort = crée la confiance utilisateur dans les recommandations. Dépend du bloc 1 (données fiables)
 | Comparateur de scénarios | 3 | 2 | Non | UI/UX sur les résultats du solveur. Simple mais dépend que le solveur fasse plusieurs scénarios. Impact moyen = "nice" pour décideurs indécis
 | Arbitrage visuel (trade-offs) | 3 | 3 | Non | Dataviz + UI interactive. Modérément complexe, impact moyen = aide à la prise de décision mais pas critique si les indicateurs sont lisibles

**Synthèse Bloc 2** : 2 gros bloqueurs (assistant 1-clic + moteur multi-critères). Le solveur est la dépendance centrale. Conseil : démarrer avec un solveur simplifié en V1 (ex: TSP classique sans vraiment optimiser sur 4 critères) puis enrichir.

### 2.1.3. Bloc 3 : Collaboration & Vue unifiée

 | Fonctionnalité | Impact | Effort | Blocage technologique | Justification
 | :-- | :-- | :-- | :-- | :--
 | Dashboard unifié (POI + budget + calendrier) | 4 | 3 | Non | Dépend que vous ayez les données POIs + calculs de budget/temps (bloc 1+2). UI/UX complexe mais no blocker tech. Impact fort = c'est comment les utilisateurs voient le trip
 | Carte multi-couche | 3 | 4 | Oui : Requires APIs cartographie (Mapbox, Google Maps) + intégration météo/trafic temps réel | Très coûteux techniquement (multi-source, perf). Impact moyen = "beau" mais pas critique pour fonctionner. Peut être dégradé à une seule couche en V1
 | Collaboration temps réel (commentaires, @mentions, votes) | 4 | 4 | Oui : Requires WebSocket / real-time DB (Firebase, Postgres avec subscriptions) + gestion des conflits de concurrence | Impact fort = proposition de valeur clé pour les groupes. Mais coûteux en infra et bugs de sync. Peut être dégradé à "refresh manuel" en V1
 | Historique des modifications | 2 | 2 | Non | Facile si vous versionnez vos données (audit log). Impact faible mais "must have" légalement/pour UX (undo).
 | Mode groupe avec préférences partagées | 3 | 2 | Non | Logique métier simple (shared settings). Dépend que votre modèle de données supporte les groupes.
 | Gestion des droits & audit log | 2 | 2 | Non | Standard (RBAC basique). Facile mais souvent oublié, important pour la fiabilité de la collaboration

**Synthèse Bloc 3** : 2 bloqueurs (maps multi-couche + collab temps réel), tous deux coûteux. Stratégie V1 : dashboard + mode groupe basique, collaboration en "refresh manuel" (pas WebSocket), une seule couche de carte.

### 2.1.4. Bloc 4 : Fiabilité & Validation des données

 | Fonctionnalité | Impact | Effort | Blocage technologique | Justification
 | :-- | :-- | :-- | :-- | :--
 | Agrégation multi-sources | 4 | 3 | Oui : Dépend que vous ayez plusieurs sources connectées (bloc 1) + règles de fusion de données | Impact fort = c'est comment vous montez en fiabilité. Mais ça suppose déjà que vous avez 2+ sources. Peut être monophage en V1
 | Validation croisée | 3 | 3 | Oui : Requires heuristiques/règles métier pour détecter les contradictions (ex: si 3 sources disent 10€ et 1 dit 100€, laquelle croire ?) | Modérément coûteux. Impact moyen = améliore la confiance mais n'est pas critique si une seule source
 | Indice de fiabilité | 3 | 2 | Non | Facile si vous agrégez les sources (simple formule). Impact moyen = donne de la transparence à l'utilisateur
 | Mise à jour automatique et fréquente | 2 | 2 | Oui : Requires infrastructure d'ingestion temps réel (webhooks, scheduled jobs) | Impact faible en V1. Peut être batch quotidien au lieu de temps réel. Mais dépend de votre infra
 | Détection de contradictions (horaires, transferts impossibles) | 4 | 3 | Oui : Requires rules engine + vérification logique (ex: "transfert bus-musée en 5 min" dans quartier X ?) | Impact fort = évite les itinéraires non-réalisables. Coûteux mais critique pour la crédibilité du produit

**Synthèse Bloc 4** : 3 bloqueurs légers (agrégation + validation + détection). Tous dépendent d'avoir des données de bonne qualité. Stratégie V1 : monosource + détection basique des horaires impossibles, pas de validation croisée.

### 2.1.5. Bloc 5 : Adaptabilité en temps réel

 | Fonctionnalité | Impact | Effort | Blocage technologique | Justification
 | :-- | :-- | :-- | :-- | :--
 | Recalcul dynamique (trafic, météo, horaires, fatigue) | 4 | 5 | Oui : Requires ingestion temps réel + modèle "nowcasting" + moteur de replanification incrémentale. Triple combo complexe | Impact fort pendant le voyage mais MVP peut survivre sans. Très coûteux = À DÉGAGER du V1
 | Proposition d'alternatives | 3 | 3 | Non | UI pour montrer les Plan B. Simple si le solveur les calcule. Dépend du bloc 2 (solveur).
 | Plan B automatique par étape | 3 | 3 | Oui : Requires stocker N itinéraires vs juste 1, + logique de "basculement intelligente" | Modérément coûteux. Impact moyen = utile mais pas critique si l'utilisateur peut resigner manuellement
 | Notifications intelligentes | 2 | 4 | Oui : Requires websocket + règles push (ex: "musée ferme 45 min") + traitement temps réel | Impact faible en V1. Très coûteux. À DÉGAGER du V1
 | Mode hors-ligne | 2 | 4 | Oui : Requires gestion de cache, sync incrémentale, résolution des conflits après reconnexion | Impact faible (niche = pauvres connexions). Très coûteux. À DÉGAGER du V1
 | Score de flexibilité | 2 | 2 | Non | Simple métrique si vous gardez trace des alternatives/plan B. Impact faible = curiosity feature
 | Gestion spécialisée vélo/transports | 3 | 3 | Oui : Requires APIs spécialisées (routage vélo distinct, GTFS pour transports) + graphe dédié | Impact moyen = couvert par certains personas. Dépend de la disponibilité des APIs. Peut être V1.1

**Synthèse Bloc 5** : DANGER : ce bloc est une graveyard de bonnes idées trop coûteuses. À laisser largement de côté en V1. Garder : proposition d'alternatives (basique) + score flexibilité. Dégager : recalcul dynamique, notifications, hors-ligne.

### 2.1.6. Bloc 6 : Apprentissage & Boucle post-voyage

 | Fonctionnalité | Impact | Effort | Blocage technologique | Justification
 | :-- | :-- | :-- | :-- | :--
 | Rapport post-voyage | 2 | 2 | Non | Simple agrégation des metrics du voyage. Impact faible = nice-to-have pour nostalgie. Peut être V1.1
 | Collaborative filtering | 2 | 5 | Oui : Requires machine learning infra (feature store, pipeline d'apprentissage) | Impact moyen long-terme (améliore les reco au voyage suivant) mais très coûteux. À DÉGAGER du V1
 | Boucle d'apprentissage des préférences | 2 | 4 | Oui : Requires télémétrie fine (check-in, acceptation des suggestions) + feedback loop | Impact moyen. Coûteux. À DÉGAGER du V1

**Synthèse Bloc 6** : ML/apprentissage = trop coûteux pour V1. Garder seulement le rapport (cosmétique) et des hooks télémétrie basiques pour préparer l'ML de V2.

## 2.2. Synthèse globale : Matrice arbitrage MVP

 | Priorité | Fonctionnalités | Impact | Effort | Blocage technologique | Recommendation
 | :-- | :-- | :-- | :-- | :-- | :--
 | MUST (V1 critique) | Connecteurs import | 5 | 3 | Oui | À faire en premier — sans ça, pas d'adoption
 |  | Standardisation POI | 5 | 4 | Oui | À faire en premier — fondation de tout
 |  | Assistant 1-clic (simplifié) | 5 | 4 | Oui | À faire — promise du produit, mais version lite (1 mode, pas 4)
 |  | Moteur multi-critères (basique) | 5 | 5 | Oui | À faire en v1 — coeur du produit, mais limiter à 2-3 modes max, pas 4
 |  | Dashboard unifié | 4 | 3 | Non | À faire — c'est comment les gens visualisent. No-brainer
 |  | Scoring & priorisation POI | 4 | 2 | Non | À faire — facile, valeur forte
 |  | Indicateurs explicites | 4 | 2 | Non | À faire — crée la confiance, trivial si solveur OK
 | SHOULD (V1 intéressant) | Détection de contradictions | 4 | 3 | Oui	À inclure si temps — important pour crédibilité. Effort modéré.
 |  | Mode groupe + préférences partagées | 3 | 2 | Non | À inclure — facile, améliore UX groupe
 |  | Historique des modifications | 2 | 2 | Non | À inclure — facile, legal+UX
 |  | Gestion droits & audit log | 2 | 2 | Non | À inclure — standard, facile
 |  | Gestion spécialisée vélo/transports | 3 | 3 | Oui | À considérer — impact moyen, coûteux, dépend APIs dispo. Peut être V1.1
 | COULD (V1 optionnel) | Comparateur scénarios | 3 | 2