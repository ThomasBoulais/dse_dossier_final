# Rapport préliminaire - Itinéraire de voyage

*Rédaction : Thomas BOULAIS*

Le projet est la **création d’une application web** qui permet de proposer à l’utilisateur **un itinéraire de voyage optimisé** à partir de contraintes renseignées comme la durée ou l’endroit désiré.

L’objectif de ce document est d’avoir un **premier contact avec le sujet** au travers des sources de données à notre disposition. Une fois analysées, l’émergence des **lacunes actuelles** devrait permettre de définir la ou les **problématiques métiers** au(x)quel(s) la mise en place d’une **plateforme de données** est une solution adéquate. Après une brêve synthèse des parties précédentes, nous concluerons sous forme d'ouverture en direction des **opportunités Produit** potentielles pour l’application à développer.

## Lexique
- **POI(s)** : Points d’intérêt (*Point Of Interest*)
- **OSM** : OpenStreetMap
- **DT** : DATAtourisme
- **RDB** : base de données relationnelles
- **ODbL** : contrat de licence favorisant l’utilisation des données (Open Database Licence)

## Analyse exploratoire des flux de données

#### 1.1. Identifier les sources de départ

Notre point de départ est de découvrir et étudier les sources de données à notre disposition. Après une brève description de chacune d’entre elles, nous verrons leur structure de données, identifierons les étapes de transformation nécessaires à leur interopérabilité et présenterons la nouvelle base de données prête à être consommée par l’application cible.

#### 1.1.a. DATAtourisme

DATAtourisme est une plateforme nationale pour les données d’offres touristiques en territoire français. En agrégeant, normalisant, qualifiant et diffusant en open data les données institutionnelles d’information touristiques, ses objectifs sont de faciliter l’accès aux données publiques, valoriser l’offre touristique des territoires et favoriser la création de services innovants.  

La donnée, sous format JSON-LD, est récupérable via le site https://diffuseur.datatourisme.fr en associant la création d’un flux (webservice) avec la clef API associée à l’application. Sa structure est articulée en modèle sémantique: chaque élément, propriété, relation et contrainte est stockée de telle sorte que leur définition soit explicite, contrairement aux RDB où la clef étrangère d’une table n’a de sens qu’avec une interpolation ou explication fonctionnelle de celle-ci.

<center><img src='assets/KnowledgeGraph_DataTOURISME.png' width=600></center>
<center>*figure 1: schéma d’un fragment du modèle sémantique DATAtourisme*</center><br>

Accompagnée de son ontologie (https://www.datatourisme.fr/ontology/core) l’exploration de la donnée nous apprend que les POIs (Points Of Interests) sont répartis en 4 types de POI (lieu, fête et manifestation, produit, itinéraire touristique), avec un grand nombre de tags métiers présents ou pas selon le type et les sous-types des POIs.  

Dans notre cas d’étude et en préparation du projet d’itinéraire de voyage, le point d’attention se fera autour des champs issus des familles suivantes : 
- **nom**
- **informations générales**
- **géométrie & localisation**
- **types et sous-types**
- **périodes & horaires d’ouverture**

// présenter les TYPE ET SOUS-TYPE  
// présenter la GEOMETRIE

Pour la gestion des horaires d’activité un schéma structuré existe, on remarque cependant qu’une partie des points de données observés renseigne ces informations dans le tag “additionalInformation” à la place pour renseigner textuellement les horaires.

#### 1.1.b. OSM

OpenStreetMap (OSM) est une source mise en place par la fondation OpenStreetMap dont les données sont issues de production participative avant d’être mise à disposition sous licence ODbL (Open Database Licence, contrat licence favorisant la libre circulation des données). Ces données couvrent les données publiques d’une majorité de la planète et sont utilisées dans de multiples secteurs et activités, tels que : navigation (cyclisme, transport public, randonnée, ski, ferroviaire), météo, cours d’eau, surveillance, infrastructures énergétiques et de communication, etc.  

La libraire python OSMnx permet de télécharger, modéliser, analyser et visualiser des caractéristiques géographiques et réseaux de routes OSM. La donnée est récupérée en format GeoParquet, une version du modèle de données orientée colonnes Parquet définie spécifiquement pour stocker des données spatiales.  

Ses 387 colonnes contiennent une myriade d’informations allant de XXX à XXX en passant par XXX. Dans notre cas d’étude, les champs relatifs aux catégories suivantes nous seront utiles : 

- TYPES ET SOUS-TYPES
- GEOMETRIE
- HORAIRES 

### 1.2. Identifier les transformations & interactions

Comme vu dans le bloc précédent, la disparité des sources induit le besoin de les transformer afin d’obtenir une base de données harmonisée, prête à l’emploi pour l’application.  

En suivant l’architecture médaillon, les étapes vont comme suit : 

SCHÉMA  

*POIs *  
```
OSM : 	Source ➡️ Bronze ➡️ Silver ↘️
					  Gold
DT : 	Source ➡️ Bronze ➡️ Silver ↗️
```
*ROAD NETWORKS *
```
OSM : 	Source ➡️ Bronze ➡️ Silver ➡️ Gold
```

 | Etape | Action(s) | Format en sortie
 | :-- | :-- | :--
 | **POIs OSM Bronze** | filtre sur la zone considérée (Hérault) | ➡️ CSV & geoparquet
 | **POIs OSM Silver** | filtre sur colonnes pertinentes + création centroïdes  | ➡️ CSV & geoparquet
 | **POIs OSM Gold** |  | 
 | **POIs DT Bronze** | dump puis  | ➡️ list de dict pour chaque entrée
 | **POIs DT Silver** |  | 
 | **POIs DT Gold** |  | 
 | **Road Networks OSM** |  | graphml


étapes de nettoyage à réaliser (normalisation, harmonisation, enrichissement)  
Comment les données interagissent entres elles ? Si on cherche “Musée” (cat. OSM), comment le filtre est enrichi par “Evenement culturels” (cat. DATAtourisme)  
le résultat doit montrer Source > Ingestion > Transformation  
(Nettoyage/Enrichissement) → Stockage (Votre nouvelle base de données) → Consommation (Votre application Web).

## Problématique métier
### 2.1. Constat
manques actuels côté métier => manque d’informations métiers plus précises sur les POIs OSM & géométrie à normaliser, manque de routes pour accéder aux POIs DATAtourisme  

Bien que les 2 sources existent, l'incapacité actuelle à les fusionner dynamiquement signifie que l’user est contraint d’effectuer un travail de modélisation humaine chronophage.  

=> Le problème est qu’en considérant toutes les contraintes existantes, le calcul de l’itinéraire optimisé est impossible.

### 2.2. Analyse des services souhaités
détail des fonctionnalités clefs de l’application  
*Manque actuel > problématique > nécessité d’une nouvelle architecture*

## Synthèse de l’existant (opportunité développement)
### 3.1. Rappel factuel (OSM & DATAtourisme)
### 3.2. Identifier la lacune
### 3.3. Opportunité

**Opportunité** : développement d’une couche de valeur pour combler le fossé identifié  
**Architecture** : orchestrateur de service prenant les DS en y appliquant la logique métier (optimisation itinéraire/respect des contraintes)


