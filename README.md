# TD2 - Qualité developpement - Gestion de dépôts

## 1. Les méthodes de gestion

Définissez au mieux les méthodes de gestion suivantes :
(Aidez-vous du CM2 et des outils de recherche)

- Git Trunk
- Git Flow
  Indiquez les cas d’usage typique de chaque méthode et leurs avantages et inconvénients.

#

### Git trunk :

- Les développeurs travaillent sur une seule branche principale (master).
- Les fonctionnalités sont développées directement sur la branche principale, ou dans des branches courtes avant d'être fusionnées.
- Cela permet de réduire les conflits lors de fusions de branches.
- Les changements sont donc minimes (petite fonctionnalités) et plus faciles à gérer.

> **Avantages**
>
> - Limite les conflits
> - Facile à mettre en place
> - Facilite la collaboration (équipe réduite)

> **Inconvénients**
>
> - Bugs sur la mise en production
> - Il faut des équipes seniors, qui maitrisent leurs sujets
> - Conflit entre développeurs sur un même fichier
> - Pas adapté pour des projets complexes

#

### Git Flow :

- Les fonctionnalités sont développées dans des branches longues, pour chaque cas d'usages.
- La branche principale `master` sont souvent des branches dites "stables", et prêtes à être déployées en production.
- La branche `develop` est la branche de développement, elle contient les fonctionnalités en cours de développement.

> **Avantages**
>
> - Gestion rigoureuse et claire du projet
> - Limite le risque d'erreurs
> - Développer des fonctionnalités en parallèle

> **Inconvénients**
>
> - Plus de branches, une plus grande complexité de gestion
> - Supervision plus accrue avec des juniors
> - Trop de formalité pour des projets trop simples

## 2. Git Trunk

### 1. Définissez le feature-flags (aussi appelé feature-toggles)

Cette fonctionnalité permet d'activer / désactiver des fonctionnalités au lancement à l'exécution, sans modifier le code déployée.

C'est un outil qui permet de cloisonner une fonctionnalitée, dans son environnement exploité.

### 2. Indiquez les moyens usuels d’implémenter du feature-flags

- **Variables d'environnements** : On peut définir des variables d'environnements pour activer ou désactiver des fonctionnalités.
- **Fichiers de configurations** : On peut définir des fichiers JSON, YAML ou XML de configurations pour activer ou désactiver des fonctionnalités.
- **Services externes** : On peut utiliser des services externes pour activer ou désactiver des fonctionnalités, qui permettant de gérer les Feature Flags.
- **Gestionnaire de ressources** : Système de gestion de ressources et de cache pour activer ou désactiver des fonctionnalités (Redis).

### 3. Décrire le flux de travail du Trunk-Based Repository

Le flux de travail d’un Trunk-Based Repository repose sur l’idée d’une intégration continue des modifications dans une seule branche principale, appelée souvent `trunk` ou `main`. Ce workflow favorise des livraisons rapides, des cycles courts, et une réduction des conflits.

La création de branche est possible, mais ce sont souvent des branches dites "courtes", pour des fonctionnalités simples.

Pour la validation du code, on utilise des vérifications de build, de compilations, des tests unitaires, des tests d'intégrations, et des tests de non-régression. On peut aussi faire travailler des développeurs en pair-programming, afin qu'ils se valident entres-eux.

Pour la release, on créer une branche longue `release`, qui permet de préparer la mise en production.

## 3. Git flow

### 1. Décrire le flux de travail du Git Flow

Le flux de travail Git Flow repose sur deux branches principales, `master` pour le code stable et publié, c'est une branche qui est une base commune pour tous les développeurs.

`develop` pour le développement actif.

Les développeurs créent des branches temporaires pour des tâches spécifiques : les branches `feature/*` sont utilisées pour développer de nouvelles fonctionnalités et sont fusionnées dans develop une fois terminées, après reviews des développeurs.

Lorsque les fonctionnalités sont prêtes pour une nouvelle version, une branche `release/*` est créée depuis develop pour effectuer les ajustements finaux avant d’être fusionnée dans `master` et `develop`.

En cas de bug critique en production, une branche `hotfix/*` est créée depuis `master`, corrigée rapidement, puis fusionnée dans `master` et `develop`.

Ce flux de travail permet une gestion structurée des versions et des correctifs tout en maintenant la stabilité du code en production.

### 2. Décrire la méthode préférée pour gérer plusieurs versions majeures/mineures en parallèle

La méthode préférée pour gérer plusieurs versions majeures et mineures en parallèle est d'utiliser des branches de support dédiées, souvent appelées branches de maintenance ou branches versionnées. On peut les tirer des branches `release/*` ou `tag/*`.

Ce modèle permet de maintenir, corriger, et publier des mises à jour spécifiques pour différentes versions tout en continuant le développement actif sur la branche principale.

