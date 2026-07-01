# stellarstack-templates

Templates applicatifs one-click de StellarStack (WordPress, Nextcloud, Gitea, Ghost, Grafana, Uptime Kuma, etc.).

> **Dépôt public.** Il constitue à terme le socle du catalogue de templates et de la marketplace communautaire. Aucune donnée sensible ou spécifique à un client ne doit y figurer.
>
> **Statut : temporaire sur GitHub**, le temps que `git.stellarstack.fr` (GitLab CE) soit opérationnel. Voir [Migration](#migration-vers-gitlab-ce).

## Objet

Ce dépôt contient les définitions des applications déployables en un clic depuis le catalogue StellarStack — la bibliothèque qui permet à un utilisateur d'obtenir une application fonctionnelle en quelques minutes, sans configuration manuelle.

## Lien avec le cahier des charges

- **SF-6** : Templates applicatifs (one-click apps) — catalogue, déploiement en un clic, paramétrage optionnel, mise à jour assistée.
- **SF-12** : Marketplace de templates — ce dépôt est le socle technique sur lequel s'appuiera, à terme, la publication communautaire de templates (SF-12.1).

Cas d'usage de référence (cf. CDC) : une agence web déploie dix sites clients depuis un template, sans configurer manuellement dix serveurs web et leurs certificats SSL.

## Structure du dépôt

```
stellarstack-templates/
├── wordpress/
│   ├── template.yaml       # Définition du template (métadonnées, paramètres, ressources)
│   ├── docker-compose.yml  # ou manifests Helm/K8s selon l'architecture retenue
│   └── README.md           # Description spécifique du template
├── nextcloud/
├── gitea/
├── ghost/
├── grafana/
├── uptime-kuma/
├── _template-model/         # Gabarit à copier pour créer un nouveau template
└── README.md
```

*Chaque application dispose de son propre sous-dossier, avec la même structure interne, pour rester prévisible et facile à parcourir.*

## Comment ajouter un nouveau template

1. Copier `_template-model/` vers un nouveau dossier nommé d'après l'application (kebab-case).
2. Renseigner `template.yaml` : nom, description, catégorie, ressources minimales recommandées, paramètres exposés à l'utilisateur (nom de domaine, identifiants, dimensionnement...).
3. Fournir la définition de déploiement (Docker Compose, Helm chart ou manifest K8s, selon ce qu'attend le moteur de déploiement de `stellarstack-platform`).
4. Documenter le template dans son propre `README.md` (à quoi sert l'appli, config par défaut, limitations connues).
5. Tester le déploiement en environnement de recette avant toute ouverture au catalogue de production.
6. Ouvrir une Pull Request — chaque nouveau template est revu avant intégration (cf. SF-12.2, validation et modération avant mise à disposition).

## Conventions

- **Un dossier = une application**, nommage en kebab-case.
- **Config par défaut fonctionnelle immédiatement** (SF-6.2) : un template doit être utilisable sans paramétrage obligatoire, avec des valeurs par défaut raisonnables.
- **Pas de secrets codés en dur** : tout identifiant généré à la volée par le moteur de déploiement, jamais une valeur fixe dans le template.
- **Provenance vérifiée** : toute image ou dépendance externe utilisée par un template doit provenir d'une source de confiance (cohérent avec ST-5.5, contrôle de provenance des images).

## Migration vers GitLab CE

Même trajectoire que les autres dépôts, avec la même vigilance qu'`stellarstack-docs` étant donné son caractère public : bascule vers `git.stellarstack.fr` prévue dès que l'instance GitLab CE est opérationnelle, avec arbitrage sur le maintien ou non d'un miroir public.

## Mise à jour de ce document

Document vivant : toute nouvelle catégorie de templates ou changement de convention de structure doit être répercuté ici.

---
*StellarStack — Cloud PaaS/SaaS Simple, Transparent, Souverain*
