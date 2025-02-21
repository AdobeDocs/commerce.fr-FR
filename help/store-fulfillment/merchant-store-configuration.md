---
title: Configuration des magasins marchands
description: Configurez les sources Inventory management améliorées comme magasins marchands.
role: Admin
level: Experienced
feature: Shipping/Delivery, Inventory, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 0%

---

# Configuration des magasins marchands (Source)

Cette solution améliore les fonctionnalités natives d’Inventory management en étendant les sources de stocks avec des fonctionnalités orientées opérations pour les commerçants.

- Ajouter les coordonnées géographiques de l’emplacement du magasin
- Désignez la source comme [!DNL Store Pickup Location] et spécifiez les fonctionnalités d’expédition disponibles (Expédier vers le magasin, Expédier à partir du magasin).
- Spécifiez les options de retrait disponibles (en magasin ou à la rue), les instructions de retrait personnalisées et d’autres informations pour communiquer les détails et les instructions de retrait aux clients

Les termes _source_ et _emplacement du magasin marchand_ sont utilisés de manière interchangeable. Tous les enregistrements sont des sources de stock, mais les sources peuvent également être des emplacements de magasin marchand, selon les paramètres de configuration.

Gérez la configuration des magasins marchands à partir de l&#39;administrateur : **[!UICONTROL Stores > Inventory > Sources >  Edit Source]**.

>[!NOTE]
>
>Pendant le processus de configuration, il peut être nécessaire de vider le cache après avoir créé des sources ou mis à jour des sources existantes.

## **Général**

<table>
<tbody>
<tr>
<th>Champ</th>
<th>Description</th>
<th>Champ d’application</th>
<th>Obligatoire</th>
</tr>
<tr>
<td><strong>[!UICONTROL Latitude]</strong></br><code>Base Attribute: latitude</code></td>
<td>Coordonnée latitude de l’emplacement du magasin marchand. Ces informations requises sont utilisées dans la recherche d’emplacement et l’emplacement du mappage sur l’expérience storefront. La valeur doit correspondre à l’adresse exacte du magasin pour passer la validation.</td>
<td>Global</td>
<td>Oui</td>
</tr>
<tr>
<td><strong>[!UICONTROL Longitude]</strong></br><code>Base Attribute: Longitude</code></td>
<td>Coordonnée longitudinale de l’emplacement du magasin marchand. Ces informations requises sont utilisées dans la recherche d’emplacement et l’emplacement du mappage sur l’expérience storefront. La valeur doit correspondre à l’adresse exacte du magasin pour passer la validation.</td>
<td>Global</td>
<td>Oui</td>
</tr>
<tr>
<td><strong>[!UICONTROL Use as Pickup Location]</br></strong><code>Base Attribute: is_pickup_location_active</code></td>
<td>Désignez la source comme emplacement de prélèvement de magasin disponible. Ce paramètre détermine si la source est synchronisée et affichée pour les visiteurs.</td>
<td>Global</td>
<td>Non</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship to Store]</strong><br><code>Extension Attribute: allow_ship_to_store</code></td>
<td>Configurez les fonctionnalités de livraison à la boutique au niveau de la source. Pour plus d'informations, voir l'option [Configuration générale](enable-general.md), <strong>[!UICONTROL Enable Ship To Store]
</tr>
<tr>
<td><strong>[!UICONTROL Latitude]</strong></br><code>Base Attribute: latitude</code></td>
<td>Coordonnée latitude de l’emplacement du magasin marchand. Ces informations requises sont utilisées dans la recherche d’emplacement et l’emplacement du mappage sur l’expérience storefront. La valeur doit correspondre à l’adresse exacte du magasin pour passer la validation.</td>
<td>Global</td>
<td>Oui</td>
</tr>
<tr>
<td><strong>[!UICONTROL Longitude]</strong></br><code>Base Attribute: Longitude</code></td>
<td>Coordonnée longitudinale de l’emplacement du magasin marchand. Ces informations requises sont utilisées dans la recherche d’emplacement et l’emplacement du mappage sur l’expérience storefront. La valeur doit correspondre à l’adresse exacte du magasin pour passer la validation.</td>
<td>Global</td>
<td>Oui</td>
</tr>
<tr>
<td><strong>[!UICONTROL Use as Pickup Location]</br></strong><code>Base Attribute: is_pickup_location_active</code></td>
<td>Désignez la source comme emplacement de prélèvement de magasin disponible. Ce paramètre détermine si la source est synchronisée et affichée pour les visiteurs.</td>
<td>Global</td>
<td>Non</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship to Store]</strong></br> <code>Extension Attribute: [!DNL allow_ship_to_store]</code></td>
<td>Configurez les fonctionnalités de livraison à la boutique au niveau de la source. Pour plus d'informations, voir l'option [Configuration générale](enable-general.md), <strong>[!UICONTROL Enable Ship To Store]</strong>.</td>
<td>Global</td>
<td>Non</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship From Store]</strong></br><code>Extension Attribute: [!DNL use_as_shipping_source]</code></td>
 <td>Configurez les fonctionnalités d’expédition à partir du magasin au niveau de la source. Pour plus d'informations, voir l'option [Configuration générale](enable-general.md), [!UICONTROL Enable Ship From Store].</td>
