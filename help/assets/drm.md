---
title: Digital Rights Management in [!DNL Assets]
description: Scopri come gestire gli stati di scadenza delle risorse e le informazioni per le risorse con licenza in [!DNL Experience Manager] come [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management,DRM
role: User,Admin
exl-id: fa5f94df-1c15-4593-afcb-1d24508da2bf
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1345'
ht-degree: 3%

---

# Digital Rights Management per le risorse digitali {#digital-rights-management-in-assets}

Le risorse digitali sono spesso associate a una licenza che specifica i termini e la durata dell’utilizzo. Utilizzo della [!DNL Experience Manager] Platform consente di gestire in modo efficiente le informazioni sulla scadenza delle risorse e le informazioni sulla licenza.

## Scadenza risorse {#asset-expiration}

Per applicare i requisiti di licenza per le risorse, utilizza le informazioni sulla scadenza delle risorse. Le informazioni sulla scadenza garantiscono che la pubblicazione della risorsa pubblicata venga annullata alla scadenza, il che impedisce la violazione della licenza. Un utente senza autorizzazioni di amministratore non può modificare, copiare, spostare, pubblicare e scaricare una risorsa scaduta.

Puoi visualizzare lo stato di scadenza di una risorsa nei seguenti punti:

* **Vista a schede**: Per una risorsa scaduta, un flag sulla scheda indica che è scaduta.
* **Vista a elenco**: Per una risorsa scaduta, il **[!UICONTROL Stato]** visualizza la colonna **[!UICONTROL Scaduto]** striscione.
* **Timeline**: Puoi visualizzare lo stato di scadenza di una risorsa nella timeline. Seleziona la risorsa e scegli Timeline.
* **Barra dei riferimenti**: Puoi anche visualizzare lo stato di scadenza delle risorse nella **[!UICONTROL Riferimenti]** barra. Gestisce gli stati di scadenza delle risorse e le relazioni tra le risorse composte e le risorse secondarie, le raccolte e i progetti a cui si fa riferimento.

Per visualizzare le pagine web di riferimento e le risorse composte di una risorsa, effettua le seguenti operazioni:

1. Accedi alla risorsa, selezionala e fai clic su ![icona dei riferimenti dei contenuti della barra a sinistra](assets/do-not-localize/content-rail-icon.png). Viene visualizzata la barra a sinistra.
1. Seleziona **[!UICONTROL Riferimenti]** dalla barra a sinistra.
1. Per le risorse scadute, la [!UICONTROL Riferimenti] visualizza lo stato di scadenza come **[!UICONTROL Risorsa scaduta]**. Se la risorsa è scaduta, la [!UICONTROL Riferimenti] visualizza lo stato **[!UICONTROL Risorse secondarie scadute]**.

### Cercare risorse scadute {#search-expired-assets}

Per cercare una risorsa scaduta, incluse le risorse secondarie scadute, procedi come segue:

1. In [!DNL Assets] console, fai clic su **[!UICONTROL Ricerca]** nella barra degli strumenti e premere `Enter`.

1. Fai clic sull’icona di Navigazione globale e seleziona la **[!UICONTROL Stato di scadenza]** opzione .

1. Seleziona **[!UICONTROL Scaduto]**. Nei risultati della ricerca vengono visualizzate le risorse scadute.

Quando scegli la **[!UICONTROL Scaduto]** l&#39;opzione [!DNL Assets] in console vengono visualizzate solo le risorse e le risorse secondarie scadute a cui fanno riferimento le risorse composte. Le risorse composte che fanno riferimento a risorse secondarie scadute non vengono visualizzate immediatamente dopo la scadenza delle risorse secondarie. Vengono invece visualizzati dopo [!DNL Experience Manager] rileva che fanno riferimento a risorse secondarie scadute alla successiva esecuzione della pianificazione.

È possibile modificare la data di scadenza di una risorsa pubblicata in una data precedente al ciclo di pianificazione corrente. Tuttavia, la pianificazione rileva ancora una risorsa come una risorsa scaduta quando viene eseguita la prossima volta e [!DNL Experience Manager] riflette lo stato del rapporto. La data di scadenza di una risorsa viene visualizzata in modo diverso per gli utenti che usano fusi orari diversi.

Inoltre, se un errore impedisce al programmatore di rilevare le risorse scadute nel ciclo corrente, lo scheduler riesamina tali risorse nel ciclo successivo e ne rileva lo stato scaduto.

Per abilitare [!DNL Assets] per visualizzare le risorse composte di riferimento insieme alle risorse secondarie scadute, configura **[!UICONTROL Notifica di scadenza di Adobe CQ DAM]** workflow in [!DNL Experience Manager]. L’utilità di pianificazione basata su tempo pianifica un processo per verificare in un momento specifico se una risorsa è scaduta o meno. Al termine del processo, le risorse con risorse secondarie scadute e risorse di riferimento vengono visualizzate come scadute nei risultati della ricerca.

1. Accedere al [!DNL Cloud Manager] Archivio Git associato all’ambiente.
1. Commit di un file denominato `com.day.cq.dam.core.impl.ExpiryNotificationJobImpl.cfg.json` nel repository con i seguenti contenuti.

   ```json
   {
      "send_email":"false", "asset_expired_limit":"100", "prior_notification_seconds":"86400", "cq.dam.expiry.notification.url.protocol":"http", "cq.dam.expiry.notification.scheduler.istimebased":"true", "cq.dam.expiry.notification.scheduler.period.rule":"10", "cq.dam.expiry.notification.scheduler.timebased.rule":"0 0 0 * * ?"
   }
   ```

1. Seguire le istruzioni di [come eseguire la configurazione OSGi in [!DNL Experience Manager] come [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md).

Puoi configurare la pianificazione utilizzando le seguenti proprietà:

* A `true` valore della proprietà `cq.dam.expiry.notification.scheduler.istimebased` avvia la pianificazione. * Il valore della proprietà `cq.dam.expiry.notification.scheduler.timebased.rule` è l’espressione regolare per definire l’ora. L&#39;esempio precedente avvia il processo di pianificazione alle 00 ore.
* Se `send_email` è impostato su `true`, il creatore di risorse (la persona che carica una particolare risorsa in [!DNL Assets]) riceve un’e-mail alla scadenza della risorsa.
* Il numero massimo di risorse scadute in un&#39;iterazione dello scheduler è il valore della proprietà `asset_expired_limit`.
* Per eseguire periodicamente il processo, imposta il valore della proprietà `cq.dam.expiry.notification.scheduler.istimebased` come `false` e imposta il valore della proprietà `cq.dam.expiry.notification.scheduler.period.rule` con tempo in secondi.

<!-- TBD: Web Console not available in CS.

1. Open [!DNL Experience Manager] Configuration Manager.
1. Choose **[!UICONTROL Adobe CQ DAM Expiry Notification]**. By default, **[!UICONTROL Time-based Scheduler]** is selected, which 

1. For example, the example expression '0 0 0 &ast; &ast; ?' triggers the job at 0000 hrs.

1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

1. In the **[!UICONTROL Prior notification in seconds]** field, specify the time in seconds before the asset expiry when you want to receive a notification. If you are an administrator or the asset creator, you receive a message before the expiration of the asset. After the asset expiry, you receive another notification that confirms the expiration. In addition, the expired asset is deactivated.

1. Select **[!UICONTROL Save]**.
-->

## Stati delle risorse {#asset-states}

La [!DNL Assets] La console può visualizzare vari stati delle risorse. A seconda dello stato corrente di una particolare risorsa, nella relativa vista a schede viene visualizzata un’etichetta che ne descrive lo stato, ad esempio Scaduto, Pubblicato, Approvato, Rifiutato e così via.

1. In [!DNL Assets] interfaccia utente, seleziona una risorsa.

1. Seleziona **[!UICONTROL Pubblica]** dalla barra degli strumenti. Se non vedi [!UICONTROL Pubblica] nella barra degli strumenti, fai clic su **[!UICONTROL Altro]** sulla barra degli strumenti e individua **[!UICONTROL Pubblica]** opzione .

1. Scegli **[!UICONTROL Pubblica]** dal menu , quindi chiudi la finestra di dialogo di conferma.

1. Esci dalla modalità di selezione. Lo stato di pubblicazione della risorsa viene visualizzato nella parte inferiore della miniatura della risorsa nella vista a schede. Nella vista a elenco, la colonna Pubblicato visualizza l’ora in cui è stata pubblicata la risorsa.

1. Per visualizzare la pagina dei dettagli della relativa risorsa, nella [!DNL Assets] interfaccia, seleziona una risorsa e fai clic su **[!UICONTROL Proprietà]**.

1. In [!UICONTROL Avanzate] imposta una data di scadenza per la risorsa dalla **[!UICONTROL Scadenza]** campo .

1. Fai clic su **[!UICONTROL Salva]** quindi fai clic su **[!UICONTROL Chiudi]** per visualizzare la console Risorse .

1. Lo stato di pubblicazione della risorsa indica uno stato scaduto nella parte inferiore della miniatura della risorsa nella vista a schede. Nella vista a elenco, lo stato della risorsa viene visualizzato come **[!UICONTROL Scaduto]**.

1. In [!DNL Assets] console, seleziona una cartella e crea un’attività di revisione nella cartella.

1. Rivedi e approva/rifiuta le risorse nell’attività di revisione e fai clic su **[!UICONTROL Completa]**.

1. Passare alla cartella per la quale è stata creata l&#39;attività di revisione. Lo stato delle risorse approvate o rifiutate viene visualizzato nella parte inferiore della vista a schede. Nella vista a elenco, gli stati di approvazione e scadenza vengono visualizzati nelle colonne appropriate.

1. Per cercare le risorse in base al loro stato, fai clic su **[!UICONTROL Ricerca]** per visualizzare la barra di ricerca.

1. Seleziona `Return` e fai clic su [!DNL Experience Manager].

1. Nel pannello di ricerca, fai clic su **[!UICONTROL Stato di pubblicazione]** e seleziona **[!UICONTROL Pubblicato]** per cercare le risorse pubblicate in [!DNL Assets].

1. Per cercare le risorse approvate o rifiutate, seleziona **[!UICONTROL Stato di approvazione]** e selezionare l&#39;opzione appropriata.

1. Per cercare le risorse in base al loro stato di scadenza, seleziona **[!UICONTROL Stato di scadenza]** nel pannello di ricerca e seleziona l’opzione appropriata.

1. Puoi anche cercare le risorse in base a una combinazione di stati in vari facet di ricerca. Ad esempio, puoi cercare le risorse pubblicate approvate in un’attività di revisione e non scadute. Per cercare tali risorse, seleziona le opzioni appropriate nei facet di ricerca.

## Digital Rights Management in [!DNL Assets] {#digital-rights-management-in-assets-1}

La funzionalità DRM impone l’accettazione del contratto di licenza prima di poter scaricare una risorsa con licenza da [!DNL Assets].

Se selezioni una risorsa protetta e fai clic su **[!UICONTROL Scarica]**, viene reindirizzato a una pagina di licenza per accettare il contratto di licenza. Se non accetti il contratto di licenza, la **[!UICONTROL Scarica]** opzione non disponibile.

Se la selezione contiene più risorse protette, seleziona una risorsa alla volta, accetta il contratto di licenza e procedi con il download.

Un’attività è considerata protetta se una di queste condizioni è soddisfatta:

* Proprietà dei metadati della risorsa `xmpRights:WebStatement` punta al percorso della pagina che contiene il contratto di licenza per la risorsa.
* Valore della proprietà dei metadati della risorsa `adobe_dam:restrictions` è un HTML non elaborato che specifica il contratto di licenza.

>[!NOTE]
>
>La posizione `/etc/dam/drm/licences` è stato utilizzato per memorizzare le licenze nelle versioni precedenti di [!DNL Experience Manager]. La posizione è ora obsoleta. Se si creano o modificano pagine di licenza o si porta le pagine da precedenti [!DNL Experience Manager] versioni, Adobe consiglia di memorizzare tali risorse in `/apps/settings/dam/drm/licenses` o `/conf/*/settings/dam/drm/licenses` posizioni.

### Scaricare risorse protette da DRM {#downloading-drm-assets}

1. Nella vista a schede, seleziona le risorse da scaricare e fai clic su **[!UICONTROL Scarica]**.
1. Nella pagina **[!UICONTROL Gestione copyright]**, seleziona dall’elenco la risorsa da scaricare.
1. In [!UICONTROL Licenza] riquadro, scegli **[!UICONTROL Accetto]**. Accanto alla risorsa viene visualizzato un segno di spunta. Seleziona la **[!UICONTROL Scarica]** opzione .

   >[!NOTE]
   >
   >La **[!UICONTROL Scarica]** l’opzione è abilitata solo quando scegli di accettare il contratto di licenza per una risorsa protetta. Tuttavia, se la selezione include sia risorse protette che non protette, solo le risorse protette sono elencate nel riquadro e nella **[!UICONTROL Scarica]** per scaricare le risorse non protette, è disponibile l’opzione . Per accettare in contemporanea i contratti di licenza per più risorse protette, seleziona le risorse dall’elenco e fai clic su **[!UICONTROL Accetto]**.

1. Per scaricare la risorsa o i relativi rendering, seleziona **[!UICONTROL Scarica]** nella finestra di dialogo.

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cercare risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco di metadati](metadata-import-export.md)
