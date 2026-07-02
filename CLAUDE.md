# stellarstack-templates — Contexte dépôt

> Templates applicatifs one-click de StellarStack. Complète le `CLAUDE.md` racine du workspace.
> **Dépôt PUBLIC.** Aucune donnée sensible, aucun secret, rien de spécifique à un client. Socle du futur catalogue et de la marketplace communautaire.

## Rôle

Définitions des applications déployables en un clic depuis le catalogue : WordPress, Nextcloud, Gitea, Ghost, Grafana, Uptime Kuma, etc. But — une app fonctionnelle en quelques minutes, sans configuration manuelle.

Couverture CDC : **SF-6** (templates one-click : catalogue, déploiement, paramétrage optionnel, mise à jour assistée), **SF-12** (marketplace : ce dépôt est le socle de la publication communautaire, SF-12.1). Cas de référence : une agence web déploie dix sites clients depuis un template sans configurer dix serveurs et leurs certificats.

## Structure cible

Un dossier par application (kebab-case), même structure interne pour rester prévisible :

```
<app>/
├── template.yaml       # métadonnées, catégorie, ressources mini, paramètres exposés
├── docker-compose.yml  # ou chart Helm / manifest K8s selon le moteur de déploiement de platform
└── README.md           # description, config par défaut, limitations connues
_template-model/        # gabarit à copier pour un nouveau template
```

## Ajouter un template

1. Copier `_template-model/` vers `<nouvelle-app>/` (kebab-case).
2. Renseigner `template.yaml` (nom, description, catégorie, ressources mini, paramètres utilisateur : domaine, identifiants, dimensionnement…).
3. Fournir la définition de déploiement attendue par le moteur de `stellarstack-platform`.
4. Documenter dans le `README.md` du template.
5. Tester en recette avant toute ouverture au catalogue de production.
6. Ouvrir une PR — chaque template est revu avant intégration (SF-12.2, modération).

## Conventions

- **Workflow git/Jira** : boucle standard du `CLAUDE.md` racine (section « Workflow git & Jira ») — travail sur `feature|fix/SS-<num>-<slug>` créées via `/nouvelle-branche` depuis `dev`, jamais de commit direct sur `main`/`dev`, synchro Jira via `/point-avancement`.
- **Un dossier = une application**, kebab-case.
- **Config par défaut fonctionnelle immédiatement** (SF-6.2) : utilisable sans paramétrage obligatoire, valeurs par défaut raisonnables.
- **Aucun secret en dur** : tout identifiant généré à la volée par le moteur de déploiement, jamais une valeur fixe.
- **Provenance vérifiée** (ST-5.5) : images et dépendances externes issues de sources de confiance uniquement.
- Toute nouvelle catégorie ou changement de convention de structure → répercuté dans le README.

## Découpage / interfaces

- La définition de déploiement doit correspondre à ce qu'attend le moteur de déploiement de `stellarstack-platform`.
- Dépôt public : appliquer le test « serais-je à l'aise si un concurrent lisait ça ? » avant tout commit.