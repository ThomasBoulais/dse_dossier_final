## Executive Summary

A partir de la Discovery 2 profils utilisateurs distincts ont émergé : la **Planificatrice pragmatique** et l'**Explorateur flexible**. Leurs besoins et attentes au niveau de l'application sont différents mais convergent techniquement vers un moteur unique capable de générer ET d'ajuster des itinéraires.

Le MVP recommandé **priorise 6 fonctionnalités MUST-HAVE** (fondées sur dépendances technologiques strictes) puis **5 SHOULD-HAVE** qui amplifient la valeur. Cette approche délivre un produit viable en **10-12 semaines** pour une petite équipe, sans dette technique.


## 1. Les deux personas et leurs besoins

| **Critère** | **Planificatrice pragmatique** | **Explorateur flexible** |
|---|---|---|
| **Profil** | 25-34 ans, petit groupe, tech-savvy, Excel + Maps | 25-45 ans, solo/duo, cherche expériences authentiques |
| **Objectif principal** | Voir un max sans fatigue • Respecter budget/horaires • Trajets optimisés | Sortir des sentiers battus • Garder liberté sur place • Pas de rigidité imposée |
| **Frustrations** | Imprévus • Infos incomplètes/obsolètes • Outils manuels non connectés | Itinéraires rigides • Lieux trop touristiques • Pas d'alternatives proposées |
| **Attentes** | Optimisation auto + ajustement dynamique + visualisation compromis | Reco adaptées à leurs goûts + itinéraires "beaux" + scénarios alternatifs |

### Insight clé

**Les deux personas convergent vers une seule solution technique** : un moteur qui génère l'itinéraire optimal ET permet de l'ajuster/substituer sans le recalculer entièrement. La Planificatrice utilise la rigidité initiale pour gagner du temps ; l'Explorateur utilise la flexibilité post-génération pour garder sa liberté.

## 2. Stratégie MVP : Hiérarchie fonctionnelle et dépendances

Les différentes étapes de réalisation sont forcées par les dépendances. La standardisation des POIs par exemple, est primordiale pour les autres actions et doit être réalisée en amont de celles-ci.


 | Durée | Action
 | :-- | :--
 | Semaines 1-3 | Standardisation des POIs, puis attribution d'un score d'attractivité
 | Semaines 3-7 | Moteur multi-critères
 | Semaines 4-6 | Dashboard unifié et Indicateurs explicites
 | Semaines 6-7 | 1ère version d'itinéraire en 1 clic
 | Semaines 5-8 | Détection contradictions + Mode groupe (si assez de temps)


## 3. Spécification MUST-HAVE (6 fonctionnalités)

### M1 - Standardisation des POIs 
*Semaines 1-3, Effort 4/5, Impact 5/5*

**Spécification** : un schéma unique pour tous les POIs : le nom, les types & sous-type  (culture/nature/restauration/loisir), la durée visite (min), les coûts (€), les périodes et horaires d'ouverture, la localisation (lon/lat), les informations descriptives du POI.

**Source V1** : APIs pour les 2 sources OSM & DATAtourisme. Validation basique : horaires valides, prix numérique, durée > 0.

