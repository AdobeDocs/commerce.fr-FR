---
title: Gouvernance de la documentation Commerce
description: 'Découvrez le modèle de gouvernance interne de Commerce Insights. Non publié sur Experience League : délibérément exclu de la table des matières.'
source-git-commit: 1da6d9753acbeadf3a0df5fae86a9386643c6d6d
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# Gouvernance de la documentation Commerce

Il s’agit d’une référence interne pour l’équipe de documentation. Il n’est pas répertorié dans `TOC.md`. Il n’est donc pas créé ni publié sur Experience League. Conservez-le ici afin qu’il reste proche du contenu qu’il régit.

## Propriété

Les articles Commerce Insights appartiennent à l’auteur ou à l’équipe de publication qui est chargé de veiller à leur exactitude et à leur actualité. Ces articles sont actuellement hébergés dans le référentiel `commerce.en`. L’équipe Documentation de Commerce vous aide à garantir la qualité du contenu et à publier l’article en production.

## Élément à inclure dans Commerce Insights

- **Appartient à ce groupe** : conseils stratégiques et livres blancs pour les solutions Commerce qui couvrent les conseils de mise en œuvre basés sur des scénarios réels. Incluez des liens vers les pages de documentation Commerce appropriées pour la prise en charge.

- **Appartient plutôt au référentiel de produit** : configuration détaillée, tutoriels, documents de référence (référence API/CLI/configuration) et dépannage. Si une publication commence à accumuler ce type de détails, déplacez-la vers le guide produit approprié et créez plutôt un lien vers celui-ci.

## Ajouter du nouveau contenu

Créez un ticket COMDOX JIRA pour l’article à publier. Copiez le `[templates/comdox-intake-template.md](templates/comdox-intake-template.md)` dans la description du ticket et renseignez-le : il demande au demandeur d’identifier l’audience, de signaler si le contenu est temporaire (avec une date d’expiration) et de confirmer qu’il appartient au guide des informations et non à la documentation du produit Commerce.

Une fois la portée du ticket atteinte, commencez l&#39;article à partir d&#39;un modèle en `templates/` (`whitepaper-template.md`, `security-guidance-template.md`, `insight-perspective-template.md`—non publié, copiez l&#39;article approprié dans le fichier cible et supprimez les commentaires de l&#39;espace réservé du frontmate du modèle). Ajoutez une entrée `TOC.md` une fois que le contenu est prêt à être publié.

- **La nouvelle section de niveau supérieur** (par exemple, Insights > Gestion de catalogue) nécessite une révision de l&#39;IA avant l&#39;ajout, car elle modifie la forme de navigation du guide. Effectuez une boucle dans la personne propriétaire de la révision Commerce IA pour l’histoire ou la tâche.

- **Ajouter à la table des matières** - Ajoutez une nouvelle rubrique à la table des matières avant de la publier. Si nécessaire, utilisez masquer les métadonnées pour publier un article masqué accessible uniquement aux personnes qui disposent du lien. Voir [Masquage du contenu](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/hiding-files) dans le Guide de l’auteur ExL.

## Rythme de révision

Consultez le contenu de l’article lorsque de nouvelles solutions Commerce sont renommées ou mises à jour, ou lorsque les informations ne sont plus pertinentes.
