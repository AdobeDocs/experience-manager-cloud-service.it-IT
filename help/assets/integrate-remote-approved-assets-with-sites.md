---
title: Integrare AEM Assets remoto con AEM Sites
description: Scopri come configurare e collegare siti AEM con Approved AEM Assets in Creative Cloud.
source-git-commit: f6c0e8e5c1d7391011ccad5aa2bad4a6ab7d10c3
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 2%

---


# Integrare AEM Assets remoto con AEM Sites  {#integrate-approved-assets}

Una gestione efficace delle risorse digitali è fondamentale per offrire esperienze di marchio coinvolgenti e coerenti su varie piattaforme online. Dynamic Medie con funzionalità OpenAPI migliora la gestione delle risorse digitali consentendo un’integrazione perfetta tra AEM Sites e AEM Assets as a Cloud Service. Questa funzione innovativa consente di condividere e gestire facilmente diversi tipi di risorse digitali approvate in più ambienti AEM, semplificando i flussi di lavoro per autori di siti ed editor di contenuti.

Dynamic Medie con funzionalità OpenAPI consente agli autori dei siti di utilizzare le risorse di DAM remoto direttamente nell&#39;Editor pagina AEM e nel [Frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments.html), semplificando i processi di creazione e gestione dei contenuti.

Gli utenti possono connettere più istanze di AEM Sites, senza restrizioni sul numero massimo, a una distribuzione DAM remota, un vantaggio notevole rispetto alla funzionalità [Connected Assets](use-assets-across-connected-assets-instances.md).

![immagine](/help/assets/assets/connected-assets-rdam.png)

Dopo la configurazione iniziale, gli utenti possono creare pagine sull’istanza di AEM Sites e aggiungere risorse in base alle esigenze. Quando aggiungono delle risorse, possono selezionare le risorse memorizzate nel DAM locale oppure sfogliare e utilizzare le risorse disponibili nel DAM remoto.

Dynamic Medie con funzionalità OpenAPI offre diversi altri vantaggi, come l’accesso e l’utilizzo di risorse remote in Frammento di contenuto, il recupero dei metadati delle risorse remote e molto altro. Ulteriori informazioni sugli altri [vantaggi di Dynamic Medie con funzionalità OpenAPI rispetto a Connected Assets](/help/assets/dynamic-media-open-apis-faqs.md).

## Prima di iniziare {#pre-requisits-sites-integration}

