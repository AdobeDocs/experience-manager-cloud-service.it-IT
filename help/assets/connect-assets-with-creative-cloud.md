---
title: Connettere AEM Assets a Creative Cloud
description: Scopri come configurare e collegare AEM Assets a Creative Cloud. Connettiti a una licenza Creative Cloud fornita a un’altra organizzazione IMS per utilizzare facilmente le più recenti integrazioni Creative Cloud in AEM Assets, inclusi Express e Creative Cloud Libraries.
exl-id: 880200fe-94b3-49de-802c-34283f7c71bc
feature: Collaboration
role: User
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 70%

---

# Connettere AEM Assets a Creative Cloud  {#cross-org-entitlements}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integrazione di AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Estensibilità interfaccia utente</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Abilita Dynamic Media Prime e Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Best practice per la ricerca</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Best practice per i metadati</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funzionalità OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentazione di AEM Assets per sviluppatori</b></a>
        </td>
    </tr>
</table>

Experience Manager Assets è in grado di connettersi a una licenza Creative Cloud fornita a un’altra organizzazione IMS per utilizzare facilmente le integrazioni Creative Cloud più recenti in AEM Assets, inclusi Express e Creative Cloud Libraries.

Se per i prodotti Creative Cloud e AEM Assets è stato eseguito il provisioning per organizzazioni IMS separate, è possibile connettersi a un’organizzazione Creative Cloud diversa per eseguire flussi di lavoro integrati tra le due soluzioni.

## Prerequisiti {#prerequisites}

* Diritti di amministratore su Experience Manager Assets

* Diritto attivo a Creative Cloud per lo stesso ID utente utilizzato in Creative Cloud e Experience Manager. I diritti a ID personali e federati con lo stesso indirizzo e-mail vengono trattati come ID utente diversi.

## Connettersi a una nuova organizzazione Creative Cloud {#connect-to-creative-cloud-org}

Per connettersi a una nuova organizzazione Creative Cloud, effettua le seguenti operazioni:

1. Accedi a **[!UICONTROL Impostazioni]** > **[!UICONTROL Creative Cloud]**.

1. Seleziona la nuova organizzazione Creative Cloud utilizzando l’elenco a discesa **[!UICONTROL Seleziona nuovo ID organizzazione Creative Cloud]**. Nell’elenco vengono visualizzate tutte le organizzazioni a cui hai accesso. Seleziona l’organizzazione con diritti attivi per Creative Cloud.

1. Fai clic su **[!UICONTROL Cambia organizzazione]** per passare alla nuova organizzazione.

   ![Diritti per più organizzazioni](assets/cross-org-entitlements.png)

## Limitazioni {#limitations}

* Puoi collegare AEM Assets a un’organizzazione Creative Cloud alla volta. La connessione a più organizzazioni Creative Cloud alla volta non è supportata.

* L’organizzazione Creative Cloud a cui ti connetti in AEM Assets è applicabile a tutti gli utenti all’interno dell’organizzazione.
