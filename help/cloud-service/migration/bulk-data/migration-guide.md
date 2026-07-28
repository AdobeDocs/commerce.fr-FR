---
title: Exécution d’une migration de données en bloc
description: Découvrez comment configurer et exécuter une migration de données en bloc d’une instance Adobe Commerce PaaS ou locale vers Adobe Commerce as a Cloud Service avec l’interface de ligne de commande.
feature: Cloud
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:19:07.600Z'
TQID: 'https://experienceleague.adobe.com/z9659Vnf2JLxJ4U5p3tEEjurj5Mg3bfKj68Gheq2AXY'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 670b6214b28be93a16130552a226a8cadb487324
workflow-type: tm+mt
source-wordcount: 2802
ht-degree: 0%

---

# Exécuter une migration de données en bloc

{{bulk-data-early-access}}

Ce guide est une référence opérationnelle détaillée pour l’exécution d’une migration des données à partir d’une installation PaaS [!DNL Adobe Commerce] ou locale vers [!DNL Adobe Commerce as a Cloud Service] à l’aide de l’outil de migration de données en bloc. Les valeurs de configuration réelles et les détails spécifiques à l’environnement varient en fonction de votre configuration.

Avant de commencer, confirmez que vous avez terminé chaque élément de la [liste de contrôle de préparation du client](readiness-checklist.md) et vérifié l’accès à l’API avec le [guide d’accès au service de migration](cdms-access.md).

>[!NOTE]
>
>Une documentation technique complète couvrant l’architecture de l’outil, la conception interne, la structure de transformation des données et la structure de test d’intégrité est fournie dans le cadre du package de distribution d’outils.

## Conditions préalables

- **[!DNL Docker]** et **[!DNL Docker Compose]** doivent être installés sur la machine sur laquelle vous exécutez la migration.
- L’utilisateur exécutant la migration doit être autorisé à exécuter les commandes `docker` et `docker compose` (ou les `docker-compose` hérités). Le [!DNL Linux], l’utilisateur ou l’utilisatrice doit faire partie du groupe `docker`. Sur [!DNL macOS] et [!DNL Windows], les [!DNL Docker Desktop] doivent être en cours d’exécution et accessibles. L’interface de ligne de commande de migration appelle [!DNL Docker] à plusieurs reprises et les erreurs d’autorisation ici bloquent l’exécution.
- La configuration principale doit être cohérente entre la source et la cible avant d’exécuter la migration. Les données de configuration de base, telles que les paramètres de magasin et la configuration du système, ne sont pas migrées par cet outil. Configurez-le indépendamment sur la cible et alignez-le sur la source avant la migration.

## Configurer le package d’outils

Configurez l’environnement pour la migration de données en bloc :

