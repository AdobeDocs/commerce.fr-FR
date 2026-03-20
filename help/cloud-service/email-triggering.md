---
title: Déclenchement d’e-mail via REST
description: Découvrez comment déclencher des e-mails transactionnels à la demande à l’aide de l’API REST en spécifiant un identifiant de modèle, un e-mail de destinataire et des variables de modèle pour  [!DNL Adobe Commerce as a Cloud Service].
role: Admin
level: Experienced
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: 9661e368f7a0dc85edcd3e52a67ae2a98355d8b5
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# Déclenchement d’un e-mail via l’API REST

Auparavant, vous ne pouviez envoyer des e-mails que lorsque des événements étaient déclenchés, par exemple lors de l’enregistrement des clients ou de l’achat d’une commande. Dans [!DNL Adobe Commerce as a Cloud Service], vous pouvez envoyer des e-mails à la demande par l’intermédiaire de l’API REST en spécifiant un identifiant de modèle, l’adresse électronique du destinataire et des variables de modèle.

>[!NOTE]
>
>Actuellement, seuls les modèles personnalisés nouvellement créés peuvent être envoyés. Les modèles prédéfinis et système ne sont pas pris en charge.

Le point d’entrée `V1/custom-email/send` permet aux **systèmes tiers** tels que les intégrations et les services externes, d’envoyer des e-mails à la demande en spécifiant :

- **ID du modèle** - ID du modèle d’e-mail.
- **E-mail du destinataire** - Adresse e-mail cible de cette requête.
- **Variables** - (Facultatif) Paires clé-valeur définies personnalisées à injecter dans le modèle, par exemple `customer_name` ou `order_id`.

>[!NOTE]
>
>L’e-mail est envoyé de manière synchrone à l’aide de la portée de magasin actuelle et de l’adresse e-mail **De** par défaut ou définie pour les modèles.

## contrat REST

La section suivante explique comment envoyer des e-mails transactionnels à la demande à l’aide de l’API REST.

### Point d’entrée

- **URL** - `POST /rest/V1/custom-email/send`
- **Autorisation** - Seule l’**autorisation IMS service à service** est prise en charge. L’appelant doit avoir accès à la ressource **Envoyer un e-mail personnalisé via l’API** (`Magento_CustomEmailSend::send_custom_email`). Pour plus d’informations, voir [Authentification REST](https://developer.adobe.com/commerce/webapi/rest/authentication/).
- **Utilisation asynchrone** (recommandé) - Bien que ce point d’entrée soit implémenté de manière synchrone, nous vous recommandons de l’appeler à l’aide de l’**API REST asynchrone** afin que la requête soit mise en file d’attente et traitée par un client, en évitant les connexions HTTP de longue durée. Dans [!DNL Adobe Commerce as a Cloud Service], vous pouvez utiliser l’itinéraire avec `/async` après `V1`, par exemple : `POST https://<server>.api.commerce.adobe.com/<tenant-id>/V1/async/custom-email/send`.

  Pour plus d’informations, voir [Points d’entrée web asynchrones (SaaS)](https://developer.adobe.com/commerce/webapi/rest/use-rest/asynchronous-web-endpoints/).

### Corps de la requête

- **templateId** (entier, obligatoire) : ID du modèle d’e-mail tel que défini dans la section Admin sous [!UICONTROL **Marketing**] > [!UICONTROL _Communications_] > [!UICONTROL **Modèles d’e-mail**].

- **recipientEmail** (chaîne, obligatoire) : adresse e-mail cible. Le format d’e-mail doit être valide. Les valeurs manquantes ou vides déclenchent une erreur de validation.
- **variables** (objet, facultatif) - Mappage clé-valeur injecté dans le modèle sous forme de `UnstructuredArray`.

  Si vous n’utilisez pas de variables, transmettez un objet vide ou omettez-le. Dans le corps et l’objet du modèle d’e-mail, utilisez la syntaxe de variable pour référencer une variable, par exemple `var order_id`. L’objet prend également en charge les mêmes variables personnalisées et syntaxe que celles décrites dans [Scénarios de modèle pris en charge](#supported-template-scenarios).

### Réponse de succès (HTTP 200)

L’API renvoie un HTTP 200 lors d’un envoi réussi.

### Réponses d’erreur

- **HTTP 400 - Erreur de validation**

  L’intégration doit fournir un `templateId` et un `recipientEmail` valides pour chaque requête.

   - `"message": "Invalid recipient email format"` - adresse du destinataire non valide ou incorrecte
   - `"message": "Recipient email is required."` - `recipientEmail` manquant ou vide
   - `"message": "Template ID must be a positive integer."` - `templateId` manquant, nul ou non valide

- **HTTP 404 - Modèle introuvable**

  Exemple : `"message": "Email template with ID \"999\" does not exist."`

## Scénarios de modèle pris en charge

Les fonctionnalités de modèle suivantes sont prises en charge à la fois dans le **corps de l’e-mail** et l’objet du **modèle** :

>[!NOTE]
>
>L’objet du modèle prend également en charge les variables personnalisées. Utilisez le `var variableName` et d’autres syntaxes comme décrit dans la section suivante.

- **Directive Include** - pour inclure d&#39;autres modèles de conception, tels qu&#39;un en-tête d&#39;email.

  ```javascript
  {{template config_path="design/email/header_template"}}
  ```

- **Variables simples** - utilisez des `var variableName`, par exemple `var order_id` ou `var g`.

  ```javascript
  {{var order.test}}
  {{var g}}
  {{var order_id}}
  ```

- **Notation imbriquée/par points** - pour les clés imbriquées transmises dans le `variables` de requête, dans les traductions, utilisez des noms avec préfixe dollar, tels que `$order_data.customer_name`, `$order.increment_id` ou `$order_data.frontend_status_label`.

  ```javascript
  {{trans "%name," name=$order_data.customer_name}}
  {{trans "Your order #%increment_id has been updated with a status of **%order_status**." increment_id=$order.increment_id order_status=$order_data.frontend_status_label |raw}}
  ```

- **Traduction (trans)** : texte paramétré, traductions multilignes avec plusieurs espaces réservés et des balises HTML.

  ```javascript
  {{trans "%name," name=$order_data.customer_name}}
  {{trans "Your order #%increment_id has been updated with a status of **%order_status**." increment_id=$order.increment_id order_status=$order_data.frontend_status_label |raw}}
  ```

- **Sortie brute** - utilisez le filtre `|raw` lorsque le contenu traduit ou variable contient HTML (par exemple, `<strong>` ou `<a>`).

  ```javascript
  {{trans "Your order #%increment_id has been updated with a status of **%order_status**." increment_id=$order.increment_id order_status=$order_data.frontend_status_label |raw}}
  ```

- **URL helper** - pour stocker les URL dans les traductions.

  ```javascript
  {{trans 'You can check the status of your order by [logging into your account](%account_url).' account_url=$this.getUrl($store,'customer/account/',[_nosid:1]) |raw}}
  ```
