---
title: Digital Rights Management in [!DNL Assets]
description: Scopri come gestire gli stati di scadenza delle risorse e le informazioni per le risorse con licenza in [!DNL Experience Manager] come a [!DNL Cloud Service].
contentOwner: AG
feature: Gestione risorse, DRM
role: User,Admin
exl-id: fa5f94df-1c15-4593-afcb-1d24508da2bf
source-git-commit: f993148a9f678cfdaf0693e4964f02b9163cf2ff
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 2%

---

# Digital Rights Management per le risorse digitali {#digital-rights-management-in-assets}

Le risorse digitali sono spesso associate a una licenza che specifica i termini e la durata dell’utilizzo. Utilizzando la piattaforma [!DNL Experience Manager], puoi gestire in modo efficiente le informazioni sulla scadenza delle risorse e le informazioni sulle licenze.

## Scadenza risorse {#asset-expiration}

Per applicare i requisiti di licenza per le risorse, utilizza le informazioni sulla scadenza delle risorse. Le informazioni sulla scadenza garantiscono che la pubblicazione della risorsa pubblicata venga annullata alla scadenza, il che impedisce la violazione della licenza. Un utente senza autorizzazioni di amministratore non può modificare, copiare, spostare, pubblicare e scaricare una risorsa scaduta.

Puoi visualizzare lo stato di scadenza di una risorsa nei seguenti punti:

* **Vista** a schede: Per una risorsa scaduta, un flag sulla scheda indica che è scaduta.
* **Vista** a elenco: Per una risorsa scaduta, nella colonna  **** Statusvengono visualizzati i  **** caratteri Expiredbanner.
* **Timeline**: Puoi visualizzare lo stato di scadenza di una risorsa nella timeline. Seleziona la risorsa e scegli Timeline.
* **Barra** Riferimenti: Puoi anche visualizzare lo stato di scadenza delle risorse nella barra  **** Riferimenti. Gestisce gli stati di scadenza delle risorse e le relazioni tra le risorse composte e le risorse secondarie, le raccolte e i progetti a cui si fa riferimento.

Per visualizzare le pagine web di riferimento e le risorse composte di una risorsa, effettua le seguenti operazioni:

1. Accedi alla risorsa, selezionala e fai clic sull&#39;icona dei riferimenti ai contenuti della barra a sinistra ](assets/do-not-localize/content-rail-icon.png). ![ Viene visualizzata la barra a sinistra.
1. Seleziona **[!UICONTROL Riferimenti]** dalla barra a sinistra.
1. Per le risorse scadute, lo stato di scadenza è [!UICONTROL Riferimenti]: **[!UICONTROL Risorsa scaduta]**. Se la risorsa è scaduta, nella barra [!UICONTROL Riferimenti] viene visualizzato lo stato **[!UICONTROL Risorse secondarie scadute]**.

### Cercare risorse scadute {#search-expired-assets}

Per cercare una risorsa scaduta, incluse le risorse secondarie scadute, procedi come segue:

1. Nella console [!DNL Assets], fai clic su **[!UICONTROL Cerca]** nella barra degli strumenti e premi `Enter`.

1. Fai clic sull&#39;icona di Navigazione globale e seleziona l&#39;opzione **[!UICONTROL Stato scadenza]** .

1. Selezionare **[!UICONTROL Scaduto]**. Nei risultati della ricerca vengono visualizzate le risorse scadute.

Quando scegli l’opzione **[!UICONTROL Expired]** , nella console [!DNL Assets] vengono visualizzate solo le risorse e le risorse secondarie scadute a cui fanno riferimento le risorse composte. Le risorse composte che fanno riferimento a risorse secondarie scadute non vengono visualizzate immediatamente dopo la scadenza delle risorse secondarie. Vengono invece visualizzati dopo che [!DNL Experience Manager] rileva che fanno riferimento a risorse secondarie scadute al successivo esecuzione della pianificazione.

È possibile modificare la data di scadenza di una risorsa pubblicata in una data precedente al ciclo di pianificazione corrente. Tuttavia, la pianificazione rileva ancora una risorsa come una risorsa scaduta quando viene eseguita la prossima volta e [!DNL Experience Manager] riflette lo stato nel relativo rapporto. La data di scadenza di una risorsa viene visualizzata in modo diverso per gli utenti che usano fusi orari diversi.

Inoltre, se un errore impedisce al programmatore di rilevare le risorse scadute nel ciclo corrente, lo scheduler riesamina tali risorse nel ciclo successivo e ne rileva lo stato scaduto.

