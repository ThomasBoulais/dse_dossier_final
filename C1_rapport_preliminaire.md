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

## Analyse exploratoire des flux de données 👀

### 1.1. Identifier les sources de départ ✅

Notre point de départ est de découvrir et étudier les sources de données à notre disposition. Après une brève description de chacune d’entre elles, nous verrons leur structure de données, identifierons les étapes de transformation nécessaires à leur interopérabilité et présenterons la nouvelle base de données prête à être consommée par l’application cible.  

L'étude des données dans le cas d’itinéraires de voyage concentre notre attention autour de champs issus des familles suivantes :
- **Nom** : le nom du POI ;

- **Localisation** : coordonnées géographiques du POI, direct ou via géométrie ;
- **Catégories** : catégorie du POI (culturel, restauration, etc.) avec sous-catégorie plue détaillée (musée ou lieu historique pour un type culturel par exemple) ;
- **Périodes & horaires d’ouverture** : permet de savoir quand un POI est visitable ou pas ;
- **Informations générales** : contact email et téléphonique,  description & caractéristiques du POI.

#### 1.1.a. DATAtourisme ✅

**DATAtourisme** est une plateforme nationale pour les données d’offres touristiques en territoire français. En agrégeant, normalisant, qualifiant et diffusant en open data les données institutionnelles d’information touristiques, **ses objectifs sont de faciliter l’accès aux données publiques, valoriser l’offre touristique des territoires et favoriser la création de services innovants**.  

La donnée, sous format `JSON-LD`, est récupérable via le site https://diffuseur.datatourisme.fr en associant la création d’un flux (*webservice*) avec la clef API associée à l’application. Sa structure est articulée en **modèle sémantique**: chaque **élément**, **propriété**, **relation** et **contrainte** est stockée de telle sorte que **leur définition soit explicite**, contrairement aux *RDB* où la clef étrangère d’une table n’a de sens qu’avec une interpolation ou explication fonctionnelle de celle-ci.

<center><img src='assets/KnowledgeGraph_DataTOURISME.png' width=1000></center>
<center><i>figure 1: schéma d’un fragment du modèle sémantique DATAtourisme</i></center><br>

