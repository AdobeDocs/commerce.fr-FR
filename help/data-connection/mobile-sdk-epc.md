---
title: Intégration de Adobe Experience Platform Mobile SDK à Commerce
description: Découvrez comment utiliser le SDK mobile Adobe Experience Platform avec votre storefront Commerce découplé ou personnalisé.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: 02d07abb-8d7f-4f0a-9f96-f42654cd79d3
source-git-commit: a3e19940e2a3d8a240bb17703cfdd9903df311aa
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Intégration de Adobe Experience Platform Mobile SDK à Commerce

>[!IMPORTANT]
>
>Adobe Experience Platform Mobile SDK for iOS prend en charge iOS 11 ou une version ultérieure.

L’intégration de [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/) à l’application mobile Commerce permet aux commerçants d’envoyer des données Commerce [données d’événement](events.md) à Experience Platform Edge.

Lorsque les données d’événement Commerce sont disponibles en périphérie, elles sont accessibles par d’autres applications Adobe Experience Cloud. Par exemple, vous pouvez utiliser les données pour créer des audiences dans Real-Time CDP, puis [utiliser ces audiences](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html) pour personnaliser votre application mobile Commerce.

## Configuration

Pour commencer à utiliser Adobe Experience Platform Mobile SDK avec Commerce, installez et configurez SDK dans Experience Platform. Ensuite, finalisez votre configuration dans Commerce.

### Experience Platform

1. Découvrez les fonctionnalités des applications mobiles en consultant le tutoriel [Adobe Experience Cloud dans les applications mobiles](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html).

1. [Installation et configuration](https://developer.adobe.com/client-sdks/documentation/getting-started/) le SDK dans Experience Platform.

   >[!NOTE]
   >
   >Le schéma que vous créez et configurez dans Experience Platform est identique à celui que vous utilisez dans le code de l’application de votre application mobile Commerce.

### Commerce

Une fois la configuration SDK de la plateforme Experience Platform terminée, ajoutez la configuration SDK à Commerce.

1. Pour envoyer des données d’événement Commerce à Experience Platform via SDK, vous devez fournir un schéma XDM dans le code de l’application. Ce schéma doit correspondre au schéma [configuré](https://developer.adobe.com/client-sdks/home/getting-started/set-up-schemas-and-datasets/) pour le SDK dans Experience Platform.

   L’exemple suivant montre comment effectuer le suivi de l’événement `web.webpagedetails.pageViews` et définir la `identityMap` à l’aide du champ d’e-mail.

   ```swift
   let stateName = "luma: content: ios: us: en: home"
   var xdmData: [String: Any] = [
       "eventType": "web.webpagedetails.pageViews",
       "web": [
           "webPageDetails": [
               "pageViews": [
                   "value": 1
               ],
               "name": "Home page"
           ]
       ]
   ]
   
   let experienceEvent = ExperienceEvent(xdm: xdmData)
   Edge.sendEvent(experienceEvent: experienceEvent)
   
   // Adobe Experience Platform - Update Identity
   
   let emailLabel = "mobileuser@example.com"
   
   let identityMap: IdentityMap = IdentityMap()
   identityMap.add(item: IdentityItem(id: emailLabel), withNamespace: "Email")
   Identity.updateIdentities(with: identityMap)
   ```

1. Connectez-vous à l’environnement Commerce Cloud.

   Dans les paramètres de version de votre projet, ajoutez l’URL au point d’entrée Commerce GraphQL. Par exemple :

   - Déboguer : http://_debug_.commercesite.cloud/graphql/
   - Version : http://_release_.commercesite.cloud/graphql/

1. Pour récupérer des données à partir des points d’entrée Commerce GraphQL, générez d’abord les fichiers et répertoires nécessaires dans votre projet à l’aide du [Générateur de code Apollo](https://www.apollographql.com/docs/ios/).

   1. Dans le répertoire du projet, [installez](https://www.apollographql.com/docs/ios/get-started#1-install-the-apollo-frameworks) Apollo iOS.

   1. [Initialisez](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#initialize) l’interface de ligne de commande Apollo Codegen.

      Cela crée un fichier `apollo-codegen-configuration.json`.

   1. Générez les fichiers et répertoires GraphQL nécessaires dans votre projet en remplaçant le contenu du fichier `apollo-codegen-configuration.json` par ce qui suit :

      ```json
      {
      "schemaName" : "MagentoAPI",
      "input" : {
          "operationSearchPaths" : [
          "**/*.graphql"
          ],
          "schemaSearchPaths" : [
          "**/*.graphqls"
          ]
      },
      "output" : {
          "testMocks" : {
          "none" : {
          }
          },
          "schemaTypes" : {
          "path" : "../MagentoAPI",
          "moduleType" : {
              "swiftPackageManager" : {
              }
          }
          },
          "operations" : {
          "inSchemaModule" : {
          }
          }
      },
      "schemaDownloadConfiguration": {
          "downloadMethod": {
              "introspection": {
                  "endpointURL": "http://magento24.com/graphql/",
                  "httpMethod": {
                      "POST": {}
                  },
                  "includeDeprecatedInputValues": false,
                  "outputFormat": "SDL"
              }
          },
          "downloadTimeout": 60,
          "headers": [],
          "outputPath": "magento.graphqls"
      }
      }
      ```

   1. [Récupérer](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#fetch-schema) le schéma Commerce GraphQL.

      Assurez-vous que le chemin d’accès se trouve dans le fichier `./apollo-codegen-config.json` , qui contient la référence au schéma Commerce GraphQL.

   1. [Générez](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#generate) le code source.

      Assurez-vous que le chemin d’accès se trouve dans le fichier `./apollo-codegen-config.json` , qui contient les informations de configuration pour générer les fichiers et répertoires nécessaires.

   1. Dans le dossier **GraphQLGenerated** nouvellement créé, ajoutez ou modifiez des types GraphQL. Par exemple, vous pouvez ajouter un type de `DynamicBlocks.graphql` avec le contenu suivant :

      ```graphql
      query dynamicBlocks($input: DynamicBlocksFilterInput){
          dynamicBlocks(input: $input)
          {
              items {
                  content {
                      html
                  }
              }
          }
      }
      ```

   Vous avez maintenant intégré Adobe Experience Platform Mobile SDK à votre application mobile Commerce. Les données d’événement circulent de votre application vers Experience Platform Edge.

## Comment distinguer les événements Commerce générés à partir d&#39;applications mobiles

Tous les [événements](events.md) contiennent un champ appelé `channel`. Le champ `channel` contient `channel._id` et `channel._type` qui, pour un storefront Luma, ont respectivement les valeurs d’espace de noms `"https://ns.adobe.com/xdm/channels/web"` et `"https://ns.adobe.com/xdm/channel-types/web"`. Toutefois, pour un storefront mobile, les valeurs des espaces de noms sont respectivement `"https://ns.adobe.com/xdm/channels/mobile-app"` et `"https://ns.adobe.com/xdm/channel-types/mobile"`.

## Étapes suivantes

Pour savoir comment récupérer des audiences Real-Time CDP à partir de votre application Commerce mobile afin d’informer les règles de prix de panier, les blocs dynamiques et les règles de produit associées, consultez [Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html#retrieve-audiences-using-the-adobe-experience-platform-mobile-sdk).