## 4. Noms de branche (GitFlow)

Donnez les noms de branches correspondant aux situations suivantes :

- Une fonctionnalité « Gestion des utilisateurs – suppression » (ticket n°B-768) :

`feature/B-768-user-management`

- Un fix « Mauvaise redirection après ajout d’un email à l’utilisateur » (ticket A-46) :

`fix/A-46-bad-redirection-after-user-email`

- L’ajout d’une configuration « devcontainer » pour l’environnement de développement :

`develop`

> Tagger le commit associé avec un tag `chore/devcontainer`

- Un hotfix pour préparer un patch depuis une version 1.3.1 :

`hotfix/1.3.2` ou `hotfix/1.3.1-hotfix-1`

- Une release mineure après 1.4.17 :

`release/1.4.18` ou `release/1.5.0`

- Une branche support après release 12.5.6 :

`support/12.5.X`

## 5. Commit messages

Indiquez les informations importantes qu’un message de commit devrait indiquer d’un coup d’œil (obligatoires et souhaitées).
Voici plusieurs messages de commit :

    feat[B-658]: side-menu statistics page link

    - adding a side menu item
    - adding a static link to the stats page
    ~ making various minor fixes on CSS
    Co-author : Kamel Debbiche
    Refs: https://doc.myapp.acompany.net/gui-rules/
    docs[A-245]: C4 modeling – books micro-service
    - init structurizr file (..books.service.structurizr)

    * removing outdated ADL and documentation
    chore!: drop support of PHP 7
    BREAKING CHANGE: use PHP features not available in PHP 7
    feat: add French language support with i18n

- Identifier les éléments un à un et déterminer leur caractère obligatoire ou optionnel. Enfin, déterminez une structure générale applicable à cet ensemble.

> - Le nom du commit est obligatoire.
> - Le type du commit est obligatoire.
> - Le numéro de ticket est optionnel.
> - La description du commit est optionnelle.
> - Les modifications apportées sont optionnelles.
> - Les co-auteurs sont optionnels.
> - Les références sont optionnelles.
> - Les notes de versions sont optionnelles.

- Lister les types de commit possibles et décrire leur utilisation

> - **feat/** : Ajout d'une nouvelle fonctionnalité
> - **fix/** : Correction d'un bug
> - **docs/** : Modification de la documentation
> - **chore/** : Petites modifications, petites tâches (corvées)
> - **release/** : Publication d'une nouvelle version
> - **ci/** : Modifications des fichiers de configuration CI
> - **style/** : Formattage du code
> - **refactor/** : Refactoring du code
> - **perf/** : Amélioration des performances
> - **test/** : Ajout de tests

- Qu’est qu’un breaking-change ?

Une modification qui casse la compatibilité avec les versions précédentes, et qui nécessite une mise à jour des utilisateurs.

> Un changement qui n'est pas rétro-compatible.

> Il doit toujours être documentée, donnée lieu à une version majeure, et être définie dans une matrice de compatibilité.

## 6. Semantic versioning

REF : https://semver.org/lang/fr/

Décrire en français les numéros de version suivants et déduire :

- **1.1.0** : Version majeure 1, version mineure 1, version correctif 0.

  > - Majeure suivante **(2.0.0)**
  > - Pre-majeure suivante **(2.0.0-0)**
  > - Mineure suivante **(1.2.0)**
  > - Pre-mineure suivante **(1.2.0-0)**
  > - Patch suivant **(1.1.1)**
  > - Pre-patch suivant **(1.1.1-0)**
  > - Pre-release suivante **(1.1.1-0)**

- **1.0.0-RC.2** : Version de pré-lancement, majeure 1, mineure 0, correctif 0, deuxième release candidate.

  > - Majeure suivante **(1.0.0)**
  > - Pre-majeure suivante **(2.0.0-0)**
  > - Mineure suivante **(1.0.0)**
  > - Pre-mineure suivante **(1.1.0-0)**
  > - Patch suivant **(1.0.0)**
  > - Pre-patch suivant **(1.0.1-0)**
  > - Pre-release suivante **(1.0.0-RC.3)**

- **1.0.0-snapshot+build.9cbd45f6** : Majeur 1, mineur 0, correctif 0, version snapshot avec un build.

  > - Majeure suivante **(1.0.0)**
  > - Pre-majeure suivante **(2.0.0-0)**
  > - Mineure suivante **(1.0.0)**
  > - Pre-mineure suivante **(1.1.0-0)**
  > - Patch suivant **(1.0.0)**
  > - Pre-patch suivant **(1.0.1-0)**
  > - Pre-release suivante **(1.0.0-snapshot-0)**

- **3.0.0-beta.1** : 3eme version majeure, première version beta.

- **2.3.1+nightly.230524.0114** : Version mineure, avec un build nightly.