<td>Global</td>
<td>Non</td>
</tr>
<tr>
<td>Global</td>
<td>Non</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship From Store]</strong><code></br><code>Extension Attribute: [!DNL use_as_shipping_source]</code></td>
<td>Configurez les fonctionnalités d’expédition à partir du magasin au niveau de la source. Pour plus d'informations, voir l'option [Configuration générale](enable-general.md), [!UICONTROL Enable Ship From Store].</td>
<td>Global</td>
<td>Non</td>
</tr>
</tbody>
</table>



| **Champ** | **Description** | **Portée** | **Obligatoire** |
|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Latitude]**</br>`Base Attribute: latitude` | Coordonnée latitude de l’emplacement du magasin marchand. Ces informations requises sont utilisées dans la recherche d’emplacement et l’emplacement du mappage sur l’expérience storefront. La valeur doit correspondre à l’adresse exacte du magasin pour passer la validation. | Global | Oui |
| **[!UICONTROL Longitude]**</br>`Base Attribute: Longitude` | Coordonnée longitudinale de l’emplacement du magasin marchand. Ces informations requises sont utilisées dans la recherche d’emplacement et l’emplacement du mappage sur l’expérience storefront. La valeur doit correspondre à l’adresse exacte du magasin pour passer la validation. | Global | Oui |
| **[!UICONTROL Use as Pickup Location]**</br>`Base Attribute:[!DNL is_pickup_location_active]` | Désignez la source comme emplacement de prélèvement de magasin disponible. Ce paramètre détermine si la source est synchronisée et affichée pour les visiteurs. | Global | Non |
| **[!UICONTROL Enable Ship to Store]**</br>`Extension Attribute: [!DNL allow_ship_to_store]` | Configurez les fonctionnalités de livraison à la boutique au niveau de la source. Pour plus d’informations, voir l’option [Configuration générale](enable-general.md), **[!UICONTROL Enable Ship To Store]**. | Global | Non |
| **[!UICONTROL Enable Ship From Store]**</br>`Extension Attribute: [!DNL use_as_shipping_source]` | Configurez les fonctionnalités d’expédition à partir du magasin au niveau de la source. Pour plus d’informations, voir l’option [Configuration générale](enable-general.md), [!UICONTROL Enable Ship From Store] | Global | Non |

{style="table-layout:auto"}

## Configuration de l’emplacement de prélèvement

