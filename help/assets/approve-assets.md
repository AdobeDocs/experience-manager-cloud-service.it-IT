---
title: Approvare le risorse in Experience Manager
description: Scopri come approvare le risorse in [!DNL Experience Manager].
role: User
exl-id: fe61a0f1-94d3-409a-acb9-195979668c25
source-git-commit: d542df9ae943d03a56b5d85b1bd189f81c35fe28
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 4%

---

# Approva risorse in [!DNL Experience Manager]

| [Best practice per la ricerca](/help/assets/search-best-practices.md) | [Best practice per i metadati](/help/assets/metadata-best-practices.md) | [Hub di contenuti](/help/assets/product-overview.md) | [Dynamic Media con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentazione di AEM Assets per sviluppatori](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

I Brand Manager e gli addetti al marketing mantengono un controllo rigoroso sulle risorse del brand. È disponibile per l’uso solo la versione approvata e più recente della risorsa, che garantisce la coerenza del brand su tutti i canali e le applicazioni.

Puoi approvare le risorse in AEM Assets per semplificare la gestione delle risorse, garantendo un processo controllato ed efficiente per la loro gestione.

## Prima di iniziare {#pre-requisites}

Per modificare la proprietà **[!UICONTROL Verifica stato]** di una risorsa è necessario disporre dell&#39;accesso ad AEM Assets as a Cloud Service.

## Configurazione

Prima di approvare una risorsa, devi effettuare un aggiornamento una tantum dello schema di metadati applicabile nella visualizzazione Amministratore. Puoi saltare questa configurazione per la vista Assets. Per configurare lo schema metadati, effettua le seguenti operazioni:

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Schemi metadati]**.
1. Seleziona lo schema metadati applicabile e fai clic su **[!UICONTROL Modifica]**. <br>Viene aperto l&#39;Editor modulo schema metadati **[!UICONTROL 2} con la scheda**[!UICONTROL  Base ]**evidenziata.]**
1. Scorri verso il basso e fai clic su **[!UICONTROL Verifica stato]**.
1. Fai clic sulla scheda **[!UICONTROL Regole]** nel pannello laterale destro.
1. Deseleziona **[!UICONTROL Disattiva modifica]** e fai clic su **[!UICONTROL Salva]**.
Se devi visualizzare la proprietà a cui è mappato il campo **[!UICONTROL Stato revisione]**, passa alla scheda **[!UICONTROL Impostazioni]** e visualizza il valore `./jcr:content/metadata/dam:status` nel campo **[!UICONTROL Mappa sulla proprietà]**.

>[!NOTE]
>
>Se le risorse o le cartelle hanno uno schema predefinito diverso, assicurati di effettuare questo aggiornamento in quello specifico schema.

## Approvare risorse {#approve-assets}

Per approvare le risorse in [!DNL Experience Manager Admin view], eseguire la procedura seguente:

1. Seleziona le risorse e fai clic su **[!UICONTROL Proprietà]** nel riquadro superiore.
1. Nella scheda **[!UICONTROL Base]**, scorri verso il basso fino a **[!UICONTROL Stato revisione]**.
1. Cambia lo stato di revisione in **[!UICONTROL Approvato]**.
   ![immagine](/help/assets/assets/approve-old-ui.png)
