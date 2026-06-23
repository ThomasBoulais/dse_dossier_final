# **Plan d'accompagnement - Itinéraire de voyage**

## **1. Stratégie d'accompagnement**

### **1.1 Principes généraux**

Le plan d'accompagnement adopte une approche **légère et efficiente** :

- **UX intuitive** : Streamlit offre une interface épurée, minimisant la courbe d'apprentissage.
- **Documentation minimaliste** : Avantage = rapidité onboarding ; risque = questions « basiques » au support.
- **Démonstration vidéo** : Cœur du dispositif d'onboarding, couvrant les scénarios clés pour les 2 personas.
- **Support tiered** : Trois niveaux d'utilisateurs (finaux, administrateurs, développeurs) avec besoins différents.

### **1.2 Publics cibles et besoins**

| **Public** | **Profil** | **Besoin prioritaire** | **Livrables** |
|:---|:---|:---|:---|
| **Utilisateurs finaux** | Planificatrices pragmatiques & explorateurs flexibles | Comprendre comment générer un itinéraire en 5 min | Vidéo démo (2-3 min) + FAQ quick start |
| **Administrateurs de données** | Équipe maintenance POIs / données DATAtourisme | Mettre à jour/enrichir données POIs, monitorer qualité | Guide administrateur + runbook maintenance |
| **Développeurs (futur)** | Équipes extension/maintenance code | Comprendre architecture, fork/modifier modèle RL | Documentation technique + API docs (OpenAPI auto) |
| **Décideurs / Jury** | Évaluateurs projet académique | Valider approche, résultats, viabilité | Rapport formel (C19/C20/C23) + démo vidéo |

## **2. Matériaux d'accompagnement**

### **2.1 Livrables pédagogiques**

| **Matériel** | **Format** | **Durée / Taille** | **Public** | **Contenu clé** |
|:---|:---:|:---:|:---|:---|
| **Vidéo démo (Planificatrice)** | MP4 (1080p, sous-titres FR) | 2-3 min | Utilisateurs finaux | Saisie profil → Générer itinéraire → Visualisation carte/timeline → Exporter PDF |
| **Vidéo démo (Explorateur)** | MP4 (1080p, sous-titres FR) | 2-3 min | Utilisateurs finaux | Saisie préférences personnalisées → Obtenir scénarii alternatifs → Ajuster critères |
| **FAQ Quick Start** | Markdown (GitHub) + PDF | 2-3 pages | Utilisateurs finaux | Q: "Où rentrer ma destination ?" ; "Combien de jours ?" ; "Puis-je modifier itinéraire ?" ; "Format export ?" |
| **Guide Administrateur** | Markdown + Jupyter Notebook | 5-7 pages + script | Administrateurs données | Refresh DATAtourisme API → Validation POIs → Détection doublons/orphelins → QA metrics |
| **Documentation API** | OpenAPI/Swagger (auto-généré FastAPI) | HTML interactif | Développeurs | Endpoints, schémas request/response, exemples cURL |
| **Guide Architecture** | Markdown + diagrammes | 8-10 pages | Développeurs | Data flow, schéma DB, architecture RL, décisions design |
| **Vidéo démo (Technique)** | MP4 (optionnel) | 5-10 min | Développeurs + jury | Architecture système → Démarrer services localement → Appel API → Interprétation réponse |


**[WIP] : à suivre**