---
title: Condividi Assets in [!DNL the Content Hub]
description: Condividi Assets in [!DNL the Content Hub]
role: User
exl-id: 5284d229-1596-40bf-aa5f-af4b6500ebdf
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 6%

---

# Condividere risorse nell’hub di contenuti {#search-assets-as-a-link}

| [Best practice per la ricerca](/help/assets/search-best-practices.md) | [Best practice per i metadati](/help/assets/metadata-best-practices.md) | [Hub di contenuti](/help/assets/product-overview.md) | [Dynamic Media con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentazione di AEM Assets per sviluppatori](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![Condividi immagine banner risorse](assets/share-assets-banner.png)

>[!AVAILABILITY]
>
>La guida di Content Hub è ora disponibile in formato PDF. Scarica l’intera guida e utilizza Adobe Acrobat AI Assistant per rispondere alle tue domande.
>
>[!BADGE Guida di Content Hub PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

La condivisione delle risorse tramite un collegamento è un modo pratico per rendere le risorse disponibili agli utenti [!DNL the Content Hub]. Questa funzionalità consente agli utenti autorizzati di accedere e scaricare le risorse condivise con loro. Quando si scaricano risorse da un collegamento condiviso, [!DNL the Content Hub] utilizza un servizio asincrono che offre un download più rapido e ininterrotto.

## Prerequisiti {#prerequisites}

[Gli utenti di Content Hub](deploy-content-hub.md#onboard-content-hub-users) possono eseguire le azioni indicate in questo articolo.

## Condividere una singola risorsa {#share-a-single-asset}

Puoi condividere una singola risorsa eseguendo i seguenti passaggi:

1. Seleziona una risorsa e fai clic sull&#39;icona ![condividi](assets/share.svg) per condividerla.

   ![Condivisione di una singola risorsa](assets/sharing-single-asset.png)

1. Utilizza il campo **[!UICONTROL Scadenza]** per specificare una data di scadenza per il collegamento. Seleziona una delle opzioni disponibili, ad esempio 24 ore, 1 settimana, 30 giorni, 90 giorni, 1 anno o specifica una data personalizzata.

1. Fai clic su **[!UICONTROL Copia collegamento di condivisione]**. Puoi quindi condividere il collegamento copiato con il destinatario.

## Condividere più risorse {#share-multiple-assets}

[!DNL The Content Hub] consente di condividere più risorse tramite un collegamento condiviso. Esegui i passaggi seguenti:

1. Seleziona le risorse da condividere con il destinatario autorizzato. È possibile selezionare più risorse una alla volta oppure fare clic su **[!UICONTROL Seleziona tutto]** per selezionare tutte le risorse disponibili contemporaneamente. L&#39;opzione **[!UICONTROL Seleziona tutto]** viene visualizzata solo quando si seleziona almeno una risorsa.

1. Fai clic sull&#39;icona ![condividi](assets/share.svg).

   ![Condivisione di più risorse](assets/sharing-multiple-assets.png)

1. Nella sezione di anteprima puoi anche eliminare le risorse in base alle tue esigenze. Utilizza il campo **[!UICONTROL Scadenza]** per specificare una data di scadenza per il collegamento. Seleziona una delle opzioni disponibili, ad esempio 24 ore, 1 settimana, 30 giorni, 90 giorni, 1 anno o specifica una data personalizzata.

1. Fai clic su **[!UICONTROL Copia collegamento di condivisione]**. Puoi quindi condividere il collegamento copiato con il destinatario.

## Visualizzare in anteprima e condividere le risorse {#preview-assets}

Puoi visualizzare in anteprima per vedere come si presenterà una risorsa digitale che condividerai prima di condividerla con un destinatario del collegamento. Fai clic sulla risorsa necessaria per l’anteprima. [!DNL Content Hub] visualizza la [visualizzazione dettagliata per la risorsa](asset-properties-content-hub.md).

Fai clic sull&#39;icona ![condividi](assets/share.svg) per condividere una risorsa. Utilizza il campo **[!UICONTROL Scadenza]** per specificare una data di scadenza per il collegamento. Seleziona una delle opzioni disponibili, ad esempio 24 ore, 1 settimana, 30 giorni, 90 giorni, 1 anno o specifica una data personalizzata. Fai clic su **[!UICONTROL Copia collegamento di condivisione]**. Puoi quindi condividere il collegamento copiato con il destinatario.

![Anteprima risorse in Content Hub](assets/preview-assets-content-hub.png)

## Accedere alle risorse condivise {#access-shared-assets}

Dopo aver condiviso il collegamento per le risorse, i destinatari autorizzati possono fare clic su tale collegamento per visualizzare in anteprima o scaricare le risorse condivise in un browser web.

Per scaricare una risorsa, fai clic sul collegamento condiviso e sull’icona Scarica disponibile nella scheda delle risorse.  Puoi anche selezionare più risorse e fare clic su **[!UICONTROL Scarica]**. <!--You can either download original assets or Original+Renditions of an asset.--> [!DNL The Content Hub] scarica ciascuna risorsa una per una nel file system locale.

![Accedi ai collegamenti condivisi](assets/content-hub-access-shared-links.png)
