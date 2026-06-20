# Recommandations et axes de développement - Itinéraire de voyage

## 1) Problématique métier et attentes utilisateurs
L’enjeu métier est de réduire le “coût cognitif” et le temps de planification, tout en améliorant la qualité du voyage : un itinéraire doit être **réaliste**, **cohérent** avec des **contraintes** (temps, rythmes, options/obligations, préférences), et suffisamment **robuste** pour gérer les imprévus (météo, fermeture, retards).  
Les solutions existantes couvertes par la veille montrent surtout une forte valeur sur la **logistique** (organisation, collaboration, budget, documents, offline), mais moins sur la partie **optimisation multi-critère** et l’**arbitrage** (et donc l’adaptation / plan B).

## 2) Axes de développement recommandés (avec argumentaire)

### Axe A — Moteur de génération d’itinéraires “multi-critère” orienté contraintes
**Recommandation :** concevoir un moteur qui génère un itinéraire en tenant compte simultanément de plusieurs dimensions, par exemple :
- horaire / plages de visite,
- temps de trajet (et marges),
- fatigue / rythmes (durées max par journée, temps de repos),
- contraintes optionnelles vs obligatoires,
- préférences (lieux, activités, styles de route/transport),
- faisabilité (éviter les combinaisons impossibles ou trop serrées).

**Argumentaire :**
- C’est l’écart principal identifié par la veille : les apps analysées proposent davantage de planification assistée ou de recalcul simple, mais rarement un solveur robuste qui arbitre explicitement.
- Multi-critère = meilleure adéquation à la réalité utilisateur (un seul “meilleur chemin” ne suffit pas).

### Axe B — Arbitrage explicite et justification des choix (aide à la décision)
**Recommandation :**
- afficher un “raisonnement utilisateur” : pourquoi cette option est choisie (ex. “préserve le respect du temps de visite”, “évite une marche trop longue”, “priorise les obligations”),
- et proposer une lecture claire des compromis (ex. temps vs confort vs coût).

**Argumentaire :**
- L’aide à l’arbitrage devient un facteur différenciant : l’utilisateur n’a pas seulement un résultat, il comprend et peut ajuster.
- Cela améliore l’acceptation du système : moins de “boîte noire”, plus de contrôle.

### Axe C — Robustesse : option B et adaptation guidée en cas d’imprévu
**Recommandation :**
- intégrer un mécanisme de **plan B** : lorsqu’un événement invalide une partie du programme (retard, fermeture, météo), le système propose :
  - une replanification “minimale” (préserver le maximum déjà acquis),
  - une alternative justifiée (ce qui change et pourquoi),
  - et un indicateur de risque (impact sur fatigue/temps/budget).
- prévoir des scénarios d’imprévu dans le modèle de données (cause, périmètre impacté, degré d’urgence).

**Argumentaire :**
- La veille met en évidence une absence fréquente de plan B robuste.
- La valeur métier est directe : moins d’échecs de planification et plus de satisfaction.

### Axe D — “Trip package” : intégrer logistique + optimisation (end-to-end)
**Recommandation :**
conserver les briques fortes observées tout en les connectant à l’optimisation :
- budget et catégories dépenses,
- documents de réservation,
- checklists/inventaires,
- offline-first,
- collaboration et partage du planning,
- ajout de POIs et intégration “on the flow”.

**Argumentaire :**
- Une génération d’itinéraires utile doit se traduire en exécution : réservations, suivi, contenus offline.
- Le moteur d’optimisation devient la “cerise” au sommet d’une expérience voyage complète.

### Axe E — Accessibilité et RSE dès la conception (qualité produit et conformité)
**Recommandation :**
- RGAA : formulaires et parcours accessibles, lecture claire des itinéraires, compatibilité technologies d’assistance.
- RSE/écologie : réduire les replanifications inutiles, proposer des variantes cohérentes (modes/rythmes) pour limiter l’inefficacité.
- Inclusion : permettre d’exprimer des contraintes de mobilité (ex. fatigue, accessibilité quand l’info existe) et proposer des alternatives adaptées.

**Argumentaire :**
- Ces exigences ne sont pas seulement “conformité” : elles améliorent la pertinence fonctionnelle pour des profils variés et donc la valeur utilisateur.

## 3) Plan d’action (version pragmatique)
1. **MVP optimisation** : générer un itinéraire multi-critère pour un périmètre limité (ex. 2–3 jours, nombre de POIs borné), avec :
   - contraintes optionnel/obligatoire,
   - explication simple des compromis,
   - marges de faisabilité.
2. **MVP arbitrage UI** : permettre des ajustements rapides (pondérations/contraintes) + affichage “pourquoi”.
3. **Plan B v1** : replanification minimale sur un événement unique (retard ou fermeture d’un POI).
4. **Connecteurs logistiques** : budget/documents/checklist offline ; intégration POIs.
5. **Améliorations RSE/RGAA** : audit accessibilité + contraintes d’inclusion.

## 4) Synthèse des recommandations (message à retenir)
- Priorité 1 : **génération d’itinéraires multi-critère** avec gestion réaliste des contraintes.
- Priorité 2 : **arbitrage explicite** pour que l’utilisateur comprenne et ajuste.
- Priorité 3 : **robustesse avec plan B** afin d’éviter la casse du voyage en cas d’imprévu.
- En parallèle : s’appuyer sur les points forts de la veille (logistique, collaboration, offline, POIs, budget) pour assurer une expérience “end-to-end”.
- Enfin : intégrer **RGAA** (accessibilité) et **RSE** (écologie + inclusion handicap) comme paramètres de conception.

## 5) Vocabulaire et prise de parole (script court, 45–60 secondes)
“Notre veille montre que beaucoup d’applications aident surtout à organiser la logistique du voyage : collaboration, budget, documents, offline, et parfois le recalcul autour de POIs. La différenciation à construire, c’est la génération d’itinéraires réellement optimisés : un moteur multi-critère qui respecte des contraintes optionnelles et obligatoires, avec un arbitrage explicable pour éviter l’effet boîte noire. Ensuite, je recommande d’ajouter une robustesse avec plan B, pour adapter l’itinéraire en cas d’imprévu tout en minimisant l’impact sur ce qui a déjà été validé. Enfin, on connecte ce moteur au trip end-to-end et on garantit l’accessibilité RGAA et les enjeux RSE dès la conception : inclusion et réduction des replanifications inutiles.”