1. Fai clic su **[!UICONTROL Salva e chiudi]**.

   >[!VIDEO](https://video.tv.adobe.com/v/3427430)

   Allo stesso modo, puoi approvare le risorse utilizzando la [nuova visualizzazione Assets](/help/assets/manage-organize-assets-view.md).

## Approva in blocco le risorse {#bulk-approve-assets}

Semplifica il flusso di lavoro approvando rapidamente più risorse contemporaneamente. Puoi approvare in blocco le risorse per accelerare il processo di approvazione, risparmiando tempo e migliorando la produttività.
<br>Segui questi passaggi per approvare risorse in blocco in [!DNL Experience Manager Admin view]:

1. Crea una cartella nell’ambiente di authoring (https://author-pXXX-eYYY.adobeaemcloud.com). Sostituisci _XXX_ con il tuo ID programma e _YYY_ con l&#39;ID ambiente dell&#39;Experience Manager.
1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Profili metadati]**.
1. Fai clic su **[!UICONTROL Crea]** in alto a destra della pagina.
1. Aggiungi un titolo profilo e fai clic su **[!UICONTROL Crea]**. Il profilo metadati è stato creato correttamente.
1. Selezionare il profilo metadati appena creato e fare clic su **[!UICONTROL Modifica _(e)_]**. <br>Viene aperto il modulo **[!UICONTROL Modifica profilo metadati]**con la scheda **[!UICONTROL Base]**evidenziata.
1. Trascina e rilascia un **[!UICONTROL Campo di testo a riga singola]** dalla sezione **[!UICONTROL Genera modulo]** a destra alla sezione Metadati nel modulo.
1. Fai clic sul campo appena aggiunto, quindi esegui i seguenti aggiornamenti nel pannello **[!UICONTROL Impostazioni]**:
   1. Cambia l&#39;etichetta **[!UICONTROL Campo]** in _Assets approvato_.
   1. Aggiorna **[!UICONTROL Mappa sulla proprietà]** in _./jcr:content/metadata/dam:status_.
   1. Cambia il valore predefinito in _approvato_.

1. Fai clic su **[!UICONTROL Salva]**.
1. Nella pagina **[!UICONTROL Profili metadati]**, seleziona il profilo metadati appena creato.
1. Fai clic su **[!UICONTROL Applica profilo metadati a cartelle]** nella barra delle azioni superiore.
1. Seleziona le cartelle da approvare e fai clic su **[!UICONTROL Applica]**.
   <br> L&#39;autorizzazione per l&#39;intera cartella è impostata per l&#39;approvazione e tutte le risorse caricate in questa cartella vengono approvate automaticamente.

   >[!VIDEO](https://video.tv.adobe.com/v/3427431)

>[!NOTE]
> 
>Questo approccio approva le nuove risorse create nella cartella. Per le risorse esistenti nella cartella, devi selezionarle e approvarle manualmente. <br> In alternativa, è possibile utilizzare l&#39;opzione **[!UICONTROL Rielabora]** per applicare le modifiche dal profilo metadati alle risorse precedenti.

Allo stesso modo, per approvare in blocco le risorse all’interno di una cartella nella vista Assets:

1. Seleziona le risorse e fai clic su **[!UICONTROL Modifica in blocco metadati]**.

1. Seleziona **[!UICONTROL Approvato]** nel campo **[!UICONTROL Stato]** disponibile nella sezione [!UICONTROL Proprietà] nel riquadro di destra.

1. Fai clic su **[!UICONTROL Salva]**.

## Copiare l’URL di consegna per le risorse approvate {#copy-delivery-url-approved-assets}

L&#39;URL di consegna per tutte le risorse approvate nell&#39;archivio è disponibile se nell&#39;istanza di AEM as a Cloud Service è abilitato [!UICONTROL Dynamic Media con funzionalità OpenAPI].

Per copiare l’URL di consegna di una risorsa approvata all’interno dell’archivio:

1. Seleziona la risorsa e fai clic su **[!UICONTROL Dettagli]**.

1. Fai clic sull’icona Dynamic Media disponibile nel riquadro a destra.

1. Selezionare **[!UICONTROL Dynamic Media con OpenAPI]** disponibile nel pannello **[!UICONTROL Dynamic Media]**.

1. Fai clic su **[!UICONTROL Copia URL]** per copiare l&#39;URL di consegna della risorsa.
   ![rappresentazioni dinamiche](/help/assets/assets/dm-with-openapi-non-image-assets.png)

   >[!NOTE]
   >
   >L’opzione per copiare l’URL di consegna per le risorse approvate è disponibile nella vista Assets.

Per informazioni sulle altre rappresentazioni visualizzate nel pannello Dynamic Media, consulta [Visualizzare e scaricare le rappresentazioni di Dynamic Media](/help/assets/renditions.md#view-download-dm-renditions).
