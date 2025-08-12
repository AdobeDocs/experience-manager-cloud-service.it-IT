---
title: Visualizzare in anteprima le risorse prima di utilizzarle nelle pagine AEM Sites
description: Dynamic Media con funzionalità OpenAPI consente di visualizzare in anteprima le risorse sulle pagine di anteprima di Adobe Experience Manager (AEM) Sites. Questa anteprima consente a te e alle parti interessate di rivedere e convalidare gli aggiornamenti alle risorse prima di pubblicarle (con le risorse aggiornate) per l’utilizzo pubblico.
role: Admin, User
exl-id: 6f071ca9-0f84-45fc-a6b3-047cca9d5e65
source-git-commit: 3f3e091d09b94418fc2cda0bd3b3ce950555b7a9
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 0%

---


# Visualizzare in anteprima le risorse prima di utilizzarle nelle pagine AEM Sites {#asset-preview-using-Dynamic-Media-with-OpenAPI-capabilities}

[!DNL Dynamic Media with OpenAPI capabilities] consente di visualizzare in anteprima le risorse disponibili nelle pagine dell&#39;autore di [!DNL Adobe Experience Manager (AEM) Sites] prima di renderle pubbliche. L’anteprima della risorsa è disponibile nel livello di authoring e anteprima del sito.

