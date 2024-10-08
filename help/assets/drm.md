---
title: Digital Rights Management in [!DNL Assets]
description: Scopri come gestire gli stati di scadenza delle risorse e le informazioni per le risorse con licenza in [!DNL Experience Manager] as a [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management,DRM
role: User, Admin
exl-id: fa5f94df-1c15-4593-afcb-1d24508da2bf
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '1386'
ht-degree: 6%

---

# Digital Rights Management per risorse digitali {#digital-rights-management-in-assets}

| [Best practice per la ricerca](/help/assets/search-best-practices.md) | [Best practice per i metadati](/help/assets/metadata-best-practices.md) | [Hub di contenuti](/help/assets/product-overview.md) | [Dynamic Medie con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentazione per gli sviluppatori di AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/drm.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

Le risorse digitali sono spesso associate a una licenza che specifica i termini e la durata di utilizzo. Utilizzando la piattaforma [!DNL Experience Manager], puoi gestire in modo efficiente le informazioni sulla scadenza delle risorse e le informazioni sulle licenze.

## Scadenza risorsa {#asset-expiration}

Per applicare i requisiti di licenza per le risorse, utilizza le informazioni sulla scadenza delle risorse. Le informazioni sulla scadenza garantiscono che la pubblicazione della risorsa pubblicata venga annullata alla scadenza, impedendo in tal modo la violazione della licenza. Un utente senza autorizzazioni di amministratore non può modificare, copiare, spostare, pubblicare e scaricare una risorsa scaduta.

Puoi visualizzare lo stato di scadenza di una risorsa nelle seguenti posizioni:

* **Vista a schede**: per una risorsa scaduta, un flag sulla scheda indica che è scaduta.
* **Vista a elenco**: per una risorsa scaduta, la colonna **[!UICONTROL Stato]** visualizza il banner **[!UICONTROL Scaduto]**.
* **Timeline**: puoi visualizzare lo stato di scadenza di una risorsa nella timeline. Seleziona la risorsa e scegli Timeline.
* **Barra dei riferimenti**: puoi anche visualizzare lo stato di scadenza delle risorse nella barra **[!UICONTROL Riferimenti]**. Gestisce gli stati di scadenza delle risorse e le relazioni tra le risorse composte e le risorse secondarie, le raccolte e i progetti di riferimento.

Per visualizzare le pagine web di riferimento e le risorse composte di una risorsa, effettua le seguenti operazioni:

1. Passa alla risorsa, selezionala e fai clic su ![icona riferimenti contenuti barra a sinistra](assets/do-not-localize/content-rail-icon.png). Si apre la barra a sinistra.
1. Seleziona **[!UICONTROL Riferimenti]** dalla barra a sinistra.
1. Per le risorse scadute, [!UICONTROL References] visualizza lo stato di scadenza come **[!UICONTROL La risorsa è scaduta]**. Se la risorsa è scaduta, nella barra [!UICONTROL Riferimenti] viene visualizzato lo stato **[!UICONTROL La risorsa è scaduta Sub-Assets]**.

### Cercare risorse scadute {#search-expired-assets}

Per cercare una risorsa scaduta, comprese le risorse secondarie scadute, effettua le seguenti operazioni:

1. Nella console [!DNL Assets], fare clic su **[!UICONTROL Cerca]** nella barra degli strumenti e premere `Enter`.

1. Fai clic sull&#39;icona GlobalNav e seleziona l&#39;opzione **[!UICONTROL Stato scadenza]**.

1. Seleziona **[!UICONTROL Scaduto]**. I risultati della ricerca mostrano le risorse scadute.

Quando scegli l&#39;opzione **[!UICONTROL Scaduto]**, nella console [!DNL Assets] vengono visualizzate solo le risorse e le risorse secondarie scadute a cui fanno riferimento le risorse composte. Le risorse composte che fanno riferimento a risorse secondarie scadute non vengono visualizzate immediatamente dopo la scadenza delle risorse secondarie. Vengono invece visualizzati dopo che [!DNL Experience Manager] ha rilevato che fanno riferimento a risorse secondarie scadute alla successiva esecuzione del modulo di pianificazione.

È possibile modificare la data di scadenza di una risorsa pubblicata in una data precedente al ciclo di pianificazione corrente. Tuttavia, la pianificazione rileva ancora una risorsa come scaduta quando viene eseguita la volta successiva e [!DNL Experience Manager] ne riflette lo stato nel report. La data di scadenza di una risorsa viene visualizzata in modo diverso per gli utenti con fusi orari diversi.

Inoltre, se un errore impedisce al modulo di pianificazione di rilevare le risorse scadute nel ciclo corrente, il modulo di pianificazione le esamina nuovamente nel ciclo successivo e ne rileva lo stato di scadenza.

Per abilitare la console [!DNL Assets] per visualizzare le risorse composte di riferimento insieme alle risorse secondarie scadute, configura il flusso di lavoro **[!UICONTROL Adobe CQ DAM Expiry Notification]** in [!DNL Experience Manager]. Il modulo di pianificazione basato sul tempo pianifica un processo per verificare in un momento specifico se una risorsa è scaduta o meno. Al termine del processo, le risorse con risorse secondarie scadute e le risorse di riferimento vengono visualizzate come scadute nei risultati della ricerca.

1. Accedi all&#39;archivio Git [!DNL Cloud Manager] associato al tuo ambiente.
1. Eseguire il commit di un file denominato `com.day.cq.dam.core.impl.ExpiryNotificationJobImpl.cfg.json` nell&#39;archivio con il contenuto seguente.

   ```json
   {
      "send_email":"false", "asset_expired_limit":"100", "prior_notification_seconds":"86400", "cq.dam.expiry.notification.url.protocol":"http", "cq.dam.expiry.notification.scheduler.istimebased":"true", "cq.dam.expiry.notification.scheduler.period.rule":"10", "cq.dam.expiry.notification.scheduler.timebased.rule":"0 0 0 * * ?"
   }
   ```

1. Segui le istruzioni di [come configurare OSGi in [!DNL Experience Manager] as a [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md).

Puoi configurare la pianificazione utilizzando le seguenti proprietà:

* Un valore `true` della proprietà `cq.dam.expiry.notification.scheduler.istimebased` avvia il modulo di pianificazione. * Il valore della proprietà `cq.dam.expiry.notification.scheduler.timebased.rule` è l&#39;espressione regolare per definire l&#39;ora. L&#39;esempio precedente avvia il processo di pianificazione a 00 ore.
* Se `send_email` è impostato su `true`, il creatore della risorsa (la persona che carica una particolare risorsa in [!DNL Assets]) riceve un&#39;e-mail alla scadenza della risorsa.
* Il numero massimo di risorse scadute in un&#39;iterazione della pianificazione è il valore della proprietà `asset_expired_limit`.
* Per eseguire il processo periodicamente, impostare il valore della proprietà `cq.dam.expiry.notification.scheduler.istimebased` come `false` e impostare il valore della proprietà `cq.dam.expiry.notification.scheduler.period.rule` in secondi.

<!-- TBD: Web Console not available in CS.

1. Open [!DNL Experience Manager] Configuration Manager.
1. Choose **[!UICONTROL Adobe CQ DAM Expiry Notification]**. By default, **[!UICONTROL Time-based Scheduler]** is selected, which 

1. For example, the example expression '0 0 0 &ast; &ast; ?' triggers the job at 0000 hrs.

1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

1. In the **[!UICONTROL Prior notification in seconds]** field, specify the time in seconds before the asset expiry when you want to receive a notification. If you are an administrator or the asset creator, you receive a message before the expiration of the asset. After the asset expiry, you receive another notification that confirms the expiration. In addition, the expired asset is deactivated.

1. Select **[!UICONTROL Save]**.
-->

## Stati risorse {#asset-states}

La console [!DNL Assets] può visualizzare vari stati per le risorse. A seconda dello stato corrente di una particolare risorsa, la relativa vista a schede mostra un’etichetta che ne descrive lo stato, ad esempio Scaduto, Pubblicato, Approvato, Rifiutato e così via.

1. Nell&#39;interfaccia utente [!DNL Assets], seleziona una risorsa.

1. Seleziona **[!UICONTROL Publish]** nella barra degli strumenti. Se nella barra degli strumenti non è visualizzata l&#39;opzione [!UICONTROL Publish], fare clic su **[!UICONTROL Altro]** e individuare l&#39;opzione **[!UICONTROL Publish]**.

1. Scegliere **[!UICONTROL Publish]** dal menu, quindi chiudere la finestra di dialogo di conferma.

1. Esci dalla modalità di selezione. Lo stato di pubblicazione della risorsa viene visualizzato nella parte inferiore della miniatura nella vista a schede. Nella vista a elenco, la colonna Pubblicato mostra l’ora in cui la risorsa è stata pubblicata.

1. Per visualizzare la pagina dei dettagli della risorsa, nell&#39;interfaccia [!DNL Assets] selezionare una risorsa e fare clic su **[!UICONTROL Proprietà]**.

1. Nella scheda [!UICONTROL Avanzate], imposta una data di scadenza per la risorsa dal campo **[!UICONTROL Scade]**.

1. Fai clic su **[!UICONTROL Salva]**, quindi su **[!UICONTROL Chiudi]** per visualizzare la console Risorse.

1. Lo stato di pubblicazione della risorsa indica uno stato scaduto nella parte inferiore della miniatura della risorsa nella vista a schede. Nella vista a elenco, lo stato della risorsa è **[!UICONTROL Scaduto]**.

1. Nella console [!DNL Assets], selezionare una cartella e creare un&#39;attività di revisione sulla cartella.

1. Rivedi e approva/rifiuta le risorse nell&#39;attività di revisione e fai clic su **[!UICONTROL Completa]**.

1. Passare alla cartella per la quale è stata creata l&#39;attività di revisione. Lo stato delle risorse approvate/rifiutate viene visualizzato nella parte inferiore della vista a schede. Nella vista a elenco, gli stati di approvazione e scadenza vengono visualizzati nelle colonne appropriate.

1. Per cercare le risorse in base al loro stato, fai clic su **[!UICONTROL Cerca]** per visualizzare la barra di ricerca.

1. Selezionare `Return` e fare clic su [!DNL Experience Manager].

1. Nel pannello di ricerca, fai clic su **[!UICONTROL Stato Publish]** e seleziona **[!UICONTROL Pubblicato]** per cercare le risorse pubblicate in [!DNL Assets].

1. Per cercare le risorse approvate o rifiutate, selezionare **[!UICONTROL Stato approvazione]** e selezionare l&#39;opzione appropriata.

1. Per cercare le risorse in base al loro stato di scadenza, seleziona **[!UICONTROL Stato scadenza]** nel pannello di ricerca e seleziona l&#39;opzione appropriata.

1. Puoi anche cercare le risorse in base a una combinazione di stati in vari facet di ricerca. Ad esempio, puoi cercare le risorse pubblicate che sono state approvate in un’attività di revisione e che non sono scadute. Per cercare tali risorse, seleziona le opzioni appropriate nei facet di ricerca.

## Digital Rights Management in [!DNL Assets] {#digital-rights-management-in-assets-1}

La funzionalità DRM impone l&#39;accettazione del contratto di licenza prima di scaricare una risorsa concessa in licenza da [!DNL Assets].

Se selezioni una risorsa protetta e fai clic su **[!UICONTROL Scarica]**, verrai reindirizzato a una pagina di licenza per accettare il contratto di licenza. Se non si accetta il contratto di licenza, l&#39;opzione **[!UICONTROL Scarica]** non è disponibile.

Se la selezione contiene più risorse protette, seleziona una risorsa alla volta, accetta il contratto di licenza e procedi al download della risorsa.

Un bene è considerato protetto se è soddisfatta una delle seguenti condizioni:

* La proprietà dei metadati della risorsa `xmpRights:WebStatement` punta al percorso della pagina che contiene il contratto di licenza per la risorsa.
* Il valore della proprietà dei metadati della risorsa `adobe_dam:restrictions` è un HTML non elaborato che specifica il contratto di licenza.

>[!NOTE]
>
>Il percorso `/etc/dam/drm/licences` è stato utilizzato per archiviare le licenze nelle versioni precedenti di [!DNL Experience Manager]. La posizione è ora obsoleta. Se si creano o si modificano le pagine delle licenze o si porta le pagine da [!DNL Experience Manager] versioni precedenti, l&#39;Adobe consiglia di memorizzare tali risorse in `/apps/settings/dam/drm/licenses` o `/conf/*/settings/dam/drm/licenses` posizioni.

### Scaricare risorse protette da DRM {#downloading-drm-assets}

1. Nella vista a schede, seleziona le risorse da scaricare e seleziona **[!UICONTROL Scarica]**.
1. Nella pagina **[!UICONTROL Gestione copyright]**, seleziona dall’elenco la risorsa da scaricare.
1. Nel riquadro [!UICONTROL Licenza], scegliere **[!UICONTROL Accetto]**. Accanto alla risorsa viene visualizzato un segno di spunta. Selezionare l&#39;opzione **[!UICONTROL Scarica]**.

   >[!NOTE]
   >
   >L&#39;opzione **[!UICONTROL Scarica]** è abilitata solo quando si sceglie di accettare il contratto di licenza per una risorsa protetta. Tuttavia, se la selezione include sia risorse protette che non protette, nel riquadro vengono elencate solo le risorse protette e l&#39;opzione **[!UICONTROL Scarica]** è disponibile per scaricare le risorse non protette. Per accettare in contemporanea i contratti di licenza per più risorse protette, seleziona le risorse dall’elenco e fai clic su **[!UICONTROL Accetto]**.

1. Per scaricare la risorsa o le relative rappresentazioni, seleziona **[!UICONTROL Scarica]** nella finestra di dialogo.

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
