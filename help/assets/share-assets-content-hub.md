---
title: Condividi Assets in [!DNL the Content Hub]
description: Condividi Assets in [!DNL the Content Hub]
role: User
exl-id: 5284d229-1596-40bf-aa5f-af4b6500ebdf
source-git-commit: 0e66b355d09e2fd2c4c8a5ddacc9b2d033b41bf2
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 17%

---

# Condividere risorse in Content Hub {#search-assets-as-a-link}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integrazione di AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Estensibilità dell’interfaccia utente</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Abilitare Dynamic Media Prime e Ultimate</b></a>
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

![Condividi immagine banner risorse](assets/share-assets-banner.png)

>[!AVAILABILITY]
>
>La guida di Content Hub è ora disponibile in formato PDF. Scarica l’intera guida e utilizza l’Assistente IA di Adobe Acrobat per rispondere alle tue domande.
>
>[!BADGE Guida di Content Hub - PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Crea un collegamento alle risorse selezionate per condividerle facilmente con altri utenti. In qualità di utente [!DNL Content Hub] autorizzato, seleziona una o più risorse disponibili nell&#39;ambiente [!DNL Content Hub], genera un collegamento e invialo ad altri utenti pubblici o privati.

## Prerequisiti {#prerequisites}

[Gli utenti di Content Hub](deploy-content-hub.md#onboard-content-hub-users) possono creare un collegamento alle risorse selezionate e condividerlo con altri utenti.

## Condividere le risorse {#share-assets}

Per condividere una o più risorse con utenti privati o pubblici, effettua le seguenti operazioni:
1. Passa alla home page di [!DNL Content Hub], seleziona una o più risorse e fai clic su ![condividi](/help/assets/assets/share.svg) **[!UICONTROL Condividi]** per visualizzare una singola risorsa selezionata o un elenco di più risorse selezionate nella finestra di dialogo **[!UICONTROL Condividi risorse]**.
Puoi anche selezionare e condividere le risorse disponibili in ![raccolte](/help/assets/assets/Smock_Collection_18_N.svg) **[!UICONTROL raccolte]**.
1. Visualizza una risorsa o controlla l&#39;elenco delle risorse disponibili nella finestra di dialogo **[!UICONTROL Condividi risorse]**. Fai clic su ![deseleziona](/help/assets/assets/Close.svg) accanto a una risorsa per deselezionarla dall&#39;elenco.
1. Seleziona un **[!UICONTROL periodo di scadenza]** e fai clic su **[!UICONTROL Genera collegamento privato]** per generare un collegamento da condividere con utenti privati. Gli utenti privati accedono al proprio ambiente [!DNL Content Hub] per accedere alla pagina delle risorse condivise.
   ![collegamento pubblico e privato](/help/assets/assets/private-and-public-link.png)
Attiva l&#39;interruttore **[!UICONTROL Collegamento pubblico]**, seleziona un **[!UICONTROL periodo di scadenza]** e fai clic su **[!UICONTROL Genera collegamento pubblico]** per generare un collegamento da condividere con gli utenti pubblici. Gli utenti pubblici, come ospiti, accedono alla pagina delle risorse condivise senza accedere a [!DNL Content Hub].
   ![collegamento pubblico e privato](/help/assets/assets/public-and-private-link.png)

   >[!NOTE]
   > 
   > [Abilita la condivisione di collegamenti pubblici dalla pagina di configurazione](/help/assets/configure-content-hub-ui-options.md#enable-public-link-sharing) per visualizzare **[!UICONTROL Collegamento pubblico]** nella finestra di dialogo **[!UICONTROL Condividi risorse]**.

## Condividere una risorsa dalla sua pagina di anteprima {#share-asset-from-preview-page}

Per condividere una risorsa durante l’anteprima, esegui la procedura seguente:

1. Passa alla home page di [!DNL Content Hub] e fai clic sulla miniatura della risorsa per visualizzare l&#39;anteprima della risorsa e le opzioni di menu nel riquadro a destra della finestra di dialogo.
1. Seleziona ![condividi](/help/assets/assets/share.svg) per visualizzare il pannello **[!UICONTROL Condividi]**.
   ![condividi risorsa durante l&#39;anteprima](/help/assets/assets/share-assets-from-share-panel.png)
1. Segui il passaggio 3 della sezione [condividi risorse](#share-assets) per generare e condividere il collegamento alle risorse (privato o pubblico) da questo pannello **[!UICONTROL Condividi]**.

## Accedere alle risorse condivise {#access-shared-assets}

Accedi alla pagina delle risorse condivise tramite il collegamento ed effettua le seguenti operazioni:

* Seleziona una o più risorse e fai clic su ![scarica](/help/assets/assets/download-icon.svg) **[!UICONTROL Scarica]** per selezionare le rappresentazioni **[!UICONTROL Originale]**, **[!UICONTROL Statico]** o entrambe dalle opzioni di download disponibili.
  ![](/help/assets/assets/download-shared-assets.png)
* Fai clic sulla miniatura della risorsa per visualizzarne i metadati.
* Nella pagina delle risorse condivise ([a cui si accede tramite un collegamento privato](#share-assets)) fai clic sulla miniatura di una risorsa e seleziona ![scarica](/help/assets/assets/download-icon.svg) per selezionare e visualizzare le rappresentazioni dinamiche disponibili della risorsa nel pannello **[!UICONTROL Scarica]** prima di selezionarle e scaricarle.
  ![](/help/assets/assets/download-renditions-shared-assets-page.png)