| **Champ** | **Description** | **Portée** | **Obligatoire** |
|-----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Allow In-Store Pickup]**</br>`Extension Attribute: [!DNL store_pickup_enabled]` | L&#39;une des deux options de retrait. [!DNL In-Store Pickup] fait référence à la possibilité de permettre à un client d’accéder à l’emplacement de la boutique du commerçant pour récupérer sa commande. </br></br>Lorsqu’elle est activée, cette option peut être présentée au client lors du passage en caisse. </br></br>Cette option remplace également la configuration globale à [!UICONTROL Enable In-store Pickup] qui a été configurée sur le [!UICONTROL Delivery Method] pour [!UICONTROL In-store Pickup] | Global | Non |
| **Instructions de retrait en magasin**</br>`Extension Attribute: store_pickup_instructions` | Message personnalisable envoyé au client dans l’e-mail de notification **Commande prête pour retrait en magasin**. | Global | Non |
| **Autoriser côté trottoir**</br>`Extension Attribute: curbside_enabled` | L&#39;une des deux options de retrait. La livraison à domicile permet à un client de garer son véhicule à un endroit désigné à l&#39;emplacement du magasin marchand. Dans ce scénario, la commande est remise au client par un associé au magasin. </br></br>Lorsqu’elle est activée, cette option peut être présentée au client lors du passage en caisse. En outre, le client peut être invité à décrire son véhicule et sa place de stationnement pendant le processus d&#39;enregistrement. </br></br>Cette option remplace également la configuration globale pour **Activer la collecte en bordure de rue** qui a été configurée sur le **Méthode de diffusion** pour **la collecte en magasin** | Global | Non |
| **[!UICONTROL Curbside Instructions]**</br>`Extension Attribute: curbside_instructions` | Message personnalisable envoyé au client dans l’e-mail de notification [!UICONTROL Order Ready For Pickup in Store]. | Global | Non |
| **[!UICONTROL Estimated Pickup Lead Time]**</br>`Extension Attribute: pickup_lead_time` | Nombre de minutes nécessaires avant qu&#39;une commande ne soit reçue, prélevée et prête à être prélevée. </br></br>Ces informations sont utilisées pour afficher les temps estimés de retrait des commandes aux clients sur le site Web.</br></br> la définition de cette option remplace la configuration globale pour **Délai estimé de prélèvement** configurée pour le **Méthode de livraison** dans la configuration **Prélèvement en magasin**. | Global | Non |
| **[!UICONTROL Estimated Pickup Time Label]**</br>`Extension Attribute: pickup_time_label` | Libellé indiquant le nombre de minutes avant qu’une commande ne soit prête à être récupérée.</br></br> Lors de la personnalisation de ce libellé, vous pouvez utiliser le code %1 pour insérer votre **Délai estimé d&#39;enlèvement**.</br></br> la définition de cette option remplace la configuration globale pour les [!UICONTROL Estimated Pickup Time Label] configurées pour le [!UICONTROL Delivery Method] dans le [!UICONTROL In-store Pickup]. | Global | Non |

### **Heures d’ouverture**

| **Champ** | **Description** | **Portée** | **Obligatoire** |
|------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Location Timezone]**</br>`Extension Attribute: timezone` | Fuseau horaire de l’emplacement du magasin marchand. Pour chaque jour, définissez les heures d&#39;ouverture et de fermeture.</br></br>Ces paramètres sont utilisés pour optimiser les temps de ramassage estimés et pour la création de rapports du service d’exécution des commandes. | Global | Oui |
| **[!UICONTROL Opening Hours]**</br>`Internal Attribute: inventory_source_opening_hours_dynamic_rows` | Heures d’ouverture de l’emplacement de la boutique. </br></br>Ces informations peuvent être utilisées pour optimiser les temps de ramassage estimés et pour la création de rapports du service d’exécution. | Global | Oui |

### Configuration des options de l’interface d’expérience d’archivage