* Configura le [variabili di ambiente](/help/implementing/cloud-manager/environment-variables.md#add-variables) seguenti per AEM as a Cloud Service:

   * ASSET_DELIVERY_REPOSITORY_ID= &quot;delivery-pxxxxx-eyyyyy.adobeaemcloud.com&quot; <br>
     `pXXXX` fa riferimento all&#39;ID programma <br>
     `eYYYY` fa riferimento all&#39;ID ambiente

   * ASSET_DELIVERY_IMS_CLIENT= [IMSClientId]

  o configura le [impostazioni OSGi](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/configuring/configuring-osgi.html) per AEM 6.5 nell&#39;istanza AEM Sites seguendo la procedura seguente:

   1. Accedi alla console e fai clic su **[!UICONTROL OSGi] >** o
utilizzare l&#39;URL diretto, ad esempio: `http://localhost:4502/system/console/configMgr`

   1. Aggiungi **[!UICONTROL repositoryID]**= &quot;delivery-pxxxxx-eyyyyy.adobeaemcloud.com&quot; e **[!UICONTROL imsClient]**= [IMSClientId]
Ulteriori informazioni sull&#39;[autenticazione IMS](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/ims-config-and-admin-console.html).

* Accesso IMS per accedere all’istanza remota di DAM AEM as a Cloud Service.

* Attiva Dynamic Medie con funzionalità OpenAPI nel DAM remoto.

* Configura il componente Image v3 nell’istanza AEM Sites. Se il componente non è presente, scaricare e installare il [pacchetto di contenuti](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.23.0).

## Accedere alle risorse da DAM remoto {#fetch-assets}

Dynamic Medie con funzionalità OpenAPI consente di accedere alle risorse disponibili nell’istanza DAM remota nell’Editor pagina AEM Sites locale e nel Frammento di contenuto AEM.

![immagine](/help/assets/assets/open-APIs.png)

### Accedere alle risorse remote nell’Editor pagina AEM {#access-assets-page-editor}

Per utilizzare le risorse remote nell’Editor pagina AEM nell’istanza AEM Sites, segui la procedura riportata di seguito. Puoi eseguire questa integrazione in AEM as a Cloud Service e AEM 6.5.

1. Vai a **[!UICONTROL Sites]** > _il tuo sito Web_ in cui è presente la **[!UICONTROL pagina]** dell&#39;AEM in cui devi aggiungere la risorsa remota.
1. Passa alla **[!UICONTROL pagina]** specifica dell&#39;AEM nel tuo sito Web nella sezione **[!UICONTROL Sites]** in cui intendi aggiungere la risorsa remota.
1. Selezionare la pagina e fare clic su **[!UICONTROL Modifica (_e_)]**. Verrà aperto l&#39;**[!UICONTROL Editor pagine]** dell&#39;AEM.
1. Fai clic sul Contenitore di layout e aggiungi un componente **[!UICONTROL Immagine]**.
1. Fare clic sul componente **[!UICONTROL Immagine]** e sull&#39;icona ![Impostazioni](/help/assets/assets/do-not-localize/settings-icon.svg).
1. Deseleziona l&#39;opzione **[!UICONTROL Eredita immagine in primo piano dalla pagina]**.
1. Fai clic su **[!UICONTROL Scegli]** e seleziona **[!UICONTROL Remoto]**.
   ![immagine](/help/assets/assets/uncheck-inherit-option.jpg)

   Viene richiesto di effettuare l&#39;accesso.
1. Seleziona la risorsa e fai clic su **[!UICONTROL Seleziona]**.
1. Aggiungi un testo alternativo e fai clic su **[!UICONTROL Fine]**.
   <br> La risorsa remota viene visualizzata nel componente immagine. Puoi anche verificare l’URL di consegna della risorsa quando viene caricato sulla pagina o utilizzando la scheda &quot;Anteprima&quot;. L’URL di consegna indica che si accede alla risorsa in modalità remota.

Nell’editor di pagine AEM puoi accedere alle risorse remote solo per il componente core Immagine v3 e per il componente core Teaser v2. Per altri componenti, compresi quelli personalizzati, sono necessarie personalizzazioni per integrare Asset Selector con tali componenti.

#### Video: accedere alle risorse remote nell’Editor pagina AEM

>[!VIDEO](https://video.tv.adobe.com/v/3427666)

### Accedere alle risorse remote nel frammento di contenuto AEM {#access-assets-content-fragment}

Per utilizzare le risorse remote all’interno dei frammenti di contenuto AEM nell’istanza AEM Sites, segui i passaggi seguenti. Puoi eseguire questa integrazione in AEM 6.5 e non su AEM as a Cloud Service.

1. Vai a **[!UICONTROL Assets]** > **[!UICONTROL File]**.
1. Seleziona la cartella delle risorse in cui è presente il frammento di contenuto.
1. Selezionare il frammento di contenuto e fare clic su **[!UICONTROL Modifica (_e_)]**.

   >[!NOTE]
   >
   >Se non disponi di un modello per frammenti di contenuto AEM, potresti dover [crearne uno](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments-models.html?lang=en).

1. Fai clic sull&#39;icona ![segno di spunta](/help/assets/assets/do-not-localize/checkmark-icon.svg) accanto al componente testo.
1. Seleziona **[!UICONTROL Remoto]** per recuperare la risorsa dal DAM remoto. <br>
Puoi scegliere **[!UICONTROL Local]** o **[!UICONTROL Remote]** DAM repository in base alle tue esigenze.

   ![immagine](/help/assets/assets/cf-pick.jpg)
Viene richiesto di effettuare l&#39;accesso.
1. Scegli la risorsa e fai clic su **[!UICONTROL Seleziona]**.
   <br> L&#39;URL della risorsa remota viene visualizzato nel componente testo.

#### Video: accedere alle risorse remote nel frammento di contenuto AEM

>[!VIDEO](https://video.tv.adobe.com/v/3427667)

### Accedere alle risorse remote in Edge Delivery Services {#access-assets-eds}

Puoi anche accedere alle risorse remote in Edge Delivery Services. Per ulteriori informazioni, consulta [Utilizzo delle risorse da Assets as a Cloud Service distribuite tramite Dynamic Medie con funzionalità OpenAPI](https://www.aem.live/docs/aem-assets-sidekick-plugin#utilizing-assets-from-assets-cloud-services-delivered-via-dynamic-media-with-openapi).
