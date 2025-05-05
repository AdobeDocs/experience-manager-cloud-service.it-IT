---
title: Integrare AEM Assets remoto con AEM Sites
description: Scopri come configurare e collegare i siti di AEM con Approved AEM Assets.
exl-id: 382e6166-3ad9-4d8f-be5c-55a7694508fa
source-git-commit: 2ec0b4125aa0990b6e022350a1f861fe394e6b1f
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 16%

---

# Integrare AEM Assets remoto con AEM Sites  {#integrate-approved-assets}

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

>[!AVAILABILITY]
>
>La guida di Dynamic Media con funzionalità OpenAPI è ora disponibile in formato PDF. Scarica l’intera guida e utilizza l’Assistente IA di Adobe Acrobat per rispondere alle tue domande.
>
>[!BADGE Guida di Dynamic Media con funzionalità OpenAPI - PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

Una gestione efficace delle risorse digitali è fondamentale per offrire esperienze di marchio coinvolgenti e coerenti su varie piattaforme online. Dynamic Media con funzionalità OpenAPI migliora la gestione delle risorse digitali consentendo un’integrazione perfetta tra AEM Sites e AEM Assets as a Cloud Service. Questa funzione innovativa consente di condividere e gestire facilmente diversi tipi di risorse digitali approvate tra più ambienti AEM, semplificando i flussi di lavoro per autori di siti ed editor di contenuti.

Dynamic Media con funzionalità OpenAPI consente agli autori dei siti di utilizzare le risorse di DAM remoto direttamente nell&#39;Editor pagina di AEM e nel [Frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments.html?lang=it), semplificando i processi di creazione e gestione dei contenuti.

Gli utenti possono connettere più istanze di AEM Sites, senza restrizioni sul numero massimo, a una distribuzione DAM remota, un vantaggio notevole rispetto alla funzionalità [Connected Assets](use-assets-across-connected-assets-instances.md).

![immagine](/help/assets/assets/connected-assets-rdam.png)

Dopo la configurazione iniziale, gli utenti possono creare pagine sull’istanza di AEM Sites e aggiungere risorse in base alle esigenze. Quando aggiungono delle risorse, possono selezionare le risorse memorizzate nel DAM locale oppure sfogliare e utilizzare le risorse disponibili nel DAM remoto.

Dynamic Media con funzionalità OpenAPI offre diversi altri vantaggi, come l’accesso e l’utilizzo di risorse remote in Frammento di contenuto, il recupero dei metadati delle risorse remote e molto altro. Ulteriori informazioni sugli altri [vantaggi di Dynamic Media con funzionalità OpenAPI rispetto a Connected Assets](/help/assets/dynamic-media-open-apis-faqs.md).

## Prima di iniziare {#pre-requisites-sites-integration}

Il supporto per le risorse remote che utilizzano Dynamic Media con funzionalità OpenAPI richiede:

* AEM 6.5 SP 18+ o AEM as a Cloud Service

* Componenti Core versione 2.23.2 o successiva

* Configura le [variabili di ambiente](/help/implementing/cloud-manager/environment-variables.md#add-variables) seguenti per AEM as a Cloud Service:

   * ASSET_DELIVERY_REPOSITORY_ID= &quot;delivery-pxxxxx-eyyyyy.adobeaemcloud.com&quot; <br>

     `pXXXX` fa riferimento all&#39;ID programma <br>
     `eYYYY` fa riferimento all&#39;ID ambiente

  Queste variabili vengono impostate utilizzando l’interfaccia utente di Cloud Manager dell’ambiente AEM as a Cloud Service che funge da istanza Sites locale.

   * ASSET_DELIVERY_IMS_CLIENT= [IMSClientId]: è necessario inviare un ticket di supporto Adobe per ottenere l&#39;ID client IMS.

     o configura le [impostazioni OSGi](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/configuring/configuring-osgi.html?lang=it) per AEM 6.5 nell&#39;istanza AEM Sites eseguendo la procedura seguente:

   1. Accedi alla console e fai clic su **[!UICONTROL OSGi] >** o
utilizzare l&#39;URL diretto, ad esempio: `https://localhost:4502/system/console/configMgr`

   1. Configura la configurazione OSGi **Next Generation Dynamic Media Config** (`NextGenDynamicMediaConfigImpl`) come segue, sostituendo i valori con quelli dell&#39;ambiente di risorse remote.

      ```text
        imsClient="<ims-client-ID>"
        enabled=B"true"
        imsOrg="<ims-org>@AdobeOrg"
        repositoryId="<repo-id>.adobeaemcloud.com"
      ```

      `imsOrg` non è un input obbligatorio.
      `repositoryId` = &quot;delivery-pxxxxx-eyyyyy.adobeaemcloud.com&quot;
dove `pXXXX` fa riferimento all&#39;ID del programma
      `eYYYY` fa riferimento all&#39;ID ambiente

      ![Finestra di configurazione OSGi della configurazione di Dynamic Media di nuova generazione](/help/assets/assets/remote-assets-osgi.png)

  Ulteriori informazioni sull&#39;[autenticazione IMS](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/ims-config-and-admin-console.html?lang=it).

  Per informazioni dettagliate su come configurare OSGi, consulta i seguenti documenti:

   * [Configurazione di OSGi per Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=it) per AEM as a Cloud Service
   * [Configurazione di OSGi](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-osgi.html?lang=it) per AEM 6.5

* Accesso IMS per accedere all’istanza remota di DAM AEM as a Cloud Service. Si riferisce all’autore Sites che dispone dell’accesso IMS all’ambiente DAM remoto.

* Configura il componente Image v3 nell’istanza AEM Sites. Se il componente non è presente, scaricare e installare il [pacchetto di contenuti](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.23.0).

## Configurare HTTPS {#https}

In genere si consiglia di eseguire tutte le istanze di produzione AEM utilizzando HTTP. Tuttavia, gli ambienti di sviluppo locali potrebbero non essere configurati come tali. In ogni caso, le risorse remote di Dynamic Media cion OpenAPI richiedono HTTPS per funzionare.

Per configurare HTTPS ovunque desideri utilizzare le risorse remote, inclusi gli ambienti di sviluppo, [utilizza questa guida](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html?lang=it).

## Accedere alle risorse da DAM remoto {#fetch-assets}

Dynamic Media con funzionalità OpenAPI consente di accedere alle risorse disponibili nell’istanza DAM remota nell’Editor pagina AEM Sites locale e nel Frammento di contenuto AEM.

![immagine](/help/assets/assets/open-APIs.png)

### Accedere alle risorse remote nell’Editor pagina di AEM {#access-assets-page-editor}

Per utilizzare le risorse remote nell’Editor pagina di AEM nell’istanza di AEM Sites, segui la procedura riportata di seguito. Puoi eseguire questa integrazione in AEM as a Cloud Service e AEM 6.5.

1. Vai a **[!UICONTROL Sites]** > _il tuo sito Web_ in cui è presente la **[!UICONTROL pagina]** di AEM in cui devi aggiungere la risorsa remota.
1. Selezionare la pagina e fare clic su **[!UICONTROL Modifica (_e_)]**. Verrà aperto l&#39;**[!UICONTROL Editor pagina]** di AEM.
1. Fai clic sul Contenitore di layout e aggiungi un componente **[!UICONTROL Immagine]**.
1. Fare clic sul componente **[!UICONTROL Immagine]** e sull&#39;icona ![Impostazioni](/help/assets/assets/do-not-localize/settings-icon.svg).
1. Deseleziona l&#39;opzione **[!UICONTROL Eredita immagine in primo piano dalla pagina]**.
1. Fai clic su **[!UICONTROL Scegli]** e seleziona **[!UICONTROL Remoto]**.
   ![immagine](/help/assets/assets/uncheck-inherit-option.jpg)

   Viene richiesto di effettuare l&#39;accesso.
1. Seleziona la risorsa e fai clic su **[!UICONTROL Seleziona]**.
1. Aggiungi un testo alternativo e fai clic su **[!UICONTROL Fine]**.
   <br> La risorsa remota viene visualizzata nel componente immagine. Puoi anche verificare l’URL di consegna della risorsa quando viene caricato sulla pagina o utilizzando la scheda &quot;Anteprima&quot;. L’URL di consegna indica che si accede alla risorsa in modalità remota.

Puoi accedere alle risorse remote nell’editor di pagine AEM predefinito solo per il componente core Immagine v3 e per il componente core Teaser v2. Per altri componenti, compresi quelli personalizzati, sono necessarie personalizzazioni per integrare Asset Selector con tali componenti.

#### Video: accedere alle risorse remote nell’Editor pagina di AEM

>[!VIDEO](https://video.tv.adobe.com/v/3427666)

### Accedere alle risorse remote in Frammento di contenuto di AEM {#access-assets-content-fragment}

Per utilizzare le risorse remote all’interno del frammento di contenuto di AEM nell’istanza di AEM Sites, segui la procedura riportata di seguito. Puoi eseguire questa integrazione in AEM 6.5 e non su AEM as a Cloud Service.

1. Vai a **[!UICONTROL Assets]** > **[!UICONTROL File]**.
1. Seleziona la cartella delle risorse in cui è presente il frammento di contenuto.
1. Selezionare il frammento di contenuto e fare clic su **[!UICONTROL Modifica (_e_)]**.

   >[!NOTE]
   >
   >Se non disponi di un modello per frammenti di contenuto di AEM, potresti dover [crearne uno](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments-models.html?lang=it).

1. Fai clic sull&#39;icona ![segno di spunta](/help/assets/assets/do-not-localize/checkmark-icon.svg) accanto al componente testo.
1. Seleziona **[!UICONTROL Remoto]** per recuperare la risorsa dal DAM remoto. <br>
Puoi scegliere **[!UICONTROL Local]** o **[!UICONTROL Remote]** DAM repository in base alle tue esigenze.

   ![immagine](/help/assets/assets/cf-pick.jpg)
Viene richiesto di effettuare l&#39;accesso.
1. Scegli la risorsa e fai clic su **[!UICONTROL Seleziona]**.
   <br> L&#39;URL della risorsa remota viene visualizzato nel componente testo.

#### Video: accedere alle risorse remote in Frammento di contenuto di AEM

>[!VIDEO](https://video.tv.adobe.com/v/3427667)

### Accedere alle risorse remote in Edge Delivery Services {#access-assets-eds}

È possibile accedere alle risorse remote durante l’authoring di contenuti in Microsoft Word, Google Docs o Universal Editor e quindi pubblicarli in Edge Delivery Services. Dynamic Media può essere utilizzato anche con OpenAPI per fornire risorse approvate dal marchio e sfruttare molti altri vantaggi offerti. Per ulteriori informazioni, vedere [Integrare AEM Assets durante la creazione di contenuti per Edge Delivery Services](/help/assets/integrate-aem-assets-edge-delivery-services.md).
