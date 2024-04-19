---
title: Integrare AEM Assets remoto con AEM Sites
description: Scopri come configurare e collegare siti AEM con Approved AEM Assets in Creative Cloud.
role: null
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---


# Integrare AEM Assets remoto con AEM Sites  {#integrate-approved-assets}

Una gestione efficace delle risorse digitali è fondamentale per offrire esperienze di marchio coinvolgenti e coerenti su varie piattaforme online. Dynamic Medie con funzionalità OpenAPI migliora la gestione delle risorse digitali consentendo un’integrazione perfetta tra AEM Sites e AEM Assets remoto. Questa funzione innovativa consente di condividere e gestire facilmente diversi tipi di risorse digitali approvate in più ambienti AEM, semplificando i flussi di lavoro per autori di siti ed editor di contenuti.

Dynamic Medie con funzionalità OpenAPI consente agli autori dei siti di utilizzare risorse da DAM remoto direttamente nell’Editor pagina AEM e [Frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments.html), semplificando i processi di creazione e gestione dei contenuti.

Gli utenti possono collegare più istanze di AEM Sites, senza restrizioni sul numero massimo, a un’implementazione remota di DAM, un vantaggio notevole rispetto al [Risorse collegate](use-assets-across-connected-assets-instances.md) funzionalità.

![immagine](/help/assets/assets/connected-assets-rdam.png)

Dopo la configurazione iniziale, gli utenti possono creare pagine sull’istanza di AEM Sites e aggiungere risorse in base alle esigenze. Quando aggiungono delle risorse, possono selezionare le risorse memorizzate nel DAM locale oppure sfogliare e utilizzare le risorse disponibili nel DAM remoto.

Dynamic Medie con funzionalità OpenAPI offre diversi altri vantaggi, come l’accesso e l’utilizzo di risorse remote in Frammento di contenuto, il recupero dei metadati delle risorse remote e molto altro. Ulteriori informazioni sull&#39;altro [vantaggi di Dynamic Medie con funzionalità OpenAPI rispetto alle risorse collegate](/help/assets/new-dynamic-media-apis-faqs.md).

## Prima di iniziare

* Configura quanto segue [variabili di ambiente](/help/implementing/cloud-manager/environment-variables.md#add-variables) per AEM as a Cloud Service:

   * ASSET_DELIVERY_REPOSITORY_ID= &quot;delivery-pxxxxx-eyyyyy.adobeaemcloud.com&quot; <br>
     `pXXXX` fa riferimento all’ID del programma <br>
     `eYYYY` fa riferimento all’ID ambiente

   * ASSET_DELIVERY_IMS_CLIENT= [IMSClientId]

  o configurare il [Impostazioni OSGi](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/configuring/configuring-osgi.html) per AEM 6.5 nell’istanza AEM Sites, seguendo questi passaggi:

   1. Accedi alla console e fai clic su **[!UICONTROL OSGi] >** oppure utilizza l’URL diretto, ad esempio: `http://localhost:4502/system/console/configMgr`

   1. Aggiungi il **[!UICONTROL repositoryID]**= &quot;delivery-pxxxxx-eyyyyy.adobeaemcloud.com&quot; e **[!UICONTROL imsClient]**= [IMSClientId]
Ulteriori informazioni su [Autenticazione IMS](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/ims-config-and-admin-console.html).

* Accesso IMS per accedere all’istanza remota AEM as a Cloud Service di DAM.

* Attiva Dynamic Medie con funzionalità OpenAPI nel DAM remoto.

* Configura il componente Image v3 nell’istanza AEM Sites. Se il componente non è presente, scaricare e installare [pacchetto di contenuti](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.23.0).

## Accedere alle risorse da DAM remoto {#fetch-assets}

Dynamic Medie con funzionalità OpenAPI consente di accedere alle risorse disponibili nell’istanza DAM remota nell’Editor pagina AEM Sites locale e nel Frammento di contenuto AEM.

![immagine](/help/assets/assets/open-APIs.png)

### Accedere alle risorse remote nell’Editor pagina AEM

Per utilizzare le risorse remote nell’Editor pagina AEM nell’istanza AEM Sites, segui la procedura riportata di seguito. È possibile eseguire questa integrazione in AEM as a Cloud Service e AEM 6.5.

1. Vai a **[!UICONTROL Sites]** > _il tuo sito web_ in cui l&#39;AEM **[!UICONTROL Pagina]** è presente in cui è necessario aggiungere la risorsa remota.
1. Passare allo specifico AEM **[!UICONTROL Pagina]** all&#39;interno del sito Web sotto **[!UICONTROL Sites]** sezione in cui intendi aggiungere la risorsa remota.
1. Seleziona la pagina e fai clic su **[!UICONTROL Modifica (_e_)]**. L&#39;AEM **[!UICONTROL Editor pagina]** viene aperto.
1. Fai clic sul Contenitore di layout e aggiungi un **[!UICONTROL Immagine]** componente.
1. Fai clic su **[!UICONTROL Immagine]** e fai clic su ![icona impostazioni](/help/assets/assets/do-not-localize/settings-icon.svg) icona.
1. Deseleziona la **[!UICONTROL Eredita immagine in primo piano dalla pagina]** opzione.
1. Clic **[!UICONTROL Scegli]** e seleziona **[!UICONTROL Remoto]**.
   ![immagine](/help/assets/assets/uncheck-inherit-option.jpg)

   Viene richiesto di effettuare l&#39;accesso.
1. Seleziona la risorsa e fai clic su **[!UICONTROL Seleziona]**.
1. Aggiungi un testo alternativo e fai clic su **[!UICONTROL Fine]**.
   <br> La risorsa remota viene visualizzata nel componente immagine. Puoi anche verificare l’URL di consegna della risorsa quando viene caricato sulla pagina o utilizzando la scheda &quot;Anteprima&quot;. L’URL di consegna indica che si accede alla risorsa in modalità remota.

#### Video: accedere alle risorse remote nell’Editor pagina AEM

>[!VIDEO](https://video.tv.adobe.com/v/3427666)

### Accedere alle risorse remote nel frammento di contenuto AEM

Per utilizzare le risorse remote all’interno dei frammenti di contenuto AEM nell’istanza AEM Sites, segui i passaggi seguenti. È possibile eseguire questa integrazione in AEM 6.5 e non su AEM as a Cloud Service.

1. Vai a **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. Seleziona la cartella delle risorse in cui è presente il frammento di contenuto.
1. Seleziona il frammento di contenuto e fai clic su **[!UICONTROL Modifica (_e_)]**.

   >[!NOTE]
   >
   >Se non disponi di un modello per frammenti di contenuto AEM, potrebbe essere necessario [creane uno](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments-models.html?lang=en).

1. Fai clic su ![icona segno di spunta](/help/assets/assets/do-not-localize/checkmark-icon.svg) accanto al componente testo.
1. Seleziona **[!UICONTROL Remoto]** per recuperare la risorsa da DAM remoto. <br>
Puoi scegliere **[!UICONTROL Locale]** o **[!UICONTROL Remoto]** Archivio DAM in base alle tue esigenze.

   ![immagine](/help/assets/assets/cf-pick.jpg)
Viene richiesto di effettuare l&#39;accesso.
1. Scegli la risorsa e fai clic su **[!UICONTROL Seleziona]**.
   <br> L’URL della risorsa remota viene visualizzato nel componente testo.

#### Video: accedere alle risorse remote nel frammento di contenuto AEM

>[!VIDEO](https://video.tv.adobe.com/v/3427667)