Per [visualizzare in anteprima le risorse nelle pagine di anteprima di AEM Sites](#asset-preview-on-sites-pages-using-Dynamic-Media-with-OpenAPI-capabilities), aggiorna le pagine di authoring del sito aggiungendo le risorse da visualizzare in anteprima o sostituendo quelle esistenti disponibili nella pagina dei siti attivi. Pubblica le pagine di authoring aggiornate nel livello di anteprima per generare un URL di anteprima.

Condividi la pagina di anteprima con le parti interessate per raccogliere feedback sulla qualità visiva e sull’allineamento contestuale delle risorse aggiornate. Perfeziona le risorse in base al feedback. Crea e gestisci più versioni della risorsa durante il ciclo di revisione.

Una volta finalizzate le risorse per l’uso pubblico, aggiornatele nelle pagine di authoring e pubblicatele nel livello di pubblicazione per l’accesso pubblico.

## Prima di iniziare{#prerequisites-for-previewing-assets-using-Dynamic-Media-with-OpenAPI-capabilities}

Assicurati di disporre di:

* Accesso a [!DNL AEM Assets as a Cloud Service].
* Autorizzazione per modificare la proprietà Status delle risorse.
* [È stato aggiunto il valore [!UICONTROL Anteprima] alla proprietà dei metadati [!UICONTROL  Status] disponibile nella scheda [!UICONTROL Basic]](/help/assets/metadata-assets-view.md#edit-metadata-forms) del modulo dei metadati applicato alla cartella contenente le risorse da visualizzare in anteprima.
  ![Aggiungi opzione anteprima](/help/assets/assets/metedata-form-preview.png)
* Chiave per generare il token di anteprima. [Contatta il supporto Adobe](https://helpx.adobe.com/in/contact.html) e richiedi la chiave.

## Anteprima delle risorse nella pagina di anteprima dei siti {#asset-preview-on-sites-pages-using-Dynamic-Media-with-OpenAPI-capabilities}

Puoi visualizzare in anteprima le nuove risorse o le risorse già approvate. Le risorse approvate vengono visualizzate solo sulle pagine live di Sites.

Eseguire la procedura seguente per impostare lo stato della risorsa da visualizzare in anteprima in [!DNL Assets View], quindi pubblicare la pagina di authoring Sites nel livello di anteprima per generare un URL di anteprima della pagina:

1. Impostare lo stato della risorsa su **[!UICONTROL Anteprima]** eseguendo la procedura seguente:

   1. In [!DNL Assets View], seleziona **[!UICONTROL Assets]** e passa alla cartella.
   1. Seleziona la risorsa per l’anteprima.
   1. Fare clic su **[!UICONTROL Dettagli]**.
   1. Nel [!UICONTROL pannello informazioni], imposta **[!UICONTROL Stato]** su **[!UICONTROL Anteprima]**, quindi fai clic su **[!UICONTROL Salva]**.
      ![Anteprima](/help/assets/assets/preview-boat-at-bay.png)

1. Passa alla pagina di authoring di Sites. Esegui i passaggi descritti in [Accedi alle risorse remote nella sezione Editor pagine di AEM](/help/assets/integrate-remote-approved-assets-with-sites.md#access-remote-assets-in-aem-page-editor) per utilizzare il pannello Selettore risorse per selezionare la risorsa impostata di recente su Anteprima (stato).

   >[!NOTE]
   >
   > In Asset Selector (Selettore risorse) vengono visualizzate le risorse il cui stato di aggiornamento più recente è impostato su Approvato o Anteprima.

1. Pubblica la pagina nel livello di anteprima utilizzando l&#39;opzione **[!UICONTROL Gestisci pubblicazione]**. Esegui i passaggi della sezione [Pubblicazione del contenuto in anteprima](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/sites-console/previewing-content) per pubblicare la pagina nel livello di anteprima. Dopo la pubblicazione, genera un URL di anteprima della pagina. Nella pagina Anteprima vengono visualizzate le risorse (con gli aggiornamenti di stato più recenti) nella pagina Sites.

Condividi questo URL di anteprima con le parti interessate per la revisione e il feedback. Assicurati che le parti interessate abbiano accesso alla pagina di anteprima. Per informazioni su come fornire l&#39;accesso alle pagine di anteprima, vedere [Accedere al servizio di anteprima](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments#access-preview-service).

>[!NOTE]
>
>Per impostazione predefinita, il componente di base [Immagine V3](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/wcm-components/image#version-and-compatibility) supporta la versione di anteprima delle risorse. Quando selezioni una versione di anteprima di una risorsa (risorsa con stato di anteprima) utilizzando il pannello [Selettore risorse](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/asset-selector-upload), il componente Immagine V3 la riproduce automaticamente nel livello di anteprima (una versione di anteprima nella pagina di authoring di Sites).

Dopo aver finalizzato la versione della risorsa, [pubblica le pagine nel livello di pubblicazione](#publish-your-pages-to-publish-tier) per l&#39;utilizzo pubblico.

## Pubblicare le pagine con risorse approvate per uso pubblico{#publish-your-pages-to-publish-tier}

Dopo aver finalizzato la versione della risorsa per uso pubblico, imposta lo stato della risorsa su **[!UICONTROL Approvato]**. Quindi pubblica le pagine nel livello di pubblicazione. Per pubblicare le pagine, effettua le seguenti operazioni:

1. Segui il passaggio 1 della sezione [Anteprima risorse nella pagina di anteprima dei tuoi siti](#asset-preview-on-sites-pages-using-Dynamic-Media-with-OpenAPI-capabilities) per cambiare lo stato della risorsa in **[!UICONTROL Approvato]**.
1. Passa alla pagina di authoring Sites e pubblicala in [!DNL Publish tier]. Pubblicare le pagine eseguendo i passaggi descritti in [Pubblicazione dalla sezione Editor pagine](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/page-editor/publishing#publishing-from-the-page-editor).
In alternativa, segui i passaggi descritti in [Pubblicazione di pagine dalla console Sites](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/sites-console/publishing-pages#publishing-from-the-sites-console) per pubblicare la pagina dalla console del tuo sito.

   >[!NOTE]
   >
   > Solo le risorse approvate possono essere consegnate sul livello di pubblicazione. Approva le risorse prima di pubblicare la pagina sul livello di pubblicazione per uso pubblico.

   ![La pagina è stata pubblicata](/help/assets/assets/the-page-has-been-publushed.png)
Dopo la pubblicazione, viene visualizzato un messaggio di conferma **[!UICONTROL La pagina è stata pubblicata]**. Passa alla pagina pubblicata sul livello di pubblicazione per verificare che gli aggiornamenti siano live e che il contenuto venga visualizzato come previsto.
