---
title: Utilizzo di frammenti di contenuto con Adobe Journey Optimizer
description: Scopri come i frammenti di contenuto possono essere integrati e utilizzati con Adobe Journey Optimizer.
feature: Content Fragments
role: User, Developer, Architect
solution: Experience Manager Sites
source-git-commit: 3204156f5af2e27786209a4fe10cc4c3696d3b8b
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 6%

---


# Frammenti di contenuto con Adobe Journey Optimizer {#content-fragments-with-journey-optimizer}

[Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/get-started) ti aiuta a fornire ai tuoi clienti esperienze connesse, contestuali e personalizzate. Integrando Adobe Experience Manager (AEM) as a Cloud Service con Adobe Journey Optimizer (AJO), puoi riutilizzare i contenuti AEM nei tuoi canali in uscita AJO, inclusi web, SMS ed e-mail.

Ad esempio:

* incorpora perfettamente i [frammenti di contenuto AEM](/help/sites-cloud/administering/content-fragments/overview.md) nel contenuto di [e-mail Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/get-started-email)
* visualizzare l’anteprima dell’esperienza AJO direttamente da AEM

La connessione tra Frammenti di contenuto e AJO semplifica il processo di accesso e utilizzo dei contenuti di AEM, consentendo la creazione di campagne e percorsi personalizzati e dinamici.

Per informazioni dettagliate, inizia con la documentazione di AJO:

* [Utilizzo di frammenti di contenuto in AJO](https://experienceleague.adobe.com/docs/journey-optimizer/using/integrations/aem-fragments.html#integrations)
* [Offerte di integrazione AJO con frammento di contenuto](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/managing-offers-in-the-offer-library/configure-offers/add-representations#urls)

## Ulteriori informazioni {#further-information}

Per ulteriori informazioni, consulta:

* L&#39;estensione [AJO External References](/help/sites-cloud/administering/content-fragments/extension-content-fragment-ajo-external-references.md)

<!-- Original draft text - relocated to the AJO doc set -->
<!--
## Configure AEM {#configure-aem}

For integration, and preparation for use, several steps need to be completed in AEM:

* [Create the AEM tag for AJO synchronization](#create-the-aem-tag-for-AJO-synchronization)
* [Create a Content Fragment Model](#create-a-content-fragment-model)

>[!IMPORTANT]
>
>You must also [configure AJO](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/integrations/aem-fragments).

### Create the AEM tag for AJO synchronization {#create-the-aem-tag-for-AJO-synchronization}

For synchronization, the integration of AEM and AJO uses [tags defined in AEM](/help/sites-cloud/administering/tags.md). The tag must:

* Have the specific format: ajo-enabled:{AJO-OrgId}/{AJO-SandboxName}
  * Be in the namespace: ajo-enable
  * Include the AJO organization name
  * Include the AJO sandbox name

For example: AJO Enabled: MyOrganization-AJO / MySandbox

To [create the tag](/help/sites-cloud/administering/tags.md#creating-new-tags):

1. [Create the namespace (if necessary)](/help/sites-cloud/administering/tags.md#creating-namespaces).
1. [Create the tag](/help/sites-cloud/administering/tags.md#creating-tags).
1. [Publish the tag](/help/sites-cloud/administering/tags.md#publishing-tags).

### Create a Content Fragment Model {#create-a-content-fragment-model}

[Content Fragment Models](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md) define the structure of your Content Fragment.

After creating your model, you must assign the [tag used for synchronization](#create-the-aem-tag-for-AJO-synchronization) to [your model](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#model-properties)

## Create and Publish your Content Fragment {#create-and-publish-your-content-fragment}

### Create your Content Fragment {#create-your-content-fragment}

[Create your Content Fragment](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment). You must select the **Auto Tag** option to automatically inherit all tags that you applied to the model (in particular, the [tag used for synchronization](#create-the-aem-tag-for-AJO-synchronization)).

### Author content for your Content Fragment {#author-content-for-your-content-fragment}

[Edit your Content Fragment](/help/sites-cloud/administering/content-fragments/managing.md#editing-the-content-of-your-fragment) to [author the content](/help/sites-cloud/administering/content-fragments/authoring.md) needed.

### Publish your Content Fragment

If required, [publish your Content Fragment](/help/sites-cloud/administering/content-fragments/managing.md#publishing) to make it available to AJO.

## Use your Content Fragment in Journey Optimizer {#use-your-content-fragment-in-journey-optimizer}

You can now [use your fragment in AJO](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/integrations/aem-fragments).

## Preview AJO experiences from AEM {#preview-ajo-experiences-from-aem}

To preview AJO experiences from AEM, you need to enable the UI extension:

* AJO External References 

The AJO External References extension functions by fetching references to Content Fragment from all AJO organizations and sandboxes associated with the AJO-enabled tags. The extension then shows details, dependent on whether the reference is a Campaign, a Journey or a Template.

>[!NOTE]
>
>For details on how to enable the extension, please see the document [Extension Manager in AEM Experience Manager.](https://developer.adobe.com/uix/docs/extension-manager/)

To use the extension:

1. Open the [Content Fragments Console](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console).

1. Navigate to your Content Fragment - the fragment that was created and used across various AJO channels.

1. Open your Content Fragment in the [editor](/help/sites-cloud/administering/content-fragments/managing.md#editing-the-content-of-your-fragment).

1. The AJO External References extension is available as a tab in the right panel. Select the tab to open the extension:

   ![AJO External References extension](/help/sites-cloud/administering/content-fragments/assets/cf-ajo-fragment-external-references-extension.png)

   Once a reference type is selected the extension displays the corresponding external references as a table with the columns: 

   * **Name**: the name of the reference where the Content fragment is used
   * **Preview** select this link to start the preview
   * **Status**: the status of the reference

1. You can select the **Reference Type** from the drop-down to switch between three reference types: 

   * **Campaign**
     * Displays a list of all Campaigns with links to the current Content Fragment. 
     * You can then [preview a selected Campaign](#preview-ajo-campaigns)
     * Default
   * **Journey**
     * Displays the latest Journey. 
     * You can then select and [preview a selected Journey](#preview-ajo-journeys).
   * **Template** 
     * Displays Templates related to the Content Fragment.
     * You can then select and [preview a selected Template](#preview-ajo-templates).

### Preview AJO Campaigns {#preview-ajo-campaigns}

For full information see:

* [Get started with AJO Campaigns](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
* [Preview and test your content](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/test/preview-test/preview-test)

### Preview AJO Journeys {#preview-ajo-journeys}

For full information see:

* [Get started with AJO Journeys](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey).
* [Preview and test your content](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/test/preview-test/preview-test)

### Preview AJO Template {#preview-ajo-templates}

For full information see:

* [Get started with AJO Content Templates](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates).
* [Preview and test your content](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/test/preview-test/preview-test)

## Limitations {#limitations}

Be aware that:

* Variations created by you are not considered. Only **Main** is used. 
* Any Content Fragment that appears in AJO from a connected AEM instance is considered approved and ready for use. There is currently no concept of [Content Fragment status](/help/sites-cloud/administering/content-fragments/managing.md#statuses-content-fragments) enforced within AJO.
-->
