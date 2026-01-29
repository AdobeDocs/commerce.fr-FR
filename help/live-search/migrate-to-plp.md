---
title: Migration de l’adaptateur de recherche vers le widget PLP
description: Découvrez comment migrer de l’adaptateur de recherche obsolète vers le widget  [!DNL Live Search]  page de liste de produits.
source-git-commit: 8811f0f271928fbc827e5a0164542da473c57224
workflow-type: tm+mt
source-wordcount: '2053'
ht-degree: 0%

---

# Migration de l’adaptateur de recherche vers le widget PLP

L&#39;adaptateur de recherche a été [obsolète](release-notes.md#live-search-400) à partir de la version 4.0.0 de [!DNL Live Search] et ne recevra que les mises à jour de sécurité. Le widget [page de liste de produits (PLP)](plp-styling.md) est la solution prise en charge pour toutes les implémentations [!DNL Live Search] à l’avenir. Ce guide vous aide à comprendre quand la migration est simple et quand un travail supplémentaire est nécessaire.

## Conditions préalables

Assurez-vous que votre environnement répond à ces exigences avant de commencer le processus de migration.

Avant de commencer la migration :

**Exigences techniques** :

- Adobe Commerce 2.4.4 ou version ultérieure.
- Extension [!DNL Live Search] installée.
- Accès à la ligne de commande (CLI).
- Accès à l’administrateur Commerce.
- Environnement d’évaluation ou d’assurance qualité pour les tests.

**Sauvegarde et préparation** :

1. Sauvegardez votre base de données et votre code.
1. Documentez les personnalisations actuelles.
1. Examinez [Limites et limites](boundaries-limits.md) pour vous assurer que le widget PLP répond à vos besoins.
1. Planifiez la migration pendant une période de faible trafic.
1. Informez les parties prenantes des modifications potentielles du comportement du storefront.

**Examinez la mise en œuvre actuelle** :

- Vérifiez la version actuelle de votre [!DNL Live Search].
- Documentez les facettes utilisées et leur configuration.
- Tester toutes les fonctionnalités de recherche et documenter les comportements attendus.
- Capture d’écran de la présentation actuelle des résultats de recherche.

**Compatibilité des versions** :

- Exécution d’Adobe Commerce version 2.4.4 ou ultérieure.
- Prêt pour la mise à niveau vers [!DNL Live Search] 4.0.0 ou une version ultérieure.

## Scénarios de migration

### Migration simple (aucun travail supplémentaire requis)

Vous pouvez migrer directement vers le widget PLP si votre implémentation répond à TOUS les critères suivants :

**storefront standard basé sur Luma** :

- Vous utilisez le thème Luma ou un thème qui hérite de Luma avec un minimum de personnalisations.
- Vous n&#39;avez pas apporté de modifications personnalisées aux mises en page ou aux modèles PLP.
- Vous n’avez pas créé d’extensions JavaScript personnalisées qui interagissent avec les résultats de la recherche.

**Catalogue de produits standard** :

- Tous les attributs de produit utilisent des modèles source standard (et non des modèles source personnalisés).
- Il n’existe aucun type de produit personnalisé nécessitant une logique de rendu spéciale.
- Votre catalogue utilise uniquement des facettes et des filtres standard.

**Intégrations standard** :

- Vous n’utilisez pas Google Tag Manager (GTM) pour les analyses.
- Vous n’utilisez pas d’extensions tierces qui modifient le comportement de la recherche.