| **Champ** | **Description** | **Portée** | **Obligatoire** |
|---------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Use Parking Spots]**</br>`Extension Attribute: parking_spots_enabled` | Indiquez si l’emplacement de la boutique de commerce dispose de places de stationnement désignées pour le ramassage en bordure de rue. </br></br>Lorsque cette option est activée, vous pouvez configurer les places de parking disponibles. | Global | Non |
| **[!UICONTROL Is Parking Spot a Mandatory Field?]**</br>`Extension Attribute: parking_spot_mandatory` | Indiquez si l’identification de la place de stationnement est requise pour les clients lors de leur expérience d’achat.</br></br>Si cette option est activée, le client est invité à spécifier sa place de stationnement à son arrivée. Si cette option est désactivée, le client peut ignorer cette entrée. | Global | Non |
| **[!UICONTROL Parking Spots List]**</br> `Internal Attribute: inventory_source_parking_spot_dynamic_rows` | Les places de stationnement disponibles à cet emplacement de magasin marchand pour le ramassage en bordure de rue. Utilisez l’interface fournie pour nommer chaque zone.</br></br> Il n&#39;est pas nécessaire de nommer tous les emplacements de stationnement, seulement les endroits désignés pour le bord de la rue. Par exemple, vous pouvez avoir des rangées A à G de stationnement disponibles, mais seuls les 8 premiers points de la rangée A sont désignés pour le ramassage en bordure de la rue. Dans ce scénario, vous pouvez définir 8 emplacements ; par exemple : A1, A2, A3, etc. | Global | Non |
| **[!UICONTROL Allow "Other" Parking Spot Field]**</br>`Extension Attribute: custom_parking_spot_enabled` | Lorsqu&#39;il est activé, ce paramètre permet au client de décrire sa place de parking lors de l&#39;enregistrement. | Global | Non |
| **[!UICONTROL Use Car Color]**</br>`Extension Attribute: use_car_color` | Indiquez si vous souhaitez prendre en charge la collection de couleurs du véhicule du client lors de l&#39;enregistrement. </br></br> Les sélections disponibles pour [!UICONTROL Car Color] sont configurées dans les [paramètres système d’administration pour l’expérience d’archivage](check-in-experience-setup.md). | Global | Non |
| **[!UICONTROL Is Car Color a Mandatory Field?]**</br>`Extension Attribute: car_color_mandatory` | Indiquez si l&#39;identification de la couleur du véhicule est requise pour les clients lors de l&#39;enregistrement.</br></br>Si cette option est activée, le client est invité à spécifier la couleur de son véhicule à l&#39;arrivée. Si cette option est désactivée, le client peut ignorer cette entrée. | Global | Non |
| **[!UICONTROL Use Car Make]** </br>`Extension Attribute: use_car_make` | Indiquez si vous souhaitez prendre en charge la collecte de la marque du véhicule auprès du client lors de l’enregistrement.</br></br> Les sélections disponibles pour [!UICONTROL Car Make] sont configurées dans les [paramètres système d’administration pour l’expérience d’archivage](check-in-experience-setup.md). | Global | Non |
| **[!UICONTROL Is Car Make a Mandatory Field?]**</br>`Extension Attribute: car_make_mandatory` | Indiquez si l&#39;identification de la marque du véhicule est requise pour les clients lors de l&#39;enregistrement.</br></br>Si cette option est activée, le client est invité à indiquer la marque de son véhicule à l&#39;arrivée. Si cette option est désactivée, le client peut ignorer cette entrée. | Global | Non |
| **[!UICONTROL Use Additional Information]**</br> `Extension Attribute: use_additional_information` | Indiquez si vous souhaitez prendre en charge la collecte d&#39;informations supplémentaires auprès du client lors de l&#39;enregistrement. | Global | Non |
| **[!UICONTROL Is Additional Information a Mandatory Field?]**</br>`Extension Attribute: additional_information_mandatory` | Spécifiez si des informations supplémentaires sont requises pour les clients lors de l&#39;enregistrement. </br></br>Si cette option est activée, le client est invité à saisir des informations supplémentaires à son arrivée. Si cette option est désactivée, le client peut ignorer cette entrée. | Global | Non |