>[!VIDEO](https://video.tv.adobe.com/v/3496121)

1. Extrayez le contenu du `ccsaas-migration-tools.tar.gz`.

1. Exécutez toutes les commandes à partir du dossier `ccsaas-migration-tools` extrait, où réside `bin/console`.

1. Assurez-vous que le dossier est accessible en écriture pour les journaux, le cache, les [!DNL Composer] et les fichiers générés.

   Modifiez la propriété de tous les fichiers et sous-dossiers de ce répertoire sur l’utilisateur du système d’exploitation qui exécute la migration, de sorte que l’outil puisse lire et écrire de manière cohérente. Par exemple, sur [!DNL Linux] : `chown -R <user>:<group> <project-root>`.

1. Créez les fichiers `.env` et `.my.cnf` à la racine du projet en copiant les fichiers d’exemple (`.example.env` à `.env` et `.my.cnf.example` à `.my.cnf`), puis renseignez les valeurs décrites dans les sections suivantes.

### Exemples de fichiers de configuration

Les fichiers `.example.env` et `.my.cnf.example` de la racine du référentiel constituent le point de départ de votre configuration. Copiez chaque fichier dans son nom de travail et renseignez les valeurs requises.

| Exemple de fichier | Copier vers | Ce qu’il couvre |
| --- | --- | --- |
| `.example.env` | `.env` | Liste annotée de toutes les variables d’environnement prises en charge : performances, CDMS, IMS, SaaS cible, authentification des URL sources, OAuth et valeurs PaaS facultatives (`MAGENTO_CLOUD_CLI_TOKEN` lorsque `id=` est défini dans `.my.cnf`). La liste complète des variables est disponible dans le fichier `.env`. |
| `.my.cnf.example` | `.my.cnf` | Référencez `[section]` dispositions pour les [!DNL MySQL] sur site et PaaS (`id=project:environment`). Le nom du `[section]` doit correspondre à `SOURCE_CONNECTION_NAME` dans `.env`. Les champs incluent `user`, `password`, `host`, `port`, `database` et `id=` pour PaaS. |

## Configuration du fichier d’environnement

Le fichier `.env` dans la racine du projet est la configuration de migration et d’extraction. Il pilote le pipeline de l’interface de ligne de commande, y compris les URL source et cible, OAuth, la connexion CDMS distante, l’authentification SaaS et IMS et d’autres commutateurs.

>[!NOTE]
>
>N’incluez pas de barres obliques de fin dans les URL. Par exemple, utilisez `https://example.com` au lieu de `https://example.com/`.

Modifiez le fichier `.env` et définissez correctement au moins les valeurs suivantes. Pour obtenir la liste complète des variables prises en charge, reportez-vous aux annotations intégrées dans `.example.env`.

```shell-session
SOURCE_INSTANCE_URL=https://<source-host>
SOURCE_INSTANCE_GRAPHQL_URL=https://<source-host>/graphql
SOURCE_INSTANCE_REST_URL=https://<source-host>/rest
SOURCE_INSTANCE_CONSUMER_KEY=<consumer_key>
SOURCE_INSTANCE_CONSUMER_SECRET=<consumer_secret>
SOURCE_INSTANCE_ACCESS_TOKEN=<access_token>
SOURCE_INSTANCE_ACCESS_TOKEN_SECRET=<access_token_secret>
```

### Configuration des informations d’identification OAuth source

>[!VIDEO](https://video.tv.adobe.com/v/3496142)

Ces quatre valeurs signent les requêtes de l’outil de migration vers les API du magasin source. Pour les obtenir, ouvrez le [!UICONTROL Admin] source et accédez à [!UICONTROL **Système**] > [!UICONTROL **Extensions**] > [!UICONTROL **Intégrations**]. Créez ou ouvrez une intégration, puis copiez les valeurs dans `.env` :

```shell-session
SOURCE_INSTANCE_CONSUMER_KEY=<consumer_key>
SOURCE_INSTANCE_CONSUMER_SECRET=<consumer_secret>
SOURCE_INSTANCE_ACCESS_TOKEN=<access_token>
SOURCE_INSTANCE_ACCESS_TOKEN_SECRET=<access_token_secret>
```

### Définition du jeton d’interface de ligne de commande Cloud

>[!NOTE]
>
>Cela s’applique uniquement aux instances sources [!DNL Adobe Commerce on Cloud]. L’outil détecte automatiquement le type de source à partir de `.my.cnf`. Si la section `SOURCE_CONNECTION_NAME` contient une ligne de `id=` (par exemple, `id=project:production`), la source est [!DNL Adobe Commerce on Cloud] et `MAGENTO_CLOUD_CLI_TOKEN` est obligatoire. Pour les sources locales sans `id=`, ce jeton n’est pas nécessaire et la configuration du tunnel est ignorée.

1. Accédez à `https://accounts.magento.cloud` et connectez-vous.

1. Cliquez sur l’image de votre profil, puis sélectionnez [!UICONTROL **Paramètres du compte**].

1. Accédez à la section [!UICONTROL **Jetons API**].

1. Sélectionnez [!UICONTROL **Créer un jeton API**], donnez-lui un nom explicite et copiez le jeton généré.

1. Définissez le jeton dans `.env` :

   ```text
   MAGENTO_CLOUD_CLI_TOKEN=<your_magento_cloud_api_token>
   ```

>[!NOTE]
>
>Si c’est la première fois que vous utilisez l’interface de ligne de commande Cloud, vous devez également ajouter votre clé publique SSH à votre compte . Pour obtenir des instructions, consultez le [Guide de connexions sécurisées](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections).

### Aligner les paramètres d’administration Commerce

Avant la migration, assurez-vous que les paramètres suivants sont cohérents entre la source et la cible.

>[!NOTE]
>
>Pour garantir une migration fluide, [!DNL Adobe] vous recommande de rendre toutes les configurations de base dans l’instance cible cohérentes avec la source.

### Configuration des identifiants SaaS et IMS cibles

>[!VIDEO](https://video.tv.adobe.com/v/3496167)

Il s’agit des paramètres IMS et API [!DNL Adobe Commerce as a Cloud Service] pour la cible. Vous avez besoin de l’identifiant du client, de l’identifiant de l’organisation, des informations d’identification de serveur à serveur OAuth IMS et de l’hôte IMS approprié pour votre environnement. Assurez la coordination avec votre équipe Adobe pour l’accès à l’organisation, au client et au profil. N’essayez pas de déduire ou d’estimer des valeurs sensibles.

#### Générer les informations d’identification IMS

Utiliser le [&#128279;](https://developer.adobe.com/console/). Vous avez besoin d’un accès [!UICONTROL Developer] ou [!UICONTROL Admin] à l’organisation Adobe pour créer des projets. Une connexion utilisateur de base ne suffit pas pour ajouter des API.

1. Créez un projet ou ouvrez-en un existant, puis sélectionnez [!UICONTROL Add API].

1. Choisissez [!UICONTROL **Adobe Commerce as a Cloud Service**] et continuez.

1. Sélectionnez [!UICONTROL **OAuth de serveur à serveur**] comme type d’authentification et continuez.

1. Sélectionnez le profil de produit attendu par votre équipe Adobe pour ce client, puis sélectionnez [!UICONTROL **Enregistrer l’API configurée**].

1. Dans la barre latérale du projet, ouvrez [!UICONTROL **OAuth de serveur à serveur**] (ou [!UICONTROL **Informations d’identification**]), puis copiez l’identifiant client et le secret client dans `.env` en tant que `ADOBE_IMS_CLIENT_ID` et `ADOBE_IMS_CLIENT_SECRET`.

Le point d’entrée du jeton IMS (`ADOBE_IMS_URL`) doit correspondre à l’environnement des informations d’identification.

| Niveau | `ADOBE_IMS_URL` standard |
| --- | --- |
| Contrôle qualité ou évaluation | `https://ims-na1-stg1.adobelogin.com` |
| Pré-production ou production | `https://ims-na1.adobelogin.com` |

>[!NOTE]
>
>`na1` dans ces URL représente la région dans laquelle votre instance cible est configurée. Remplacez-la par l’identifiant de région approprié si votre instance est configurée dans une autre région.

`ADOBE_IMS_META_SCOPES` doit correspondre aux étendues configurées sur ces informations d’identification. Le fichier `.example.env` inclut la chaîne de portée complète séparée par des virgules comme référence. Modifiez-la uniquement si Adobe vous le demande.

#### Mapper les informations d’identification [!DNL Adobe I/O] au fichier d’environnement

Dans [!DNL Developer Console], les valeurs de serveur à serveur OAuth sont présentées sous la forme d’un identifiant client et d’un secret client, correspondant à la structure JSON suivante :

```json
{
  "client_id": "xxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "client_secret": "xxxxxxxxxxxxxxxxxxxxxxxxxxx"
}
```

Mappez-les dans des `.env` (exemples d’espaces réservés) :

```shell-session
TARGET_ORG_ID=<org_id>@AdobeOrg
ADOBE_IMS_URL=https://ims-na1.adobelogin.com
ADOBE_IMS_CLIENT_ID=xxxxxxxxxxxxxxxxxxxxxxxxxxx
ADOBE_IMS_CLIENT_SECRET=xxxxxxxxxxxxxxxxxxxxxxxxxxx
ADOBE_IMS_META_SCOPES=AdobeID,openid,additional_info.projectedProductContext
```

Les hôtes de l’API SaaS diffèrent entre la pré-production et la production. `TARGET_INSTANCE_REST_URL` et `TARGET_INSTANCE_GRAPHQL_URL` doivent utiliser le même environnement d’API Commerce que votre migration, que ce soit en préproduction ou en production. Ne mélangez pas un niveau avec le système de gestion de la relation client (CDMS) ou le client de l’autre niveau.

| Environnement | Hôte type en `TARGET_INSTANCE_*_URL` |
| --- | --- |
| Pré-production ou sandbox | `https://na1-sandbox.api.commerce.adobe.com/{tenantId}` |
| Production | `https://na1.api.commerce.adobe.com/{tenantId}` |

>[!NOTE]
>
>`na1` dans ces URL représente la région dans laquelle votre instance cible est configurée. Remplacez-la par l’identifiant de région approprié si votre instance est configurée dans une autre région.

```shell-session
TARGET_TENANT_ID=<tenant_id>
TARGET_ORG_ID=<org_id>@AdobeOrg
ADOBE_IMS_URL=https://ims-na1.adobelogin.com
ADOBE_IMS_CLIENT_ID=<client_id>
ADOBE_IMS_CLIENT_SECRET=<client_secret>
ADOBE_IMS_META_SCOPES=AdobeID,openid,additional_info.projectedProductContext
TARGET_INSTANCE_REST_URL=https://na1-sandbox.api.commerce.adobe.com/{tenantId}
TARGET_INSTANCE_GRAPHQL_URL=https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql
```

Pour les hôtes SaaS de production, remplacez `na1-sandbox` par `na1` dans les deux URL `TARGET_INSTANCE_*`. Utilisez les `ADOBE_IMS_URL` correspondantes pour ce niveau, comme indiqué dans le tableau précédent.

### Définir le point d’entrée CDMS

Pointez l’outil de migration sur l’hôte de l’API CDMS correspondant à l’environnement vers lequel vous migrez. Définissez `CDMS_HOST` (et généralement `CDMS_PORT=443`) dans `.env`. Utilisez un hôte, en préproduction ou en production, mais pas les deux.

| Environnement | Quand l’utiliser | `CDMS_HOST` |
| --- | --- | --- |
| Pré-production | Exécutions de préproduction ou de type sandbox, systèmes de gestion de contenu par composant hors production | `https://commerce-data-migration-service-preprod-external.adobe.io` |
| Production | Migration ou basculement de production en direct | `https://commerce-data-migration-service-prod-external.adobe.io` |

Définissez ou supprimez les commentaires du bloc correspondant à votre exécution :

```shell-session
# Pre-production CDMS
CDMS_HOST=https://commerce-data-migration-service-preprod-external.adobe.io
CDMS_PORT=443

# Production CDMS (use for prod cutover only)
# CDMS_HOST=https://na1.api.commerce.adobe.com
# CDMS_PORT=443
```

### Définir le code du magasin

`STORE_CODE` est le code d’affichage du magasin utilisé par l’outil de migration pour les appels API REST de l’instance source, la création d’un client de test synthétique et le nettoyage des données. Il est également envoyé en tant qu’en-tête `x-store-code` pendant la phase de chargement.

`STORE_CODE` valeur par défaut est `default` dans `.example.env`. Vérifiez que cela correspond au code d’affichage du magasin par défaut de votre instance source. Pour vérifier, dans la [!UICONTROL Admin] source, accédez à [!UICONTROL **Magasins**] > [!UICONTROL **Tous les magasins**] et regardez la colonne [!UICONTROL **Code**] pour l’affichage du magasin qui doit être utilisé. Si le code affiché n’est pas `default`, mettez à jour le `STORE_CODE` dans `.env` pour qu’il corresponde.

## Configurer le fichier de connexion à la base de données

>[!VIDEO](https://video.tv.adobe.com/v/3496152)

Le fichier `.my.cnf` fournit [!DNL MySQL] paramètres de connexion pour le côté extraction de l’outil de migration. Créez-le en copiant les `.my.cnf.example` dans les `.my.cnf` de la racine du projet. Le nom de la section doit correspondre à `SOURCE_CONNECTION_NAME` dans `.env`.

Pour une source sur site ou auto-hébergée :

```ini
[<connection-name>]
user=<db_user>
password='<db_password>'
host=<db_host>
port=3306
database=<db_name>
```

>[!NOTE]
>
>La machine qui exécute l’outil de migration doit disposer d’un accès réseau direct à la base de données source. L’outil n’établit pas ou ne vérifie pas automatiquement la connectivité locale. Vérifiez que l’hôte, le port et les informations d’identification sont accessibles à partir de la machine de migration avant d’exécuter toute commande de migration.

Pour une source [!DNL Adobe Commerce on Cloud] :

```ini
[<connection-name>]
id=<project_id>:<environment>
```

Le champ `id=` indique à l’outil que la source est PaaS et déclenche la configuration du tunnel à l’aide de `MAGENTO_CLOUD_CLI_TOKEN`. Les valeurs `project_id` et `environment` sont disponibles dans le [!DNL Cloud Console] ou par le biais des commandes `magento-cloud project:list` et `magento-cloud environment:list` .

## Préparation du réseau et des instances

L’authentification de base HTTP devant le magasin peut bloquer le trafic d’API et d’outils. Assurez-vous qu’elle est désactivée pour l’URL source utilisée par la migration ou que les chemins d’accès de l’outil sont autorisés, de sorte que les requêtes REST et GraphQL puissent atteindre le magasin .

### Maintenir la stabilité de la base de données source pendant l’extraction

Tandis que l’outil extrait les données de la base de données source, aucun autre processus ne doit y écrire. Les écritures simultanées peuvent entraîner un instantané incohérent.

- Arrêtez cron sur la source, et tous les planificateurs de système d’exploitation qui exécutent `bin/magento` ou d’autres rédacteurs, pour la fenêtre d’extraction, ou assurez-vous qu’ils ne peuvent pas s’exécuter pendant l’extraction.
- Passez en revue d’autres intégrations, telles que ERP, OMS, PIM, les tâches personnalisées et les API tierces qui écrivent dans la même base de données. Suspendre ou bloquer les écritures pour la fenêtre d’extraction afin que rien ne puisse faire muter les tables pendant l’exécution de l’extraction.
- Cela complète le mode de maintenance et l’accès au tunnel ou à la base de données. Ensemble, ils réduisent le trafic de storefront et d&#39;API. Les intégrations Cron et sont des sources distinctes d’écritures que vous devez contrôler explicitement.

### Target

Si le catalogue cible doit être effacé avant la migration, supprimez les produits en [!UICONTROL Admin] par petits lots, par exemple 200 à la fois, afin d’éviter les conflits de catalogues en double et les délais de suppression en masse.

## Créer et exécuter la migration

Travaillez à partir du répertoire du projet extrait avec un accès en écriture.

### Maintenir la session active via SSH

Si vous vous connectez via SSH, un réseau abandonné peut tuer votre shell et interrompre une longue migration. La commande GNU `screen` maintient la session active sur le serveur :

```bash
screen -S migration          # new session named "migration"
# run ./bin/console commands here; when you want to disconnect without stopping work:
# press Ctrl+A, release, then press d   # detach
screen -ls                   # list sessions
screen -x migration          # reattach to "migration"
```

Vous pouvez également utiliser `tmux` s’il est disponible sur le serveur.

### Créer l’image Docker

Créez l’image [!DNL Docker] utilisée par `bin/console`, qui contient PHP, l’interface de ligne de commande et les dépendances. Exécutez cette opération avant la première exécution ou après les modifications du fichier Docker ou de l’image de base.

```bash
./bin/console build
```

### Démarrer les services de support

Démarrez les services de sauvegarde [!DNL Docker Compose] de l’outil, tels que la base de données de test locale, puis, lorsqu’ils sont activés dans `.env`, les services locaux facultatifs. Les services exacts dépendent de votre configuration. Exécutez cette opération après une génération réussie et avant le shell, la migration ou les commandes par phases.

```bash
./bin/console start
```

### Initialiser le conteneur d’interface de ligne de commande

Démarrez une seule fois le conteneur de l’interface de ligne de commande afin que le point d’entrée puisse terminer la configuration (une installation [!DNL Composer], par exemple) pour votre projet monté. Exécutez cette opération une fois avant la première exécution de migration dans un nouvel environnement.

```bash
./bin/console shell
exit
```

### Exécuter la migration

L’outil prend en charge deux approches de migration. Choisissez celui qui correspond à votre cas d’utilisation.

#### Migration monophasée

Aucun mode de maintenance n’est requis sur l’instance source. Exécutez le pipeline de migration complet avec une seule commande :

```bash
./bin/console migration
```

La commande exécute automatiquement toutes les étapes du pipeline de bout en bout, dans l’ordre suivant.

1. **Vérification de configuration** — valide les variables d&#39;environnement et la configuration de l&#39;outil.
1. **Initialisation de l’environnement** : démarre les services [!DNL Docker], ouvre les tunnels cloud (le cas échéant) et exécute des tests unitaires.
1. **Tests d&#39;intégration et initialisation du CDMS** — exécute des tests d&#39;intégration et initialise la connexion de l&#39;API CDMS.
1. **Créer une migration** — enregistre la migration auprès du CDMS et attend l&#39;analyse du schéma cible. L’ID de migration est enregistré dans `.migration_id`.
1. **Tests fonctionnels et génération des données de test** — exécute des tests fonctionnels et génère des données de test synthétiques sur la source pour la vérification de l&#39;intégrité (si activé).
1. **Extraction des données** — extrait les données de l&#39;instance source.
1. **Charger dans la cible** — charge les données extraites dans l&#39;instance de [!DNL Adobe Commerce as a Cloud Service] cible. Les vues intermédiaires sont nettoyées sur la source et les données de test source sont supprimées via REST en parallèle de la charge.
1. **Vérification de l&#39;intégrité des données** — déclenche la vérification de la somme de contrôle et exécute les tests de vérification des API locales. Les résultats sont consignés et les échecs n’arrêtent pas le pipeline.
1. **Nettoyage des données de test sur la cible** — supprime les données de test synthétiques de l&#39;instance cible.
1. **Résultats du processus** — génère un résumé de la migration et télécharge éventuellement les artefacts du stockage.

Utilisez cette option lorsqu’aucune fenêtre de maintenance n’est requise, ce qui est courant pour les exécutions sèches de bout en bout, les environnements de développement ou de sandbox, ou toute migration où la source peut rester active pendant l’extraction.

>[!WARNING]
>
>N’utilisez pas cette option lorsqu’une source figée est requise, par exemple, lors d’une migration de production pour laquelle de nouvelles commandes ou des modifications de données ne doivent pas se produire pendant l’extraction. Utilisez plutôt une migration par phases. N’utilisez pas cette commande comme étape dans le workflow de maintenance par phases.

#### Migration multiphase avec mode de maintenance

Le mode de maintenance est requis sur l’instance source pour garantir la cohérence des données lors de l’extraction. La migration est divisée en phases distinctes que vous devez exécuter dans l’ordre.

>[!NOTE]
>
>Deux interfaces de ligne de commande différentes sont impliquées. Les commandes `./bin/console` s’exécutent à partir de la racine du projet de l’outil de migration. Les commandes `bin/magento maintenance:*` s’exécutent sur le serveur d’applications [!DNL Adobe Commerce] source, via SSH à la racine d’installation ou via le [!UICONTROL Admin] . L’outil n’émet pas de commandes de maintenance [!DNL Magento] en votre nom.

| Phase | Qui le dirige ? | Source state |
| --- | --- | --- |
| 1. `migration:before-maintenance` | Outil | En direct — ne pas encore activer la maintenance |
| &#x200B;2. Activer le mode de maintenance | Manuelle | Transition vers figé |
| 3. `migration:during-maintenance` | Outil | Gelé — ne pas désactiver la maintenance pendant cette phase |
| &#x200B;4. Désactiver le mode de maintenance | Manuel (conditionnel) | Reprise de la production de l’instance source |
| &#x200B;5. `migration:cleanup` (facultatif) | Outil | Actif : doit être hors maintenance. |

**Phase 1 — Avant la maintenance (la source est active)**

S’exécute lorsque l’instance source est active et accepte le trafic. L’accès REST et GraphQL à la source doit être entièrement disponible. N’activez pas le mode de maintenance avant la fin de cette phase.

Revenez à la racine du serveur et exécutez :

```bash
./bin/console migration:before-maintenance
```

1. **Vérification de configuration** — valide les variables d&#39;environnement et la configuration de l&#39;outil.
1. **Initialisation de l’environnement** : démarre les services [!DNL Docker], ouvre les tunnels cloud PaaS (le cas échéant) et exécute des tests unitaires.
1. **Tests d&#39;intégration et initialisation du CDMS** — exécute des tests d&#39;intégration et initialise la connexion de l&#39;API CDMS.
1. **Créer une migration** — enregistre la migration auprès du CDMS et attend l&#39;analyse du schéma cible. L’ID de migration est enregistré dans `.migration_id`.
1. **Tests fonctionnels** — exécute des tests fonctionnels sur la source active.
1. **Génération de données de test** — crée des clients et des commandes de test synthétique sur la source pour la vérification d&#39;intégrité (si activé).

**Phase 2 — Activer le mode de maintenance (manuel)**

Activez le mode de maintenance sur la source et mettez en pause toutes les activités qui écrivent dans la base de données ou qui ont un impact sur celle-ci, y compris les tâches planifiées, les intégrations tierces, le traitement des commandes et la synchronisation des ressources multimédias.

Sur le serveur Commerce source (racine d’installation), exécutez :

```bash
bin/magento maintenance:enable
```

**Phase 3 — Pendant la maintenance (la source est gelée)**

Exécutez avec l’instance source en mode de maintenance. La source doit rester gelée pendant toute la durée de cette phase. Ne désactivez pas le mode de maintenance tant que la **Phase 3** n’est pas terminée.

```bash
./bin/console migration:during-maintenance
```

1. **Configuration des tunnels cloud** — pour [!DNL Adobe Commerce on Cloud] instances source, rouvre les tunnels cloud et vérifie la connectivité de la base de données. Ignoré automatiquement pour les instances sur site.
1. **Extraction des données** — extrait les données de l&#39;instance source figée.
1. **Nettoyage des vues intermédiaires** — supprime les vues intermédiaires de la source à l&#39;aide d&#39;une connexion directe à la base de données (sans risque en mode de maintenance).
1. **Charger dans la cible** : charge les données extraites dans l&#39;instance de [!DNL Adobe Commerce as a Cloud Service] cible et attend la fin de l&#39;opération.
1. **Vérification de l&#39;intégrité des données** — déclenche la vérification de la somme de contrôle du CDMS et exécute les tests de vérification des API locales. Les résultats sont consignés et les échecs n’arrêtent pas le pipeline.
1. **Nettoyage des données de test sur la cible** — supprime les données de test synthétiques de l&#39;instance cible.
1. **Résultats du processus** — génère un résumé de la migration et télécharge éventuellement les artefacts du stockage.

**Phase 4 — Désactiver le mode de maintenance (manuelle, conditionnelle)**

Cette phase désactive le mode de maintenance et réactive le trafic vers l’instance source. Cette étape est requise avant d’exécuter la phase de nettoyage, car le nettoyage communique avec la source via REST et échoue avec `HTTP 503` si le mode de maintenance est toujours actif.

Sur le serveur Commerce source, exécutez :

```bash
bin/magento maintenance:disable
```

**Phase 5 — Nettoyage (facultatif, la source doit être active)**

Supprimez les clients et commandes de test synthétique créés dans **Phase 1** de l’instance source via REST. Cette phase ne peut s’exécuter qu’une fois le mode de maintenance désactivé.

>[!NOTE]
>
>Ignorer cette phase si `SKIP_TEST_DATA_CREATION=true` est défini dans `.env`, car aucune donnée de test n’a été créée.

Revenez à la racine du serveur et exécutez :

```bash
./bin/console migration:cleanup
```

1. **Configuration de la connexion à la base de données** — pour [!DNL Adobe Commerce on Cloud] instances source, rouvre les tunnels cloud. Pour les instances sur site, établit et vérifie la connectivité directe de la base de données.
1. **Nettoyage REST Source** — supprime les clients et les commandes de tests synthétiques de la source via l&#39;API REST.

## Reprise ou réexécution d’une migration

L’outil de migration suit la progression à l’aide d’un fichier `.migration_id` dans la racine du projet. Ce fichier est créé automatiquement lorsqu’une nouvelle migration démarre et enregistre l’identifiant de migration actuel.

### Reprendre après un échec

Si une exécution de migration échoue ou est interrompue, exécutez à nouveau la même commande pour reprendre à partir de la dernière étape réussie (extraction, chargement ou vérification) plutôt que de redémarrer à partir de zéro. Les étapes déjà terminées sont automatiquement ignorées.

>[!IMPORTANT]
>
>Lorsque vous reprenez la phase de `migration:during-maintenance`, la source doit rester en mode de maintenance tout au long de l’opération. Si la source a été retirée de la maintenance ou si les données ont été modifiées entre les exécutions, la reprise de la migration peut produire des résultats incohérents.

### Démarrer une nouvelle migration

Pour annuler une exécution précédente et démarrer une migration entièrement nouvelle, supprimez le fichier `.migration_id` avant de démarrer la migration suivante :

```bash
rm .migration_id
```

Si `.migration_id` existe et que la migration précédente est déjà terminée, l’outil imprime un message indiquant que la migration est déjà terminée et vous conseille de supprimer le fichier.

## Vérifier les journaux et le débogage

Tous les journaux de migration sont écrits dans le répertoire `logs/` dans la racine du projet et sont organisés en sous-répertoires horodatés :

```text
logs/
  2026-03-23_14-30-00/     ← one directory per run
    index.log              ← main pipeline log (start here)
    ...
```

- `index.log` est le journal principal de l’orchestration du pipeline. Si une étape a échoué, elle indique quel script s’est arrêté avec un code non nul et pourquoi.
- Les journaux par étape, tels que `09b_run_load.log` et `11_verify_data_integrity_local.log`, contiennent des sorties détaillées pour chaque phase.