Si votre implémentation répond à ces critères, passez à la [Étapes de migration standard](#standard-migration-steps).

### Migration nécessitant un travail supplémentaire

Un travail supplémentaire est nécessaire si votre implémentation présente l’UNE des caractéristiques suivantes :

**Modifications du thème personnalisé** :

- Dispositions d’API personnalisées qui remplacent les modèles Luma.
- CSS ou JavaScript personnalisé qui cible les éléments spécifiques à l’adaptateur de recherche.
- Modifications du modèle personnalisé apportées à des fichiers PLP ou connexes.
- Le thème n’hérite pas de Luma (par exemple, le thème personnalisé à partir de zéro).

**Attributs de produit personnalisés** :

- Attributs de produit avec des modèles source personnalisés utilisés comme facettes.
- Types de produits personnalisés avec des exigences d’affichage spéciales.
- Attributs de programmation avec `"is_user_defined": false`.

**Intégrations avancées** :

- Google Tag Manager (GTM) est activement utilisé pour le suivi.
- Outils d’analyse ou de personnalisation tiers intégrés à la recherche.
- Suivi des événements personnalisés ou implémentation de la couche de données.
- Intégration à des moteurs de recherche ou de recommandation externes.

**Implémentations découplées ou PWA** :

- Utilisation de l’architecture découplée (par exemple, PWA Studio, Vue Storefront).
- Framework frontal personnalisé (React, Vue, Angular).
- Utilisation exclusive de GraphQL pour les requêtes de catalogue.
- Implémentation d’événements storefront personnalisés.

**Code de widget personnalisé** :

- Le code de l’adaptateur de recherche a été personnalisé précédemment.
- Hébergement de versions personnalisées de widgets sur votre propre réseau CDN.
- Extensions JavaScript personnalisées pour la fonctionnalité de recherche.

Si votre implémentation présente l’un de ces scénarios, voir [Scénarios de migration complexes](#complex-migration-scenarios).

## Étapes de migration standard

Pour les implémentations sans personnalisation spéciale, procédez comme suit :

### Étape 1 : mettre à niveau le [!DNL Live Search]

Mettez à niveau votre extension [!DNL Live Search] vers la version 4.0 ou ultérieure pour accéder au widget PLP.

**Rôle** : commerçant ou partenaire

1. Vérifiez votre version [!DNL Live Search] actuelle :

   ```bash
   composer show magento/live-search | grep version
   ```

1. Si vous utilisez la version 3.x ou antérieure, activez le module AdvancedSearch avant la mise à niveau :

   ```bash
   bin/magento module:enable Magento_AdvancedSearch
   ```

1. Mettez à jour `composer.json` pour exiger [!DNL Live Search] version 4.0 ou ultérieure :

   ```json
   "require": {
      "magento/live-search": "^4.0"
   }
   ```

1. Exécutez la mise à niveau :

   ```bash
   composer update magento/live-search --with-dependencies
   ```

1. Exécutez la mise à niveau du programme d&#39;installation et recompilez :

   ```bash
   bin/magento setup:upgrade
   bin/magento setup:di:compile
   ```

1. Déployez du contenu statique, si nécessaire :

   ```bash
   bin/magento setup:static-content:deploy
   ```

### Étape 2 : activer le widget PLP

Configurez le widget PLP dans l’administration Commerce.

**Rôle** : Marchand

Le widget PLP est activé par défaut pour les nouvelles installations d’[!DNL Live Search] version 4.0.0 ou ultérieure. Si vous effectuez une mise à niveau à partir d’une version antérieure :

1. Accédez à **[!UICONTROL Stores]** > Paramètres > **[!UICONTROL Configuration]**.
1. Accédez à **[!UICONTROL Live Search]** > **[!UICONTROL Storefront Features]**.
1. Développez la section **[!UICONTROL Storefront Features]** .
1. Définissez **[!UICONTROL Enable Product Listing Widgets]** sur **Oui**.
1. Cliquez sur **[!UICONTROL Save Config]**.
1. Videz le cache : **[!UICONTROL System]** > Outils > **[!UICONTROL Cache Management]** > **[!UICONTROL Flush Magento Cache]**.

### Étape 3 : test lors de l’évaluation

Validez la migration dans un environnement hors production avant de la mettre en ligne.

**Rôle** : Marchand/Partenaire

Avant le déploiement en production, testez minutieusement la fonctionnalité de recherche :

**Tests fonctionnels** :

- Vérifiez que les résultats de la recherche s’affichent correctement.
- Testez toutes les facettes configurées.
- Vérifiez que la navigation entre les catégories fonctionne.
- Test de la pagination à l’aide des résultats.
- Vérifiez que les options de tri fonctionnent comme prévu.
- Testez la fonctionnalité d’ajout au panier pour les produits simples.

**Test visuel** :

- Vérifiez que les images du produit s’affichent correctement.
- Vérifiez que les noms et les prix des produits s’affichent correctement.
- Testez les échantillons de couleurs (le cas échéant).
- Vérifiez le comportement réactif sur les appareils mobiles.
- Vérifiez que le style correspond à votre marque.

**Tests de performance** :

- Mesurer les temps de chargement des pages.
- Testez avec une taille de catalogue réaliste.
- Surveillez l’utilisation des ressources du serveur.
- Recherchez les erreurs JavaScript dans la console du navigateur.

### Étape 4 : déploiement en production

Déplacez la configuration validée vers votre storefront actif.

**Rôle** : Marchand/Partenaire

1. Planifiez le déploiement pendant la fenêtre de maintenance si possible.
1. Suivez votre processus de déploiement standard.
1. Activez le widget PLP en production à l’aide de [Étape 2 : activer le widget PLP](#step-2-enable-the-plp-widget).
1. Surveillez tout problème immédiatement après le déploiement.
1. Préparez un plan de restauration en cas de problèmes critiques.

### Étape 5 : valider et surveiller

Suivez les performances de recherche et l’expérience client après la migration.

**Rôle** : Marchand

Après le déploiement, surveillez les mesures clés :

- Taux de recherche de zéro résultat
- Taux de conversion de la recherche au panier
- Performances de chargement de page
- Commentaires des clients ou tickets d’assistance
- Erreurs JavaScript dans la console du navigateur

## Scénarios de migration complexes

Les scénarios suivants nécessitent une planification supplémentaire, un développement personnalisé ou une prise en charge spécialisée au-delà des étapes de migration standard.

### Thème personnalisé avec modifications de disposition

Dans ce scénario, vous disposez de modèles ou de mises en page personnalisés qui remplacent le comportement par défaut de la liste de produits.

**Rôle** : Développeur/Partenaire

1. **Personnalisations d’audit** :
   - Documentez tous les fichiers XML de disposition personnalisés dans votre thème.
   - Vérifiez les modifications apportées au modèle personnalisé aux pages de liste de produits ou aux fichiers associés.
   - Identifiez les classes CSS personnalisées utilisées pour le style.
   - Documentez les interactions JavaScript personnalisées.

1. **Migrer vers des personnalisations basées sur CSS** :
   - Le widget PLP utilise des classes CSS spécifiques (voir [guide de style PLP](plp-styling.md)).
   - Recréez des personnalisations visuelles à l’aide des classes CSS de widget PLP.
   - Vérifiez que les styles personnalisés s’appliquent correctement.

1. **Supprimer les personnalisations en conflit** :
   - Supprimez la disposition XML qui modifie la structure de la liste de produits.
   - Nettoyage de JavaScript qui cible les éléments spécifiques à l’adaptateur de recherche.
   - Mettre à jour les remplacements de modèle entrant en conflit avec le rendu du widget.

1. **Testez minutieusement** :
   - Vérifiez que toutes les personnalisations visuelles fonctionnent avec le widget PLP.
   - Vérifiez qu’il n’y a aucun conflit de mise en page.
   - Testez sur tous les points d’arrêt et appareils.

### Attributs de produit avec des modèles source personnalisés

Dans ce scénario, vous disposez de facettes qui utilisent des attributs de produit avec des modèles sources personnalisés qui ne sont pas pris en charge par l’adaptateur de recherche, mais qui SONT pris en charge par le widget PLP.

**Rôle** : Marchand (configuration d’administration)

1. **Identifiez les attributs affectés** :
   - Examinez les attributs de produit utilisés comme facettes.
   - Identifiez ceux qui utilisent des modèles sources personnalisés.
   - Documentez la configuration de facette actuelle.

1. **Mettez à niveau et activez le widget PLP** :
   - Suivez les [étapes de migration standard](#standard-migration-steps).
   - Le widget PLP prend en charge les attributs de modèle source personnalisés.

1. **Reconfigurez les facettes** :
   - Accédez à **[!UICONTROL Marketing]** > SEO et recherche > **[!UICONTROL Live Search]**.
   - Vérifiez la configuration des facettes pour les attributs concernés.
   - Les facettes de test fonctionnent correctement avec les modèles sources personnalisés.

1. **Valider** :
   - Testez le filtrage avec des facettes de modèle source personnalisées.
   - Vérifiez que toutes les valeurs d’attribut s’affichent correctement.
   - Assurez-vous que les performances sont acceptables.

### Intégration du gestionnaire de balises Google (GTM)

Dans ce scénario, il existe un problème connu en raison duquel l’activation du widget PLP peut entraîner l’échec de GTM.

**Rôle** : développeur/partenaire + ingénierie client

**Option 1 : continuer avec l’adaptateur de recherche (intermédiaire uniquement)**

- Gardez la carte de recherche activée si GTM est critique pour l&#39;entreprise.
- Sachez que vous ne recevrez que des mises à jour de sécurité.
- Planifiez la migration lorsque la compatibilité GTM est résolue.
- Contactez l’assistance Adobe pour obtenir des mises à jour sur la compatibilité avec GTM.

**Option 2 : Migrer le tracking GTM vers une autre approche**

1. **Implémentez une collection d’événements personnalisée** :

   - Utilisez le [SDK des événements Storefront](https://developer.adobe.com/commerce/services/shared-services/storefront-events/).
   - Capturez les événements d’interaction de recherche et de produit.
   - Envoyez manuellement les événements à la couche de données GMT.

1. **Procédez comme suit** :

   - Effectuez l’audit des exigences actuelles de suivi GTM.
   - Mappez les événements GTM aux événements Storefront.
   - Implémentez des écouteurs d’événement personnalisés.
   - Tester le flux de données vers GTM.
   - Validez les rapports d’analyse.

**Option 3 : Remplacer GTM par Adobe Analytics**

- Envisagez d’effectuer une migration vers [Adobe Analytics](https://business.adobe.com/products/adobe-analytics.html) le cas échéant.
- Contactez l’ingénierie client pour obtenir des conseils.

**Qui contacter** : envoyez un ticket d’assistance pour obtenir des mises à jour de compatibilité avec GTM ou une assistance en ingénierie client.

### Scénario : implémentation découplée ou PWA

Dans ce scénario, vous disposez d’un storefront découplé ou PWA qui nécessite une collecte d’événements personnalisée et qui ne peut pas utiliser l’interface utilisateur du widget PLP standard.

**Rôle** : Développeur/Partenaire

1. **Consultez les implémentations de référence** :
   - Étudiez le [code source du widget PLP](https://github.com/adobe/storefront-product-listing-page).
   - Consultez la documentation des API pour [[!DNL Live Search] GraphQL](graphql.md).
   - Comprenez les [requêtes du service de catalogue](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/).

1. **Implémentez une interface utilisateur personnalisée** :
   - Utilisez [!DNL Live Search]’API GraphQL pour les requêtes.
   - Créer des composants de liste de produits personnalisés.
   - Implémentez l’interface utilisateur pour les facettes.
   - Gérer la pagination et le tri.

1. **Implémentez la collecte d’événements** :
   - Consultez la [documentation sur les événements Storefront](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search).
   - Mettez en œuvre les événements requis :
      - `search-request-sent`
      - `search-response-received`
      - `search-results-view`
      - `product-page-view`
      - `add-to-cart`
   - Tester les flux de données d’événement vers Adobe Commerce.

1. **Configurer le tri à facettes** :
   - Pour les implémentations découplées, les facettes peuvent être triées par nombre.
   - Configurez dans **[!UICONTROL Live Search]** > Espace de travail **[!UICONTROL Facets]**.
   - Définissez **[!UICONTROL Sort Type]** sur **Count** pour une meilleure expérience utilisateur.

1. **Tester et valider** :
   - Vérifier la précision des résultats de recherche.
   - Testez la fonctionnalité de facettes.
   - Vérifiez que les événements sont correctement suivis.
   - Surveillez les mesures de performances.
   - Validez le fonctionnement des fonctionnalités de marchandisage intelligent.

### Scénario : modifications du code du widget personnalisé

Dans ce scénario, vous avez déjà personnalisé l’adaptateur de recherche ou le code de widget et vous devez migrer les personnalisations.

**Rôle** : Développeur/Partenaire

1. **Documenter les personnalisations existantes** :
   - Répertorier toutes les personnalisations apportées à l&#39;adaptateur de recherche.
   - Identifiez les besoins de l’entreprise qui motivent chaque personnalisation.
   - Déterminez si des personnalisations sont toujours nécessaires.

1. **Vérifiez si les fonctionnalités intégrées répondent à vos besoins** :
   - Examinez [fonctionnalités du widget PLP](plp-styling.md#widget-features).
   - Vérifiez si la personnalisation basée sur CSS est suffisante.
   - Testez le comportement par défaut du widget PLP.

1. **Si du code personnalisé est toujours nécessaire** :
   - Clonez le [référentiel de widgets PLP](https://github.com/adobe/storefront-product-listing-page).
   - Mettez en œuvre vos personnalisations.
   - Hébergez sur votre propre réseau CDN.
   - Mettez à jour la configuration de Commerce pour utiliser votre widget personnalisé.

   >[!WARNING]
   >
   >Si vous personnalisez le widget PLP à l’aide du code du référentiel, vous êtes responsable de la maintenance et des mises à jour. Les nouvelles fonctionnalités du widget PLP d’Adobe peuvent être incompatibles avec vos personnalisations.

1. **Testez minutieusement** :
   - Testez toutes les fonctionnalités personnalisées.
   - Vérifiez que les mises à jour de Commerce n’interrompent pas les personnalisations.
   - Documentez votre implémentation personnalisée.
   - Planifiez la maintenance continue.

## Limites connues et cas de périphérie

Tenez compte de ces limites lors de la migration :

**limites du widget PLP** :

- **Sens de l’ordre de tri** : lorsque le widget PLP est activé, le sens de l’ordre de tri sur les pages de liste de produits ne peut pas être modifié (croissant/décroissant).
- **Ajouter au panier** : les boutons Ajouter au panier ne sont disponibles que pour les produits simples dans le widget.
- **Tarification de niveau** : non pris en charge dans le widget PLP.
- **affichage TVA** : les prix incluent la TVA, mais celle-ci ne peut pas être affichée en tant que valeur distincte.

**Différences de caractéristiques de l’adaptateur de recherche** :

- **Échantillons de couleurs** : l’attribut `color` doit être orthographié exactement comme `color` (et non sous la forme de « couleurs » ou de noms personnalisés) pour que les échantillons fonctionnent correctement.
- **Style du thème** : les classes de thème personnalisées ne sont pas héritées par le widget. Elles doivent cibler les classes CSS spécifiques au widget.
- **Types de produits personnalisés** : non pris en charge dans le widget.

**Considérations relatives aux performances** :

- Les catalogues volumineux (plus de 50 000 produits) peuvent présenter un chargement initial de page plus long.
- Plusieurs facettes avec de nombreuses valeurs peuvent avoir un impact sur les performances.
- Les performances des appareils mobiles peuvent varier en fonction de la taille du catalogue.

**Problèmes de compatibilité** :

- Problème de compatibilité du gestionnaire de balises Google (voir [scénario GTM](#google-tag-manager-gtm-integration)).
- Certaines extensions tierces peuvent entrer en conflit avec le widget PLP.
- Les extensions de passage en caisse personnalisées peuvent nécessiter des mises à jour.

## Obtention d’aide

Contactez la ressource appropriée en fonction de vos besoins spécifiques.

L’assistance Adobe **** peut vous aider à :

- Procédures de migration standard de Live Search
- Problèmes de configuration du widget PLP
- Problèmes d’indexation des facettes ou des attributs
- Problèmes de performances liés aux implémentations par défaut
- Erreurs de mise à niveau

**Les partenaires de développement/intégrateurs système** doivent être contactés pour :

- Modifications du thème personnalisé
- Implémentations du code de widget personnalisé
- Compatibilité des extensions tierces
- Implémentations découplées ou PWA
- Suivi des événements personnalisés

Pour contacter l’assistance Adobe, consultez le [Guide d’utilisation du centre d’aide](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).

## FAQ

Trouvez des réponses aux questions courantes sur la migration de l’adaptateur de recherche vers le widget PLP.

**Q : L’adaptateur de recherche recevra-t-il des correctifs de bugs ou des mises à jour de fonctionnalités ?**

R : Non. L&#39;adaptateur de recherche est obsolète et ne recevra que les mises à jour de sécurité. Les correctifs de bugs, les améliorations de performances et les nouvelles fonctionnalités ne sont disponibles que dans le widget PLP. Si vous rencontrez des problèmes avec l’adaptateur de recherche, la migration vers le widget PLP est la solution recommandée.

**Q : La migration perturbera-t-elle mon storefront ?**

R : Si vous suivez les procédures de test appropriées lors de l’évaluation, la migration doit être transparente. disposer d’un plan de restauration prêt pour le déploiement en production ;

**Q : Combien de temps la migration prend-elle ?**

A : pour les implémentations standard : 1 à 2 heures. Pour les implémentations personnalisées : 1 à 4 semaines selon la complexité.

**Q : Mes règles de merchandising de recherche fonctionneront-elles toujours ?**

R : Oui, toutes les règles de marchandisage de recherche, les synonymes et les facettes configurés dans l’espace de travail [!DNL Live Search] continuent de fonctionner avec le widget PLP.

**Q : Ai-je besoin de reconfigurer mes facettes ?**

R : En règle générale, non, mais si vous étiez limité par des attributs de modèle source personnalisés avec l’adaptateur de recherche, vous pouvez désormais les utiliser avec le widget PLP.

**Q : Qu’en est-il de mon CSS personnalisé ?**

R : Vous devez mettre à jour CSS pour cibler les classes de widgets PLP. Voir la [référence des classes CSS](plp-styling.md#css-classes).

**Q : Cela affectera-t-il mes performances de recherche ?**

R : Le widget PLP est conçu pour être performant. La plupart des commerçants voient des performances égales ou supérieures. Les catalogues volumineux doivent être testés lors de l’évaluation.
