# Rapport de veille - Itinéraire de voyage

*Rédaction : Thomas BOULAIS*  
*Veille réalisée le 22/12/2025*  

## 1. Contexte et objectif de la veille
Le projet vise à concevoir un système de **génération d’itinéraires de voyage optimisés** sous contraintes, *par exemple temporelles, préférences, faisabilité, arbitrage en cas d’imprévu* en intégrant les exigences **RGPD**, **RGAA** et **RSE** (écologie + inclusion handicap).  

L’objectif de la veille est d’identifier, à partir d’applications de planification de voyages existantes, les **cas d’usage**, **tendances produit**, et **outils/briques** dont on pourra s'inspirer et/ou réutiliser, afin de justifier la stratégie de conception du moteur d’itinéraires optimisés.

## 2. Stratégie de veille

### 2.1 Informations recherchées
Les fonctionnalités recherchées sont celles pouvant servir de briques pour un système d’itinéraires optimisés :
- **Planification** : gestion de l'organisation des jours/lieux/horaires
- **Proposition automatique d'itinéraire** VS **si l'itinéraire doit être généré et/ou récupéré manuellement**
- **Optimisation** : présence (ou pas) d’un moteur **multi-critère** (temps, fatigue, contraintes optionnel/obligatoire, préférences utilisateur)
- **Arbitrage** : aide à choisir entre plusieurs contraintes, gestion d’un **plan B** en cas d’imprévu
- **Mutualisation / collaboration** : partage et co-édition du planning asynchrone ou en live
- **Adaptation de l'itinéraire** : recalcul de l’itinéraire/position et guidage lié aux points d’intérêt
- **Mode hors-ligne** : enregistrement de l'itinéraire, voire d'alternatives en cas d'imprévu
- **Checklists/Inventaires** : générique pour des types de voyage (*par exemple documents officiels + visa si changement de pays*)
- **Budget** : capacité de faire une estimation, de suivre les dépenses journalières
- **Réservation** : possibilité de réserver des vol/moyen de locomotion/hébergement/activités (gestion native ou renvoi vers les bons liens, visibilité des infos externes depuis l'app)

### 2.2 Canaux exploités

L'article suivant listant les ***"best travel apps"*** est la source depuis lequel les applications comparant les offres ont été analysées : https://www.pcmag.com/picks/best-travel-apps?test_uuid=04IpBmWGZleS0I0J3epvMrC&test_variant=A#travel-apps-for-recommendations

Chacune des applications a ensuite été vérifiée en explorant les pages web présentant les produits, et un filtre a été fait pour ne conserver que les applications dans le périmètre, soit 5 apps sur les 29 introduites dans l'article.

### 2.3 Critère de sélection

Les applications ont été distribuées parmi 3 catégories : `planning &    organizing`, `recommendations` et `search & booking`. Notre cas d'étude conserve uniquement les applications relevant du périmètre :
- **Type attendu** : `planning & organizing`
- **Priorité** : apps offrant des briques proches d'un planning (collaboration, POIs, hors-ligne, checklist, budget, etc.)
- **Hors périmètre** : les apps comparable à des **plateformes de recommandations** ou des **hubs de réservation** sans composante d’itinéraire sont écartés de la veille

Cette sélection explique pourquoi plusieurs candidats visibles sur la liste initiale ont été exclus : ils ne satisfont pas l’impératif de génération d’itinéraires optimisés.

### 2.4 Vérification et actualisation des sources
Pour chaque application retenue, la vérification porte sur :
- la présence de fonctionnalités annoncées (*ex. collaboration, hors-ligne, budget, POIs*),
- et surtout l’existence (ou non) d’un **moteur d’optimisation** multi-critère et d’une **aide à l’arbitrage**.

## 3. Sources retenues et traitement
Les sources suivantes ont été retenues pour la veille (issues du comparatif initial, puis triées selon le scope).

### 3.1 Tableau des sources réelles
| Nom | Type | URL | Points forts | Limites / pistes d’amélioration |
|---|---|---:|---|---|
| WanderLog | planning & organizing | https://wanderlog.com/fr | - collaboration <br>- optimisation d'itinéraire selon les points placés<br>- assistant IA<br>- accès hors ligne<br>- bugétisation<br>- possibilité de réservation (vol/voiture/hébergement)<br>- checklist / inventaire<br>- guide de voyage<br>- mode plan<br>- mutualisation de toutes les fonctions nécessaires | - mis à part l'agent AI, **pas de proposition d'itinéraire automatique**<br>- pas de moteur d'optimisation multicritère (horaire, fatigue, optionnel/obligatoire)<br>- pas d'option B en cas d'imprévu<br>- pas d'aide à l'arbitrage | 
| Stippl | planning & organizing | https://www.stippl.io | - collaboration<br>- mutualisation de toutes les fonctions nécessaires<br>- gestion des documents de réservation<br>- assistant AI<br>- possibilité de prendre abonnement eSim<br>- checklist / inventaire<br>- interface planner chouette<br>- gestion budget (type tricount + catégorisation dépenses) | - mis à part l'agent AI, **pas de proposition d'itinéraire automatique**<br>- pas de moteur d'optimisation multicritère (horaire, fatigue, optionnel/obligatoire)<br>- pas d'option B en cas d'imprévu<br>- pas d'aide à l'arbitrage |
| Komoot | planning & organizing | https://www.komoot.com/fr-fr/smarttour/e1035107064/le-pont-d-arc-boucle-dans-la-reserve-naturelle-des-gorges-de-l-ardeche | - compatibilité avec des appareils & services<br>- ajout de POIs on the flow + recalcul auto de la position<br>- indique des infos liées à la route (distance, temps estimé, déniv +/-, difficulté, profil de l'élévation)<br>- possibilité de partager/récupérer un itinéraire depuis POIs<br>- description POIs + lien vers les sources | - plutôt pensé pour un format de randonnée<br>- **pas de proposition d'itinéraire automatique**, l'itinéraire doit être créé manuellement et/ou récupéré d'un autre itinéraire déjà présent |
| RoadTrippers | planning & organizing | https://roadtrippers.com | - UX très clair pour la génération d'itinéraire : *funnel point de départ/arrivée > dates > nb de voyageurs > budget bouffe/dodo/POI > type de stops intéressants > stops incontournables > génération* | - disponible uniquement aux USA <br>- l'itinéraire prend en charge uniquement les trajets en voiture  <br>- le passage au modèle premium après génération d'itinéraire empêche l'accès aux fonctionnalités <br>- impossible de savoir si le moteur d'optimisation est multi-critère, si des options de secours sont proposées, s'il existe de l'aide pour l'arbitrage |
| Tripomatic | planning & organizing | https://maps.tripomatic.com/?utm_source=tripomatic_web&utm_medium=cta&utm_campaign=homepage#/ | - interface interactive claire (planification de nouveaux voyages soi-même ou avec l'aide d'un LLM, retour sur d'autres voyages organisés, moteur de recherche de logements avec filtres) | - mis à part l'agent AI, **pas de proposition d'itinéraire automatique**<br>- impossibilité de générer un itinéraire sans créer de compte  |


### 3.2 Tri : extraction par thèmes
La veille permet de structurer les résultats en 4 axes directement reliés au projet :
- **Briques d’organisation** : collaboration, checklist, mode hors-ligne, guides
- **Briques “parcours”** : suggestion de POIs, recalcul, infos de route
- **Gestion de la logistique** : budget, réservation, liens et documents
- **Génération/optimisation** : ce qui existe réellement comme solveur multi-criètres avec arbitrage (on remarque que dans la majorité des cas, s'il existee il s'agit plutôt d'un *ajustement guidé*)

## 4. Synthèse des résultats et cas d’usage

### 4.1 Tendances dominantes
Les apps étudiées couvrent bien la **logistique** du voyage, que ce soit l'organisation, la collaboration, le budget, un mode hors-ligne, une checklist. Cependant l'algorithme de génération d'itinéraire optimisé (multi-critère + arbitrage + plan B) est rarement au centre de l’expérience.  

- **Collaboration & mutualisation** : utiles pour un planning co-construit, *présentes chez WanderLog et Stippl*
- **Budget & documents** : essentiels pour aligner contraintes “réelles” du voyage, *présents chez WanderLog et Stippl*
- **POIs & recalcul** : avec recalcul de trajectoire/localisation, *plus présents sur des apps orientées parcours comme Komoot*
- **Optimisation** : s'agit plutôt d'un ajustement guidé (càd la génération d'un itinéraire à partir de POIs déjà renseignés) plutôt qu’un **moteur multi-critère** contrôlé par des contraintes utilisateur complètes

### 4.2 Manques/écarts majeurs vis-à-vis du projet

L'boservation des applications de la veille posent les limites suivantes  :
- **Proposition d’itinéraire automatique** uniquement présent sur *RoadTrippers*, la majorité intègre un LLM pour suggestion d'idées, et l'itinéraire est à créer manuellement ou récupéré sur *Komoot*
- **Pas de moteur d’optimisation multi-critère** explicite et contrôlable
- **Absence d’option B** systématique en cas d’imprévu
- **Peu/pas d’aide à l’arbitrage**, l’utilisateur n’est pas guidé dans le choix entre contraintes

Ces manques motivent la proposition de valeur du projet : intégrer une génération d’itinéraire qui traite les contraintes comme des éléments de décision (multi-critère), puis propose des alternatives en cas d’aléas.

### 4.3 Cas d’usage & briques à intégrer dans le projet

Les blocs suivants sont des opportunités Produit à essayer au maximum de prioriser dans la conception de la solution : 
- **Co-planification** : collaboration du planning (inspirée de *WanderLog* et *Stippl*).
- **Préparation et suivi** : checklist/inventaire + guide + mode hors-ligne (inspirés de *WanderLog* et *Stippl*).
- **POIs et recalcul “en cours de route”** : intégrer la logique de POIs incontournables et recalcul (inspirés de *Komoot*).
- **Budgétisation et réservations** : budget + gestion des documents (inspirées de *WanderLog* et *Stippl*).
- **Génération optimisée** :
  - optimisation multi-critère,
  - arbitrage explicite (ou semi-guidé) quand des contraintes entrent en conflit,
  - proposition d’un **plan B** en cas d’imprévu.

## 5. Cadre réglementaire et impacts (RGPD, RGAA, RSE)

### 5.1 Impacts des RGPD sur la conception
Un système d’itinéraires optimisés peut manipuler des données comme :
- **des comptes & préférences**, avec pour finalité de personnaliser l’itinéraire, 
- **des données de réservation/documentation**, avec pour finalité d'organiser le voyage, 
- **d'éventuels historiques de destinations**, **POIs choisis**, **préférences de mobilité**, 
- et **possiblement des données de localisation** si guidage/recalcul en cours de route.

Les impacts concrets suivants sont donc à prévoir :
- **Minimisation** : ne collecter que ce qui est nécessaire pour l’itinéraire
- **Finalité et transparence** : expliquer pourquoi certaines données sont utilisées (optimisation, affichage, hors-ligne, etc.)
- **Sécurité** : protéger l’accès aux plannings et aux documents de réservation (ou considéré hors périmètre)
- **Droits utilisateurs** : permettre l'export et la suppression si applicable dans le produit
- **Durée de conservation** : limiter et documenter la durée pour préférences/historiques

### 5.2 Impacts RGAA (accessibilité)
L’outil doit rester utilisable par des personnes en situation de handicap. Impacts typiques :
- navigation clavier, focus visible, libellés de champs accessibles,
- contrastes suffisants, taille et choix de police lisible,
- alternatives textuelles pour contenus non textuels (ex. cartes/itinéraires),
- formulaires de saisie de contraintes compréhensibles et utilisables avec des technologies d’assistance.

### 5.3 Impacts RSE (écologie + inclusion handicap)

L'outil doit prendre en considération l'**Écologie** :
- en réduisant au possible les replanifications non maîtrisées pour ne pas augmenter les déplacements “subis” et la consommation liée
- le moteur d’itinéraires peut proposer des options réduisant les distances ou favorisant les modes alternatifs de transport

L'intégration des contraintes de mobilité va dans le sens de l'**Inclusion handicap**, notamment sur : 
- l'explicitation au niveau de l'accessibilité des lieux/itinéraires quand l’information est disponible,
- la formulation simple des contraintes (par exemple “éviter escaliers”, “temps de marche limité”, “préférer itinéraires accessibles”),
- la capacité à offrir des itinéraires alternatifs cohérents avec ces contraintes.

## 6. Conclusion
La veille montre que les applications existantes se distinguent surtout sur :
- la **logistique** (collaboration, budget, documents, hors-ligne, checklist),
- et parfois le **parcours/POIs** (recalcul et informations route),

mais rarement sur :
- une **génération automatique d’itinéraire**,
- une **optimisation multi-critère** contrôlable (horaire, fatigue, optionnel-obligatoire, préférences),
- une **aide à l’arbitrage**,
- et une **gestion structurée du plan B**.

Le projet peut donc se différencier en construisant un moteur d’itinéraires optimisés qui traite les contraintes comme des leviers de décision, tout en respectant les RGPD sur les données privées, le RGAA sur l'amélioration de l'accessibilité et la RSE sur les sujets d'écologie et d'inclusion.