Per abilitare la console [!DNL Assets] affinché visualizzi le risorse composte di riferimento insieme alle risorse secondarie scadute, configura il flusso di lavoro **[!UICONTROL Notifica di scadenza Adobe CQ DAM]** in [!DNL Experience Manager]. L’utilità di pianificazione basata su tempo pianifica un processo per verificare in un momento specifico se una risorsa è scaduta o meno. Al termine del processo, le risorse con risorse secondarie scadute e risorse di riferimento vengono visualizzate come scadute nei risultati della ricerca.

1. Accedi all’ archivio Git [!DNL Cloud Manager] associato al tuo ambiente.
1. Commit di un file denominato `com.day.cq.dam.core.impl.ExpiryNotificationJobImpl.cfg.json` nell’archivio con il seguente contenuto.

   ```json
   {
      "send_email":"false", "asset_expired_limit":"100", "prior_notification_seconds":"86400", "cq.dam.expiry.notification.url.protocol":"http", "cq.dam.expiry.notification.scheduler.istimebased":"true", "cq.dam.expiry.notification.scheduler.period.rule":"10", "cq.dam.expiry.notification.scheduler.timebased.rule":"0 0 0 * * ?"
   }
   ```

1. Segui le istruzioni di [come eseguire la configurazione OSGi in [!DNL Experience Manager] come a [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md).

Puoi configurare la pianificazione utilizzando le seguenti proprietà:

* Un valore `true` della proprietà `cq.dam.expiry.notification.scheduler.istimebased` avvia la pianificazione. * Il valore della proprietà `cq.dam.expiry.notification.scheduler.timebased.rule` è l&#39;espressione regolare per definire l&#39;ora. L&#39;esempio precedente avvia il processo di pianificazione alle 00 ore.
* Se `send_email` è impostato su `true`, il creatore della risorsa (la persona che carica una particolare risorsa in [!DNL Assets]) riceve un’e-mail alla scadenza della risorsa.
* Il numero massimo di risorse scadute in un&#39;iterazione dello scheduler è il valore della proprietà `asset_expired_limit`.
* Per eseguire periodicamente il processo, imposta il valore della proprietà `cq.dam.expiry.notification.scheduler.istimebased` come `false` e imposta il valore della proprietà `cq.dam.expiry.notification.scheduler.period.rule` con il tempo in secondi.

<!-- TBD: Web Console not available in CS.

1. Open [!DNL Experience Manager] Configuration Manager.
1. Choose **[!UICONTROL Adobe CQ DAM Expiry Notification]**. By default, **[!UICONTROL Time-based Scheduler]** is selected, which 

1.  For example, the example expression '0 0 0 &ast; &ast; ?' triggers the job at 0000 hrs.

1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

1. In the **[!UICONTROL Prior notification in seconds]** field, specify the time in seconds before the asset expiry when you want to receive a notification. If you are an administrator or the asset creator, you receive a message before the expiration of the asset. After the asset expiry, you receive another notification that confirms the expiration. In addition, the expired asset is deactivated.

1. Select **[!UICONTROL Save]**.
-->

## Stati delle risorse {#asset-states}

La console [!DNL Assets] può visualizzare vari stati delle risorse. A seconda dello stato corrente di una particolare risorsa, nella relativa vista a schede viene visualizzata un’etichetta che ne descrive lo stato, ad esempio Scaduto, Pubblicato, Approvato, Rifiutato e così via.

1. Nell’interfaccia utente di [!DNL Assets] , seleziona una risorsa.

1. Seleziona **[!UICONTROL Pubblica]** dalla barra degli strumenti. Se l&#39;opzione [!UICONTROL Pubblica] non è disponibile nella barra degli strumenti, fare clic su **[!UICONTROL Altro]** nella barra degli strumenti e individuare l&#39;opzione **[!UICONTROL Pubblica]**.

1. Scegli **[!UICONTROL Pubblica]** dal menu, quindi chiudi la finestra di dialogo di conferma.

1. Esci dalla modalità di selezione. Lo stato di pubblicazione della risorsa viene visualizzato nella parte inferiore della miniatura della risorsa nella vista a schede. Nella vista a elenco, la colonna Pubblicato visualizza l’ora in cui è stata pubblicata la risorsa.

1. Per visualizzare la pagina dei dettagli della risorsa, nell’interfaccia [!DNL Assets] seleziona una risorsa e fai clic su **[!UICONTROL Proprietà]**.

1. Nella scheda [!UICONTROL Avanzate] , imposta una data di scadenza per la risorsa dal campo **[!UICONTROL Scade]** .

1. Fai clic su **[!UICONTROL Salva]**, quindi fai clic su **[!UICONTROL Chiudi]** per visualizzare la console delle risorse.

1. Lo stato di pubblicazione della risorsa indica uno stato scaduto nella parte inferiore della miniatura della risorsa nella vista a schede. Nella vista a elenco, lo stato della risorsa viene visualizzato come **[!UICONTROL Scaduto]**.

1. Nella console [!DNL Assets], seleziona una cartella e crea un’attività di revisione sulla cartella.

1. Rivedi e approva/rifiuta le risorse nell’attività di revisione e fai clic su **[!UICONTROL Completa]**.

1. Passare alla cartella per la quale è stata creata l&#39;attività di revisione. Lo stato delle risorse approvate o rifiutate viene visualizzato nella parte inferiore della vista a schede. Nella vista a elenco, gli stati di approvazione e scadenza vengono visualizzati nelle colonne appropriate.

1. Per cercare le risorse in base al loro stato, fai clic su **[!UICONTROL Cerca]** per visualizzare la barra di ricerca.

1. Selezionare `Return` e fare clic su [!DNL Experience Manager].

1. Nel pannello di ricerca, fai clic su **[!UICONTROL Stato pubblicazione]** e seleziona **[!UICONTROL Pubblicato]** per cercare le risorse pubblicate in [!DNL Assets].

1. Per cercare le risorse approvate o rifiutate, seleziona **[!UICONTROL Stato approvazione]** e seleziona l’opzione appropriata.

1. Per cercare le risorse in base al loro stato di scadenza, seleziona **[!UICONTROL Stato scadenza]** nel pannello di ricerca e seleziona l’opzione appropriata.

1. Puoi anche cercare le risorse in base a una combinazione di stati in vari facet di ricerca. Ad esempio, puoi cercare le risorse pubblicate approvate in un’attività di revisione e non scadute. Per cercare tali risorse, seleziona le opzioni appropriate nei facet di ricerca.

## Digital Rights Management in [!DNL Assets] {#digital-rights-management-in-assets-1}

La funzionalità DRM impone l’accettazione del contratto di licenza prima di poter scaricare una risorsa con licenza da [!DNL Assets].

Se selezioni una risorsa protetta e fai clic su **[!UICONTROL Scarica]**, vieni reindirizzato a una pagina di licenza per accettare il contratto di licenza. Se non accetti il contratto di licenza, l&#39;opzione **[!UICONTROL Scarica]** non è disponibile.

Se la selezione contiene più risorse protette, seleziona una risorsa alla volta, accetta il contratto di licenza e procedi con il download.

Un’attività è considerata protetta se una di queste condizioni è soddisfatta:

* La proprietà metadati della risorsa `xmpRights:WebStatement` punta al percorso della pagina che contiene il contratto di licenza per la risorsa.
* Il valore della proprietà metadati risorsa `adobe_dam:restrictions` è un codice HTML non elaborato che specifica il contratto di licenza.

>[!NOTE]
>
>Il percorso `/etc/dam/drm/licences` è stato utilizzato per memorizzare le licenze nelle versioni precedenti di [!DNL Experience Manager]. La posizione è ora obsoleta. Se crei o modifichi pagine di licenza o porti le pagine delle versioni precedenti di [!DNL Experience Manager] , Adobe consiglia di memorizzarle nelle posizioni `/apps/settings/dam/drm/licenses` o `/conf/*/settings/dam/drm/licenses`.

### Scaricare risorse protette da DRM {#downloading-drm-assets}

1. Nella vista a schede, seleziona le risorse da scaricare e seleziona **[!UICONTROL Scarica]**.
1. Nella pagina **[!UICONTROL Gestione copyright]**, seleziona dall’elenco la risorsa da scaricare.
1. Nel riquadro [!UICONTROL Licenza], scegli **[!UICONTROL Accetto]**. Accanto alla risorsa viene visualizzato un segno di spunta. Selezionare l&#39;opzione **[!UICONTROL Scarica]**.

   >[!NOTE]
   >
   >L’opzione **[!UICONTROL Scarica]** è abilitata solo quando scegli di accettare il contratto di licenza per una risorsa protetta. Tuttavia, se la selezione include sia risorse protette che non protette, solo le risorse protette sono elencate nel riquadro e l’opzione **[!UICONTROL Download]** è disponibile per scaricare le risorse non protette. Per accettare in contemporanea i contratti di licenza per più risorse protette, seleziona le risorse dall’elenco e fai clic su **[!UICONTROL Accetto]**.

1. Per scaricare la risorsa o le relative rappresentazioni, seleziona **[!UICONTROL Scarica]** nella finestra di dialogo.