**KPI succès** : taux de colonnes remplies et normalisées (notamment pour la localisation, les types/sous-types et les horaires d'ouverture) > 95%

**Impact personas** :
- **Planificatrice** : avoir des données fiables est essentielle, permettant de pouvoir calculer les métriques comme le budget, le temps ou la distance
- **Explorateur** : mettre en place un tag d'intérêt "authentique" permet de les valoriser via le score de chaque POI


### M2 - Moteur multi-critères (basique - 1 mode) 

*Semaines 3-7, Effort 5/5, Impact 5/5*  

**Spécification** : le générateur d'itinéraire est optimisé sur **1 seul critère en V1 : "profit maximisé"** (cumul du score des POIs sous contrainte temporelle).

- **Entrée** : la date et l'heure de départ, le nombre de jours de voyage et le point de départ
- **Sortie** : l'ordre de visite optimal, l'heure arrivée/départ pour chaque POI • l'heure d'arrivée finale, la durée totale de transport
- **Contraintes** : respecte les horaires d'ouverture des POIs, doit trouver une restauration sur les créneau de midi et du soir, doit trouver un logement en fin de journée
- **Algo** : Modèle de Reinforcment Learning qui apprend de son environnement

**Non considéré pour le MVP** : les pondérations personnalisables, les modes "Budget" / "Eco" / "Relax" / "Rapide". Ces modes seront définies dans la V1.1.

**KPI succès** : génère itinéraire faisable (horaires respectés) > 95% cas, satisfaction moteur > 7/10

**Impact personas** :
- **Planificatrice** : passer en automatique l'optimisation réalisée manuellement à ce jour
- **Explorateur** : légitimer le point de départ à partir duquel il sera possible de négocier les modifications


### M3 - Dashboard unifié 

*Semaines 4-6, Effort 3/5, Impact 4/5*

**Spécification** : un écran central avec les POIs sélectionnés à gauche, la carte simple au centre, la timeline itinéraire à droite et les métriques en bas.

- **Affichage** : la liste des POIs avec pour chacun leur score, coûts, heure arrivée/départ, la durée de la visite, la durée du transport, et le coût et la distance parcourure au total
- **Interactivité** : un clic peut ajouter/retirer un POI, possibilité de glisser-déposer, réordonner, modifier le temps d'une visite
- **Pas inclus en V1** : la collaboration temps réel, les différentes couches sur la carte, le recalcul dynamique

**KPI succès** : les utilisateurs trouvent une info en moins de 10 secondes, et la satisfaction est supérieure à 8/10

**Impact personas** :
- **Planificatrice** : avoir une vue unifiée sur une seule app
- **Explorateur** : voir le flow et identifier où il est possible d'effectuer des modifications


### M4 - Scoring & Priorisation POI 

*Semaines 2-3, Effort 2/5, Impact 4/5*

**Spécification** : chaque POI reçoit un score de 1 à 5 étoiles. C'est une combinaison de la note utilisateur (1-5) si elle est renseignée + de la valeur de tag "authentique" (2x poids) vs "mainstream".

**Formule simple** : (note_utilisateur + 2 × tag_authentique) / 3

**Pas en V1** : les filtres collaboratifs, un système de rang basé sur la popularité

**KPI succès** : 90% POI scorés, les utilisateurs disent que le "*score les aide à décider*"

**Impact personas** :
- **Planificatrice** : voir rapidement le ROI pour chaque POI (coût/temps VS intérêt)
- **Explorateur** : découvrir des POIs moins touristiques grâce au tag "authentique"


### M5 - Indicateurs explicites 

*Semaines 5-6, Effort 2/5, Impact 4/5*

**Spécification** : chaque itinéraire généré affiche :
- **des Chiffres clés**, comme le total de POIs visité, de km parcourus, de durée de visite, de durée de transport, de coût estimé
- **Indice de confiance** = 1 - (% POI données incomplètes). Par exemple, si 10% des POIs de l'itinéraire sont sans horaires, l'indice de confiance est à 90%
- **Format** : 5 grands nombres visibles en dessous de la carte

**Calcul** : Mis à part l'indice de confiance, les autres valeurs sont la somme des données standardisées

**KPI succès** : les utilisateurs disent qu'ils ont confiance dans ces indicateurs, les valeurs calculées estimés vs réalité sont fiables à plus de 85%

**Impact personas** :
- **Planificatrice** : **besoin client clef**, avoir une visualisation explicite présentant les compromis
- **Explorateur** : comprendre pourquoi cet itinéraire a été proposé pour décider de le modifier


### M6 - 1ère version en 1 clic

*Semaines 6-7, Effort 4/5, Impact 5/5*

**Spécification** : un bouton "Générer itinéraire" qui prend les contraintes (nombre de jour, lieu de départ) et retourne un itinéraire prêt pour discussion

- **UI** : 1 bouton + 1 bandeau avec les critères + 1 indicateur de chargement
- **Pas de sélection de mode** : trop complexe pour la V1, on reste sur un mode unique de voyage pour le moment
- **Output** : 1 itinéraire optimal unique, modifiable après coup et pouvant être relancé manuellement

**KPI succès** : 80% utilisateurs réussissent à générer l'itinéraire sans aide,satisfaction UX supérieure à 7/10

**Impact personas** :
- **Planificatrice** : **gain clé**, gagner beaucoup de temps sur la préparation en amont (passage de 4-6h à 2 min pour un premier jet exploitable)
- **Explorateur** : obtenir un point de départ pour discussions ("*bon qu'est-ce qu'on en pense ?*", "*ok là on change ça*")


## 4. SHOULD-HAVE : Fonctionnalités complémentaires 

Les fonctionnalités suivantes sont les SHOULD-HAVE identifiées précédemment, et sont à implémenter une fois les MUST-HAVE réalisées et s'il reste du temps disponible.

| **Fonctionnalité** | **Effort** | **Impact** | **Recommandation** | **Condition** |
|---|---|---|---|---|
| **Détection contradictions** | 3 sem | Haute | **Forte valeur, à inclure** | Le moteur et la standardisation des POIs sont opérationnels |
| **Mode groupe** | 2 sem | Haute | **Ouverture aux groupes, à inclure** | Le dashboard est opérationnel |
| **Historique modifications** | 2 sem | Moyenne | Si possible, sinon V1.1 | Après le mode groupe |
| **Gestion droits & audit** | 2 sem | Moyenne | Si possible, sinon V1.1 | Complément mode groupe |
| **Gestion vélo/transports** | 3 sem | Moyenne | A passer dans la V1.1 | Dépend des APIs GTFS à notre dispo |

## 5. Recommandations finales

Les recommandations quant à la Road Map sont les suivantes :  

| **Fonctionnalité** | **Raison** | **Quand** |
|---|---|---|
| Collaboration en temps réel (WebSocket) | Effort 4 sem  + coût infra élevé + delta UX faible VS raffraîchissement manuel | V1.1 |
| Comparateur de scénarios | Effort 2 sem + UI complexe | V1.1 |
| Carte multi-couches (météo/transport) | Effort 4 sem + coûts APIs | V2 |
| Recalcul dynamique (trafic live) | Effort supérieur à 5 sem (gestion du trafic en live) + besoin niche (voyage en cours) | V2 |

En terme de calendrier, la temporalité est la suivante : 
- **Semaines 1-4** : Standardisation POI + Ajout d'un score basique
- **Semaines 4-9** : Moteur multi-critères
- **Semaines 5-8** : Dashboard & Indicateurs + 1ère version en 1 clic
- **Semaines 9-12** : Tests beta + fix critiques, puis enfin lancement auprès d'un nombre d'utilisateurs restreints (entre 10 et 20 beta testeurs)

### Points de pivots potentiels

| **Point de pivot** | **Critère** | **Sinon** |
|---|---|---|
| **Pivot 1 (sem 9)** | Le moteur génère des itinéraires faisables > 95% | Revisiter le modèle jusqu'à obtention d'une précision suffisante |
| **Pivot 2 (sem 12)** | Beta test CSAT > 7/10 | Ajuster UX avant lancement |
| **Pivot 3 (sem 4 après lancement)** | NPS > 30 | Pivot vers fonctionalités X ou Y |


## Conclusion

Le produit résout un problème réel : réduire drastiquement le temps de planification pour la **Planificatrice**, et définir un cadre pour l'**Explorateur** qui lui permet de garder sa liberté tout en ayant point de départ crédible.  

Le MVP concentre les ressources à dispo sur les **6 MUST-HAVE** fondés sur des dépendances technologiques strictes. Les **5 SHOULD-HAVE** amplifient la valeur s'il reste du temps à notre disposition.  

Le **succès de l'application dépend de 2 blocages technologiques** : avoir des données POIs normalisées, et un modèle entraîné donnant des résultats fiables. Ces points cruciaux seront à adresser dans les premières semaines de développement.

Une fois prêt au lancement, un passage en **beta communauté fermée** pour apprendre est préconisé avant de définir plus clairement la Road Map pour les versions suivantes.