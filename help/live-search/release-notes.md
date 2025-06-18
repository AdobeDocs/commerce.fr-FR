---
title: Notes de mise à jour de [!DNL Live Search]
description: Dernières informations de mise à jour pour  [!DNL Live Search]  à partir d’Adobe Commerce.
feature: Services, Search, Release Notes
exl-id: 099cf79c-968c-4381-b66d-7f6141ad2db3
source-git-commit: ff5c717dbdd638e114bccc3f6dec26f4be269194
workflow-type: tm+mt
source-wordcount: '2500'
ht-degree: 0%

---

# Notes de mise à jour de [!DNL Live Search]

Ces notes de mise à jour décrivent les dernières versions de [!DNL Live Search].
La prise en charge est assurée pour la version majeure publiée actuelle. Les notes de mise à jour des anciennes versions sont fournies à titre de référence.
Les mises à jour incluent :

![Nouveau](../assets/new.svg) Nouvelles fonctionnalités
![Correctifs](../assets/fix.svg) Correctifs et améliorations
![Bogue](../assets/bug.svg) Problèmes connus

## Mises à jour des services hébergés

Ces notes décrivent les mises à jour qui ont été publiées en dehors d’une version versionnée ou les améliorations apportées au service hébergé.

_29 avril 2025_

![Correction](../assets/fix.svg) correction d’un problème en raison duquel le rapport **Exporter au format CSV** sur l’onglet [**Performances**](./performance.md) n’incluait pas toutes les données spécifiées dans la période.
![Correctif](../assets/fix.svg) Correction d’un problème qui empêchait l’enregistrement d’une [règle de marchandisage](./rules.md) si le filtre de requête de recherche était utilisé.
![Correctif](../assets/fix.svg) Correction d’un problème où les [produits épinglés](./facets-manage.md#pinunpin-facet) n’étaient pas répertoriés en haut de la page des résultats.

_21 avril 2025_

![Correction](../assets/fix.svg) Correction d’un problème lié au filtre de plage pour les prix, de sorte que les produits égaux à la plage supérieure ne soient pas inclus dans les résultats. Cette modification correspond à la façon dont les plages de prix sont définies pour les facettes.

_3 avril 2025_

![Correctif](../assets/fix.svg) Mise à jour de l’extension d’exportation de données SaaS afin de supprimer la limitation « Les produits doivent être affectés à la catégorie racine » [limitation](boundaries-limits.md#b2b-and-category-permissions) pour les commerçants B2B. Voir [Gérer l’extension d’exportation de données](../data-export/manage-extension.md) pour savoir comment mettre à jour l’extension d’exportation de données SaaS vers la version 103.4.0+.

_20 février 2025_

![Nouveau](../assets/new.svg) Commerce prend en charge les synonymes comportant plusieurs mots. [En savoir plus](synonyms-type.md#multi-word-synonym-behavior). La prise en charge des synonymes à plusieurs mots n’est disponible qu’après cette date de publication du 20 février. Tout synonyme existant comportant plusieurs mots nécessite une réindexation complète pour fonctionner, que vous pouvez demander en [créant un ticket d’assistance](https://experienceleague.adobe.com/fr/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).

_31 janvier 2025_

![Nouveau](../assets/new.svg) Il existe une nouvelle politique de conservation des données pour les données de catalogue non interrogées dans votre environnement de test. [En savoir plus](overview.md#catalog-data-retention-policy).

_19 septembre 2024_

![Nouveau](../assets/new.svg) sortie d’une version bêta qui prend en charge trois nouvelles fonctionnalités de recherche : superposée, commence par et contient. [En savoir plus](install.md#install-the-live-search-beta).

_4 septembre 2024_

![Correction](../assets/fix.svg) Augmentation du nombre maximal d’intervalles pouvant être renvoyés [dans une facette](boundaries-limits.md#facets) à 100.

_7 août 2024_

![Correctif](../assets/fix.svg) Augmentation de la valeur d’intervalle maximale, ou plage de prix, pour la [facettisation des prix](settings.md#price-faceting) de 10 000 à 40 000 000.

_13 février 2024_

![Nouveau](../assets/new.svg) [!DNL Live Search] prend désormais en charge la définition d’une règle par défaut pour [Marchandisage de recherche](rules.md).

_12 octobre 2023_

![Nouveau](../assets/new.svg) les administrateurs et administratrices de Commerce peuvent désormais spécifier la langue de l’index à [!DNL Live Search]. Voir [Paramètres](settings.md).
![Correctif](../assets/fix.svg) L’onglet « Règles de recherche » a été renommé « Marchandisage de recherche ».

_13 juin 2023_

![Correction](../assets/fix.svg) correction d’un problème où certains caractères tels que les guillemets ou les apostrophes provoquaient des problèmes de classement. La réindexation résout ces problèmes.

_25 avril 2023_

![Nouveau](../assets/new.svg) [!DNL Live Search] clients peuvent désormais profiter du nouvel indexeur de prix [SaaS](../price-index/price-indexing.md).

### Widget PLP

_2 mai 2025_

![Correctif](../assets/fix.svg) Correction d’un problème où le bouton Ajouter au panier restait en anglais lorsque le paramètre régional était remplacé par le français, l’allemand, l’italien ou l’espagnol.
![Correctif](../assets/fix.svg) Correction d’un problème où le bouton Ajouter au panier s’affichait pour les produits en rupture de stock.

_31 mai 2024_

![Nouveau](../assets/new.svg) Version 2.0.0 du widget PLP, qui prend en charge les fonctionnalités suivantes :

- Boutons Ajouter au panier - Disponible uniquement pour les produits simples.
- Plusieurs images par produit : l’image peut changer lorsqu’une couleur différente est choisie pour un produit configurable.

_27 octobre 2023_

![Nouveau](../assets/new.svg) Le widget [!DNL Live Search] PLP prend désormais en charge les échantillons de couleurs.

## [!DNL Live Search] 4.3.0

_1 mars 2025_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Fix](../assets/fix.svg) [!DNL Live Search] prend désormais en charge PHP 8.4 pour les installations exécutant Adobe Commerce 2.4.8-beta2.
![Correctif](../assets/fix.svg) Correction d’un problème en raison duquel l’adaptateur de recherche n’était pas compatible avec `psr/http-message:2.0`.

## [!DNL Live Search] 4.2.3

_13 février 2025_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Correction](../assets/fix.svg) Correction d’un problème en raison duquel la page des détails de la commande ne comportait pas le numéro de commande, la date et le bouton de **[!UICONTROL Reorder]**.

## [!DNL Live Search] 4.2.2

_6 janvier 2025_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Correctif](../assets/fix.svg) Correction d’un problème qui provoquait une erreur avec la requête `categoryList` GraphqL sur Adobe Commerce version 2.4.5 et antérieure.

## [!DNL Live Search] 4.2.1

_31 juillet 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Correctif](../assets/fix.svg) Correction d’un problème en raison duquel certains scripts ne se chargeaient pas sur la page de passage en caisse.
![Correctif](../assets/fix.svg) Correction d’une version de dépendance dans le fichier `composer.json`.

## [!DNL Live Search] 4.2.0

_31 mai 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) Extension Live Search mise à jour pour utiliser les widgets PLP version 2.0.0.

## [!DNL Live Search] 4.1.2

_16 mai 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

### Mises à jour

![Correction](../assets/fix.svg) Correction de la requête [`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-by-categories) GraphQL afin de filtrer correctement en fonction des `categoryPath` et des `categoryList` pour les catégories.

## [!DNL Live Search] 4.1.1

_19 mars 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

### Nouvelles fonctionnalités

![Nouveau](../assets/new.svg) Ajout de la prise en charge linguistique pour le polonais.
![New](../assets/new.svg) [!DNL Live Search] prend désormais en charge PHP 8.3 pour les installations exécutant Adobe Commerce 2.4.4.

## [!DNL Live Search] 4.1.0

_2 février 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

### Nouvelles fonctionnalités

![Nouveau](../assets/new.svg) Le [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/data-transfer/data-dashboard) est maintenant disponible. Ce tableau de bord remanié fournit des informations sur les flux de données pour [!DNL Product Recommendations], [!DNL Live Search] et [!DNL Catalog Service].

### Mises à jour

![Correctif](../assets/fix.svg) Correction d’un problème qui provoquait une erreur lorsque les utilisateurs invités ajoutaient des produits à un panier dans des vues de boutique autres que celles par défaut.
![Correction](../assets/fix.svg) Correction d’un problème en raison duquel la fenêtre contextuelle de recherche affichait toujours le symbole de devise devant la valeur de prix, quels que soient les paramètres régionaux.
![Correctif](../assets/fix.svg) Suppression des définitions de type inutiles pour les plug-ins principaux désactivés afin de résoudre les problèmes de compatibilité lors de l’installation.

## [!DNL Live Search] 4.0.0

_13 novembre 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

### Nouvelles fonctionnalités

![Nouveau](../assets/new.svg) [!DNL Live Search] prend désormais en charge les échantillons de couleurs dans le widget PLP.
![Nouveau](../assets/new.svg) [!DNL Live Search] affiche désormais le nom de la catégorie plutôt que l’ID de la catégorie.
![Nouveau](../assets/new.svg) [!DNL Live Search] prend désormais en charge les prix barrés dans le widget PLP.
![Nouveau](../assets/new.svg) Ajout du bouton « Masquer les filtres » pour masquer le panneau des filtres.


### Mises à jour

![Correctif](../assets/fix.svg) Le widget [!DNL Live Search] PLP est désormais activé par défaut pour les nouvelles installations.
![Correctif](../assets/fix.svg) La carte de recherche est obsolète. À l’avenir, l’adaptateur de recherche ne sera mis à jour que pour résoudre les problèmes de sécurité.
![Correctif](../assets/fix.svg) Styles CSS reconfigurés pour mieux isoler les classes de widgets.
![Correctif](../assets/fix.svg) Correctifs mineurs

Après l’installation de la version 3.1.1 ou ultérieure, activez les nouveaux indexeurs :

- Flux des prix des produits
- Étendue du flux de données du site Web
- Étendue du flux de données des groupes de clients

Après la mise à niveau, testez la configuration mise à jour dans le contrôle qualité ou l’évaluation avant d’envoyer les modifications en production.

+++3.1.1 et versions antérieures

### [!DNL Live Search] 3.1.1

_15 septembre 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) Un nouvel onglet Marchandisage de catégorie a été ajouté. Les utilisateurs peuvent désormais ajouter des classements intelligents et des classements manuels (épingle, boost, bury, hide) par catégorie
![Nouveau](../assets/new.svg) Les utilisateurs peuvent ajouter une règle de catégorie unique avec un classement intelligent ou manuel
![Nouveau](../assets/new.svg) les utilisateurs peuvent désormais ajouter des règles de classement intelligent aux sous-catégories
![Nouveau ](../assets/new.svg) des informations détaillées sont fournies lors de la suppression de sous-catégories avec classement intelligent
![Nouveau](../assets/new.svg) Ajout de la possibilité de supprimer des règles pour les stratégies de classement héritées
![Nouveau](../assets/new.svg) Ajout de la possibilité de supprimer des règles pour une seule catégorie
![Nouveau ](../assets/new.svg) les utilisateurs peuvent désormais effectuer une recherche par nom de catégorie lors de l’ajout d’une règle
![Nouveau](../assets/new.svg) Avec la vue Arborescence des catégories, les utilisateurs peuvent désormais afficher la catégorie à laquelle des règles sont appliquées.
![Nouveau](../assets/new.svg) l’aperçu des catégories affiche uniquement la catégorie sélectionnée.
Les composants ![Nouveau](../assets/new.svg) CIF AEM [Widget contextuel](https://github.com/adobe/aem-cif-guides-venia/pull/319) et [Widget PLP](https://github.com/adobe/aem-cif-guides-venia/pull/320) permettent aux sites AEM de tirer parti de l’[!DNL Live Search].

#### Mises à jour

![Correctif](../assets/fix.svg) La taille de la table des flux Produits et Prix a été considérablement réduite. Les tableaux `catalog_data_exporter_products` et `catalog_data_exporter_product_prices` doivent présenter une réduction substantielle de la taille.
![Correctif](../assets/fix.svg) L’onglet « Règles » est renommé « Règles de recherche »
![Correctif](../assets/fix.svg) Lors du classement par &#39;tendance&#39;, vous pouvez désormais choisir entre :
- 3 jours (par défaut)
- 14 jours
- 30 jours
![Correctif](../assets/fix.svg) &#39;Événements&#39; (Amplifier/Épingler/Enterrer/Masquer) a été renommé en &#39;Classement manuel&#39;
![Correctif](../assets/fix.svg) &#39;Type de classement&#39; a été renommé en &#39;Classement intelligent&#39;
![Correctif](../assets/fix.svg) Correctifs mineurs

### [!DNL Live Search] 3.1.0

_1er septembre 2023_

[!BADGE Pris en charge]{type="Informative" tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

#### Mises à jour

![Correctif](../assets/fix.svg) Le widget Liste des produits a été mis à jour pour utiliser l’[API Catalog Service](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/).

### [!DNL Live Search] 3.0.2

_7 août 2023_

[!BADGE Pris en charge]{type="Informative" tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

#### Nouvelles fonctionnalités

![Nouveau](../assets/new.svg) Les valeurs suivantes ont été ajoutées à l&#39;objet `storeDetails` :

- « Autoriser tous les produits par page »
- Taux de change
- « Produits par page sur les valeurs autorisées de la grille »
- « Produits par page sur la valeur par défaut de la grille »
- Stocker la langue

#### Mises à jour

![Correctif](../assets/fix.svg) les modules du service de catalogue ont été ajoutés au métapaquet pour prendre en charge la récupération avancée des données.
![Correctif](../assets/fix.svg) La navigation sur la page **Mon compte** ne disparaît plus lors de l’utilisation du widget Page de liste de produits.

Les commerçants doivent mettre à niveau la version >= 3.0.2 de l’extension [!DNL Live Search] pour accéder à ces fonctionnalités.

Il est recommandé de mettre à niveau et de tester avant de passer en production. Envisagez de mettre à niveau l’environnement de production pendant les heures creuses après avoir vérifié les résultats de leur environnement de test.

#### Restrictions

L’utilisation du widget Page de liste de produits Live Search entraîne l’échec de Google Tag Manager. Utilisez l’adaptateur de recherche par défaut si Google Tag Manager est nécessaire.

### [!DNL Live Search] 3.0.1

_14 mars 2023_

[!BADGE Pris en charge]{type="Informative" tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

#### Nouvelles fonctionnalités

![Nouveau](../assets/new.svg) fiche article de produit dans l&#39;aperçu des règles
![Nouveau](../assets/new.svg) [widget de page de liste de produits](https://experienceleague.adobe.com/fr/docs/commerce/live-search/live-search-storefront/plp-styling)
![Nouvelle](../assets/new.svg) [Options de filtrage par catégorie](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#facets)
![Nouveau](../assets/new.svg) Possibilité de glisser-déposer pour créer des événements d’épingle
![Nouveau](../assets/new.svg) nouvelles actions d’épingle :
- Épingler à l’emplacement - Bouton Épingler pour créer un événement d’épingle en un seul clic
- Épingler en haut - Place le produit en première position
- Épingler en bas - Place le produit en bas des résultats
- Désépingler un événement en un clic
![Nouveau](../assets/new.svg) [Classement intelligent des règles](https://experienceleague.adobe.com/fr/docs/commerce/live-search/live-search-admin/rules/rules-add)
![Nouveau](../assets/new.svg) [!DNL Live Search] prend désormais en charge les fonctionnalités [Inventory management](https://experienceleague.adobe.com/fr/docs/commerce-admin/inventory/introduction) complètes dans Commerce (anciennement connu sous le nom de Multi-Source Inventory, ou MSI). Pour activer la prise en charge complète, vous devez [mettre à jour](install.md#update) le module de dépendance `commerce-data-export` à la version 102.2.0+.

#### Mises à jour

![Corriger](../assets/fix.svg) Configurer les règles trie désormais automatiquement les positions de manière unique
![Correctif](../assets/fix.svg) La suppression d’un événement existant met désormais à jour l’aperçu
![Correction](../assets/fix.svg) Les règles sans événement peuvent être enregistrées
![Corriger](../assets/fix.svg) Supprimer le sélecteur de facettes « Sélectionner le type »
![Correctif ](../assets/fix.svg) ajout d’un nouveau statut « Modification » pour les règles non enregistrées

#### Correctifs

![Correctif](../assets/fix.svg) Correction d’une erreur de serveur lorsqu’un événement est inachevé lors de l’enregistrement
![Corriger](../assets/fix.svg) Correction de la suppression d’un événement spécifique en présence de plusieurs événements
![Correctif](../assets/fix.svg) Correction de l’événement de règle existant qui ne se mettait pas à jour lorsque un nouvel événement était ajouté
![Correctif](../assets/fix.svg) Corrigé lors du second clic « Modifier » dans les détails, [!DNL Live Search] page nécessitant un rechargement
![Correctif](../assets/fix.svg) Synonymes : correction d’un problème en raison duquel un utilisateur cliquait sur une entrée et ne pouvait pas renvoyer le focus au champ
![Correctif](../assets/fix.svg) Autres correctifs mineurs et mises à jour des performances
![Bug](../assets/bug.svg) - Le classement par « Recommandé pour vous » n’est pris en charge que dans les widgets de recherche en direct. Il n’est pas pris en charge avec la fonctionnalité de recherche par défaut de Luma et PWA.
![Bug](../assets/bug.svg) - Les facettes d’attribut de prix personnalisé ne s’affichent pas correctement dans Luma, mais l’API les filtre correctement.

Les commerçants doivent mettre à niveau la version >= 3.0.1 de l’extension [!DNL Live Search] pour accéder à ces fonctionnalités.

Il est recommandé de mettre à niveau et de tester avant de passer en production. Envisagez de mettre à niveau l’environnement de production pendant les heures creuses après avoir vérifié les résultats de leur environnement de test.

### [!DNL Live Search] 2.0.5

[!BADGE Pris en charge]{type="Informative" tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Correctif](../assets/fix.svg) - La recherche en direct générait une erreur lorsque les ressources SDK n’étaient pas disponibles en raison de problèmes réseau. Ce bogue est corrigé.

Les commerçants doivent mettre à niveau l’extension Live Search version >= 2.0.5 pour accéder à ces fonctionnalités.

Il est recommandé de mettre à niveau et de tester avant de passer en production. Envisagez de mettre à niveau l’environnement de production pendant les heures creuses après avoir vérifié les résultats de leur environnement de test.

### [!DNL Live Search] 2.0.4

[!BADGE Pris en charge]{type="Informative" tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) la recherche en direct prend désormais en charge le filtrage par le paramètre « Afficher les produits en rupture de stock » dans l’administration. Si Afficher les produits en rupture de stock est défini sur false, `inStock = true` est ajouté au filtre.
![Correctif](../assets/fix.svg) Pour améliorer les performances, le bloc « Suggestions » a été supprimé de la fenêtre contextuelle de recherche en direct. Les données sont toujours transmises par GraphQL, au cas où vous voudriez remplacer la fonction.
![Correctif](../assets/fix.svg) les `categories` et `categoryPath` ont remplacé les `categoryIds` pour le filtrage de catégorie. En savoir plus dans la rubrique [productSearch](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/).
![Correctif](../assets/fix.svg) Auparavant, un utilisateur lié à une société B2B recevait un code de groupe client incorrect lors des recherches. La recherche en direct renvoie désormais la valeur correcte.
![Correctif](../assets/fix.svg) Auparavant, lors de la recherche d’un terme qui n’existe pas, la recherche en direct renvoyait une erreur. Ce bogue est maintenant corrigé.

Les commerçants doivent mettre à niveau la version >= 2.0.4 de l’extension [!DNL Live Search] pour accéder à ces fonctionnalités.

Il est conseillé aux utilisateurs de mettre à niveau et de tester avant de passer en production. Envisagez de mettre à niveau l’environnement de production pendant les heures creuses après avoir vérifié les résultats de leur environnement de test.

### [!DNL Live Search] 2.0.3

[!BADGE Pris en charge]{type="Informative" tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) la recherche en direct prend désormais en charge les fonctionnalités B2B en respectant les autorisations de catégorie, les catalogues partagés et la tarification spécifique au groupe client.

Les commerçants doivent mettre à niveau la version >= 2.0.3 de l’extension [!DNL Live Search] pour accéder à ces fonctionnalités.

Il est conseillé aux utilisateurs de mettre à niveau et de tester avant de passer en production. Envisagez de mettre à niveau l’environnement de production pendant les heures creuses après avoir vérifié les résultats de leur environnement de test.

### [!DNL Live Search] 2.0

[!BADGE Pris en charge]{type="Informative" tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

Les installations [!DNL Live Search] existantes doivent être mises à niveau vers la version 2.0.0 de [!DNL Live Search] pour tirer parti des nouvelles fonctionnalités, des correctifs et des améliorations suivants :

![New](../assets/new.svg) [!DNL Live Search] prend désormais en charge PHP 8.1 pour les installations exécutant Adobe Commerce 2.4.4.
![Nouveau](../assets/new.svg) le module `Magento_ElasticsearchCatalogPermissionsGraphQl` est ajouté à la liste des modules qui sont désactivés lors de l&#39;installation.
![Nouveau](../assets/new.svg) Le nombre de lignes disponibles dans le [[!DNL storefront popover]](overview.md) peut être configuré à partir de l’*Admin*.
![Nouveau](../assets/new.svg) Beta [PWA](https://developer.adobe.com/commerce/pwa-studio/) pris en charge pour [!DNL Live Search].
![Nouveau](../assets/new.svg) Le processus d&#39;installation de [!DNL Live Search] est mis à jour avec des modifications de processus avancées.
![Correctif](../assets/fix.svg) [Recherche avancée](https://experienceleague.adobe.com/fr/docs/commerce-admin/catalog/catalog/search/search) lien supprimé du pied de page du storefront.
![Bogue](../assets/bug.svg) Les attributs de produit suivants ne sont pas pris en charge par l’API Commerce GraphQL lorsqu’ils sont utilisés dans le cadre de la version bêta de PWA : `description`, `name`, `short_description`
![Bogue](../assets/bug.svg) la version bêta de PWA for [!DNL Live Search] ne prend pas en charge [la gestion des événements](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/).[&#128279;](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/)

### [!DNL Live Search] 3.1

[!BADGE Pris en charge]{type="Informative" tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Correctif](../assets/fix.svg) [Attribut de prix personnalisé](https://experienceleague.adobe.com/fr/docs/commerce-admin/catalog/product-attributes/attributes-input-types) ne renvoie plus d’erreur lorsqu’il est configuré en tant que [facette](facets-add.md).
![Correctif](../assets/fix.svg) Correction d’un problème qui entraînait l’apparition d’une erreur lorsqu’aucun [symbole de devise](https://experienceleague.adobe.com/fr/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration#step-5-customize-currency-symbols-optional) (`data-currency-symbol`) n’était disponible.
![Correctif](../assets/fix.svg) [[!DNL Storefront popover]](storefront-popover.md) affiche désormais le [Prix spécial](https://experienceleague.adobe.com/fr/docs/commerce-admin/catalog/products/pricing/product-price-special) (prix final minimum) lorsqu’il est disponible.

### [!DNL Live Search] 1.3.0

[!BADGE Pris en charge]{type="Informative" tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

Le ![nouveau](../assets/new.svg) [tableau de bord de création de rapports Performance](performance.md) fournit insight dans les termes de recherche utilisés par les acheteurs.
![Nouveau](../assets/new.svg) [!DNL Live Search] [Storefront Events SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/) permet d’accéder à une couche de données commune avec des services, des mesures et des services d’abonnement et de publication d’événements.
![Correctif](../assets/fix.svg) La [[!DNL Storefront popover]](storefront-popover.md) comporte une nouvelle classe `active` pour le conteneur `.search-autocomplete` qui contrôle la visibilité.
![Correctif](../assets/fix.svg) Dans le storefront, le lien de pied de page [Termes de recherche](https://experienceleague.adobe.com/fr/docs/commerce-admin/catalog/catalog/search/search-terms) est supprimé et son cache désactivé pour les installations de [!DNL Live Search].
![Bogue](../assets/bug.svg) le correctif pour l’adaptateur de recherche gère les produits en double.
![Bogue](../assets/bug.svg) [!DNL Live Search] prend en charge les emplacements d’inventaire [source unique](https://experienceleague.adobe.com/fr/docs/commerce-admin/inventory/sources/sources-manage) (physique) avec plusieurs [stocks](https://experienceleague.adobe.com/fr/docs/commerce-admin/inventory/stocks/stocks-manage) (virtuels). Les sources d’inventaire multiples ne sont pas prises en charge actuellement.

### [!DNL Live Search] 1.2.0

[!BADGE Pris en charge]{type="Informative" tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) [[!DNL Storefront popover]](storefront-popover.md) affiche les suggestions de produits et des images miniatures des principaux résultats de recherche lorsque les acheteurs saisissent des requêtes dans la zone de recherche.
La session ![New](../assets/new.svg) Commerce *Admin* reste ouverte pendant de longues périodes d’inactivité du clavier
![Nouveau](../assets/new.svg) [!DNL Live Search] est automatiquement activé après l’intégration
![Correctif](../assets/fix.svg) Le temps d’indexation initial est inférieur à une heure
![Correctif](../assets/fix.svg) Mises à jour incrémentielles des produits en temps quasi réel (après installation et configuration)
![Corriger](../assets/fix.svg) Colonnes triables dans l’éditeur de synonymes
![Corriger](../assets/fix.svg) [!DNL Live Search] ne renvoie plus d’erreur si les critères de recherche contiennent une valeur d’ordre de tri vide
![Correction](../assets/fix.svg) Le filtrage par plage ne se rompt plus si les codes d’attribut contiennent des chaînes « vers » ou « de »

### [!DNL Live Search] 1.1.0

[!BADGE Pris en charge]{type="Informative" tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Bogue](../assets/bug.svg) Le service [!DNL Live Search] prend uniquement en charge la [devise de base](https://experienceleague.adobe.com/fr/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration) de l’installation d’Adobe Commerce.
![Bogue](../assets/bug.svg) lors de l’ajout d’une facette, le flux des attributs de produit ne se met pas correctement à jour lorsqu’il est défini sur `Update on Save`. Pour éviter ce problème, accédez à [Gestion des index](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/tools/index-management) et définissez le flux des attributs de produit sur `Update by Schedule`.
![Bug](../assets/bug.svg) [!DNL Live Search] synonymes sont définis par vue de magasin, mais sont actuellement stockés par site web et identifiés par une combinaison de `environmentId` et de `storeViewCode`. Par conséquent, tous les sites web et vues de magasin de l’installation d’Adobe Commerce partagent des synonymes. L’ensemble de synonymes le plus récemment créé pour la vue de magasin est prioritaire.
![Bug](../assets/bug.svg) Si un terme de synonyme contient plusieurs mots, chaque mot est traité comme un synonyme distinct. Par exemple, si vous définissez « pièce d’horlogerie » comme synonyme de « montre », « heure » et « pièce » sont tous deux traités comme des synonymes de montre.

+++

## Documentation

Pour en savoir plus :

- [Documentation destinée aux développeurs Adobe Commerce](https://developer.adobe.com/commerce/docs)
- [Guide de l’utilisateur Adobe Commerce](https://experienceleague.adobe.com/fr/docs/commerce)
- [[!DNL Live Search] sur Marketplace](https://commercemarketplace.adobe.com/magento-live-search.html)