Accompagnée de son **ontologie** (https://www.datatourisme.fr/ontology/core) l’exploration de la donnée nous apprend que les POIs (*Points Of Interests*) sont répartis en 4 types de POI (lieu, fête et manifestation, produit, itinéraire touristique), avec un grand nombre de tags métiers présents ou pas selon le type et les sous-types des POIs.  

**Localisation**  
La localisation spatiale, enregistrée dans le champ `isLocatedAt`, peut être exprimée de 2 manières: selon un schéma `geo` avec *longitude/latitude* ou selon un schéma `address` avec la structure complète *adresse/départmement/région/pays*.

**Catégories**  
Chaque POI est catégorisé par une ou plusieurs catégories spécifiques que nous appellerons `sous-types` parmi plus de 180 possibilités pouvant être regroupé par `type` selon leur nature. 

*Par exemple, les tags :* 
- *`Theater` et `Cinema` pourront être des **`sous-types`** associés au **`type`** `leisure & entertainment`,*
- *tandis que `BrasserieOrTavern`, `StreetFood`, `GourmetRestaurant` ou `Bakery` appartiendront plutôt au **`type`** `restauration`*

<br>

**Période & Horaires d'ouverture**  
Pour la gestion des horaires d’activité un schéma structuré existe, on remarque cependant qu’une partie des points de données observés renseigne ces informations dans le tag `additionalInformation` à la place pour renseigner textuellement les horaires.

#### 1.1.b. OSM ✅

**OpenStreetMap** (*OSM*) est une source mise en place par la fondation *OpenStreetMap* dont les données sont issues de **production participative** avant d’être mise à disposition sous licence **ODbL** (*Open Database Licence*, contrat licence favorisant la libre circulation des données). Ces données couvrent les données publiques d’une **majorité de la planète** et sont utilisées dans de multiples secteurs et activités, tels que : **navigation** (cyclisme, transport public, randonnée, ski, ferroviaire), **météo**, **cours d’eau**, **surveillance**, **infrastructures énergétiques et de communication**, etc.  

La libraire python `OSMnx` permet de télécharger, modéliser, analyser et visualiser des caractéristiques géographiques et réseaux de routes OSM. La donnée est récupérée en format `GeoParquet`, une version du modèle de données orientée colonnes Parquet définie spécifiquement pour stocker des données spatiales.  

Ses 405 colonnes contiennent une myriade d’informations dont plus de la moyenne booléennes (206) pour des informations comme `toilets:access`, `drink:espresso`, `payment:cash` ou `ruins`.  

**Localisation**  
La localisation est aussi stockée de 2 manières différentes : 
- via **Géolocalisation** avec un champ contenant soit `POINT()`, `POLYGON()` ou `LINESTRING()` qui représentent différentes géométries (point, polygone et ligne respectivement)
- via **Adresse** avec 12 colonnes qui démarrent par `addr:` comme  `addr:city`, `addr:housenumber`, `addr:postcode`, `addr:street`.

<br>

**Catégories**  
Les catégories sont exprimées par 2 champs ne prennant qu'une valeur unique et exprimant respectivement le type et si le POI possède une utilité pratique : 
- **`tourism`**, 6 possiblités:  `viewpoint`, `attraction`, `museum` `hotel`, `information`, `hostel`
- **`amenity`**, 9 possibilités : `restaurant`, `cafe`, `bar`, `arts_centre`, `place_of_worship`, `fountain`, `planetarium`, `reception_desk`, `animal_boarding`

<br>

**Périodes & horaires d’ouverture**  
Les horaires et périodes d'ouverture sont renseignées dans un champ `opening_hours` suivant la même structure comme indiqué dans l'exemple suivant : `Jul-Aug Tu-Fr 11:00-19:00; Jul-Aug Sa,Su 13:00-19:00; Sep-Jun Tu-Fr 10:00-18:00; Sep-Jun Sa,Su 13:00-18:00`  

**Réseaux de routes**  
En plus des données de POIs, la source OSM possède les informations concernant les **réseaux de routes** (piétons, automobiles) qui serviront à créer l'itinéraire. Ces données sont stockées au format `GraphML` et dont chaque entrée représente un **noeud** (`node`) ou une **arrête** (`edge`).

### 1.2. Identifier les transformations & interactions 👀

Comme vu dans le bloc précédent, les sources présentent de nombreuses similitudes, cependant leurs disparités induisent le besoin de les transformer afin d’obtenir une base de données harmonisée, prête à l’emploi pour l’application.  

En suivant l’architecture médaillon, les étapes sont les suivantes : 

**POIs**  
```
OSM : Source ➡️ Bronze ➡️ Silver ↘️
					  				Gold
DT  : Source ➡️ Bronze ➡️ Silver ↗️
```
**ROAD NETWORKS**
```
OSM : 	Source ➡️ Bronze ➡️ Silver ➡️ Gold
```

 | Type | Etape | Source | Action(s) | Format en sortie
 | :-: | :-- | :-: | :-- | :--
 | **POIs** | **Source**&nbsp; ➡️ &nbsp; **Bronze** | **`OSM`** | *1. requêtage API filtré sur la zone d'étude (Hérault)<br>2. stockage GeoParquet en format brut* | `GeoParquet` <br>+ `CSV` pour contrôle
 | **POIs** | **Source**&nbsp; ➡️ &nbsp; **Bronze** | **`DT`** | *1. requêtage API filtré sur la zone d'étude (Hérault)<br>2. Récupération & extraction du dump<br>3. stockage & extraction du dump en dossier `JSON`*  | 1 `JSON` par entrée <br>+ `JSON` des index
 | **POIs** | **Bronze**&nbsp; ➡️ &nbsp; **Silver** | **`OSM`** | *1. enrichissement/suppression NaNs<br>2. transformation géométries en point centroïdes<br>3. filtre sur colonnes pertinentes* | `GeoParquet` <br>+ `CSV` pour contrôle
 | **POIs** | **Bronze**&nbsp; ➡️ &nbsp; **Silver** | **`DT`** | *1. parsing JSON en GeoParquet<br>2. enrichissement/suppression NaNs<br>3. suppression doublons* | `GeoParquet` <br>+ `CSV` pour contrôle
 | **POIs** | **Silver**&emsp; ➡️ &nbsp; **Gold** | **`OSM`** <br>& <br>**`DT`** | *1. normalisation champs catégories <br>2. création masque horaires <br>3. merge des 2 sources <br>4. détection & suppression doublons* | `GeoParquet` <br>+ `CSV` pour contrôle
 | **Road <br>Networks** | **Source**&nbsp; ➡️ &nbsp; **Bronze** | **`OSM`** | *1. requêtage API sur la zone d'étude (Hérault)<br>2. ajout vitesse & temps de voyage* | `GraphML`
 | **Road <br>Networks** | **Bronze**&nbsp; ➡️ &nbsp; **Silver** | **`OSM`** | *-* | `GraphML`
 | **Road <br>Networks** | **Silver**&emsp; ➡️ &nbsp; **Gold** | **`OSM`** | *création d'un `CSV` liant chaque POI à ses voisins les plus proches* | `GraphML` <br>+ `CSV` pour **Model training**


Plusieurs colonnes ont besoin d'être harmonisées comme 
- les horaires  
- la gestion des catégories, avec plusieurs valeurs cumulables chez `DT` VS choix unique dans 2 colonnes chez `OSM`

étapes de nettoyage à réaliser (normalisation, harmonisation, enrichissement)  

Comment les données interagissent entres elles ? Si on cherche “Musée” (cat. OSM), comment le filtre est enrichi par “Evenement culturels” (cat. DATAtourisme)  

le résultat doit montrer Source > Ingestion > Transformation  
(Nettoyage/Enrichissement) → Stockage (Votre nouvelle base de données) → Consommation (Votre application Web).

## Problématique métier 👀
### 2.1. Constat 👀
manques actuels côté métier => manque d’informations métiers plus précises sur les POIs OSM & géométrie à normaliser, manque de routes pour accéder aux POIs DATAtourisme  

Bien que les 2 sources existent, l'incapacité actuelle à les fusionner dynamiquement signifie que l’user est contraint d’effectuer un travail de modélisation humaine chronophage.  

=> Le problème est qu’en considérant toutes les contraintes existantes, le calcul de l’itinéraire optimisé est impossible.

### 2.2. Analyse des services souhaités 👀
détail des fonctionnalités clefs de l’application  
*Manque actuel > problématique > nécessité d’une nouvelle architecture*

## Synthèse de l’existant (opportunité développement) 👀
### 3.1. Rappel factuel (OSM & DATAtourisme) 👀
### 3.2. Identifier la lacune 👀
### 3.3. Opportunité 👀

**Opportunité** : développement d’une couche de valeur pour combler le fossé identifié  
**Architecture** : orchestrateur de service prenant les DS en y appliquant la logique métier (optimisation itinéraire/respect des contraintes)


