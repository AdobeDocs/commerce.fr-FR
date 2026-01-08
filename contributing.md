---
source-git-commit: 4ddab6bbd62a3cc7c6dff089745c1b5ef5c20f70
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---
# Contribution

Merci d&#39;avoir choisi de contribuer !

Voici un ensemble de directives à suivre lorsque vous contribuez à ce projet.

## Code de conduite

Ce projet respecte le [code de conduite](code-of-conduct.md) d’Adobe. En participant,
vous devez respecter ce code. Signaler tout comportement inacceptable à
[Grp-opensourceoffice@adobe.com](mailto:Grp-opensourceoffice@adobe.com).

## Documentation du guide du contributeur

Voir le [Guide du contributeur](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html?lang=fr).

## Vous avez une question ?

Commencez par signaler un problème. Les contributeurs actuels à ce projet doivent atteindre les objectifs suivants :
le cas échéant, consensus autour de la direction du projet et des solutions aux problèmes dans les fils de publication.

## Contrat de licence du contributeur

Toutes les contributions tierces à ce projet doivent être accompagnées d’un contributeur signé
contrat de licence. Adobe a ainsi la permission de redistribuer vos contributions
dans le cadre du projet. [Signez notre CLC](https://opensource.adobe.com/cla.html). Vous
Il suffit d’envoyer un contrat de licence du contributeur Adobe une fois. Si vous en avez déjà soumis un,
tout est fin prêt !

## Révisions du code

Toutes les soumissions doivent prendre la forme de demandes d’extraction et doivent être examinées
par les contributeurs au projet. Lisez la documentation relative à la demande d’extraction de [GitHub](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests)
pour plus d’informations sur l’envoi de requêtes d’extraction.

Enfin, suivez le modèle [demande d’extraction](PULL_REQUEST_TEMPLATE.md) lorsque
envoi d’une demande d’extraction !

## Du contributeur au validateur

Nous aimons les contributions de notre communauté ! Si vous souhaitez aller plus loin que le statut de contributeur
et devenez un validateur disposant d’un accès complet en écriture ayant son mot à dire dans le projet, vous devez :
être invité(e) au projet. Les contributeurs existants font appel à une nomination interne
processus qui doit aboutir à un consensus tacite (le silence est considéré comme une approbation) avant les invitations
sont émis. Si vous vous sentez qualifié et souhaitez vous impliquer davantage,
n’hésitez pas à contacter les contributeurs existants pour en discuter.

## Problèmes de sécurité

Pour signaler un problème de sécurité, [signalez-le à nos experts en sécurité](https://helpx.adobe.com/fr/security/alertus.html).

## Nouveautés

Si vos modifications introduisent de nouvelles rubriques, des mises à jour importantes ou des corrections qui doivent être mises en évidence, vous pouvez ajouter une brève description à la section [Quoi de neuf &#x200B;](https://experienceleague.adobe.com/fr/docs/commerce/user-guides/home#whats-new) directement à partir du corps de votre requête d’extraction.

Pour ajouter une mise en surbrillance Nouveautés :

1. Incluez la balise `whatsnew` avec la description appropriée dans le corps de votre requête de tirage à la fin. La description doit fournir un contexte sur la modification et un lien vers la ou les rubriques cibles. Utilisez le format suivant (les guillemets de bloc de code sont fournis à des fins de représentation uniquement, ne les incluez pas dans le corps de votre requête de tirage) :

   ```text
   whatsnew
   Short description of the change in the [target topic](https://experienceleague.adobe.com/en/docs/commerce/target-topic.html).
   ```

   ou, s’il existe plusieurs rubriques :

   ```text
   whatsnew
   Short description of the changes in the [first target topic](https://experienceleague.adobe.com/en/docs/commerce/target-topic.html), [second target topic](https://experienceleague.adobe.com/en/docs/commerce/second-target-topic.html), and [third target topic](https://experienceleague.adobe.com/en/docs/commerce/third-target-topic.html).
   ```

   vous pouvez également utiliser des listes pour plusieurs mises en surbrillance :

   ```text
   whatsnew
   - Short description of the first change in the [first topic](https://experienceleague.adobe.com/en/docs/commerce/first-topic.html).
   - Short description of the second change in the [second topic](https://experienceleague.adobe.com/en/docs/commerce/second-topic.html).
   ```

   ```text
   whatsnew
   The following changes were made to the documentation:
   - Short description of the first change in the [first topic](https://experienceleague.adobe.com/en/docs/commerce/first-topic.html).
   - Short description of the second change in the [second topic](https://experienceleague.adobe.com/en/docs/commerce/second-topic.html).
   ```

1. Ajoutez des libellés pris en charge qui indiquent le type de modification. Les libellés pris en charge comprennent les libellés de chaque type de modification, tels que :

   - `new-topic` - pour les nouvelles rubriques
   - `major-update` - pour les mises à jour majeures qui peuvent inclure des changements importants de contenu, de structure ou de fonctionnalité
   - `technical` - pour les modifications techniques qui ne sont pas considérées comme des mises à jour majeures, mais qui nécessitent toujours une attention particulière

**Important :**

1. La partie `whatsnew` doit commencer à partir de la balise `whatsnew` et se trouver à la toute fin du corps de la demande d’extraction.
1. Les descriptions des modifications doivent inclure des liens de travail. Assurez-vous que les liens sont corrects et mènent aux sujets prévus. Si la rubrique est nouvelle, vérifiez que les liens fonctionnent après la fusion de la demande d’extraction et la publication de la nouvelle rubrique. Vous pouvez corriger les liens après la fusion de la demande d’extraction.

Par exemple, recherchez dans les demandes d’extraction fermées du référentiel pour voir comment les mises en surbrillance existantes sont formatées, puis comparez-les à la section [Nouveautés](https://experienceleague.adobe.com/fr/docs/commerce/user-guides/home#whats-new) pour voir comment elles apparaissent dans la documentation.
