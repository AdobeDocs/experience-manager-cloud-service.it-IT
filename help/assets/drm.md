---
title: Digital Rights Management in [!DNL Assets]
description: Scopri come gestire gli stati di scadenza delle risorse e le informazioni per le risorse con licenza in [!DNL Experience Manager] come [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management,DRM
role: User,Admin
exl-id: fa5f94df-1c15-4593-afcb-1d24508da2bf
source-git-commit: f993148a9f678cfdaf0693e4964f02b9163cf2ff
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 2%

---

# Digital Rights Management per le risorse digitali {#digital-rights-management-in-assets}

Digital assets are often associated with a license that specifies the terms and the duration of use. Utilizzo della [!DNL Experience Manager] Platform consente di gestire in modo efficiente le informazioni sulla scadenza delle risorse e le informazioni sulla licenza.

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
1. For expired assets, the [!UICONTROL References] displays the expiry status as **[!UICONTROL Asset is Expired]**. Se la risorsa è scaduta, la [!UICONTROL Riferimenti] visualizza lo stato **[!UICONTROL Risorse secondarie scadute]**.

### Cercare risorse scadute {#search-expired-assets}

Per cercare una risorsa scaduta, incluse le risorse secondarie scadute, procedi come segue:

1. In the [!DNL Assets] console, click **[!UICONTROL Search]** in the toolbar and press `Enter`.

1. Fai clic sull’icona di Navigazione globale e seleziona la **[!UICONTROL Stato di scadenza]** opzione .

1. Seleziona **[!UICONTROL Scaduto]**. Nei risultati della ricerca vengono visualizzate le risorse scadute.

When you choose the **[!UICONTROL Expired]** option, the [!DNL Assets] console only displays the expired assets and subassets that are referenced by compound assets. The compound assets that reference expired subassets are not displayed immediately after the subassets expire. Instead, they are displayed after [!DNL Experience Manager] detects that they reference expired subassets the next time the scheduler executes.

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
* The maximum number of assets expired in one iteration of the scheduler is the value of the property `asset_expired_limit`.
* Per eseguire periodicamente il processo, imposta il valore della proprietà `cq.dam.expiry.notification.scheduler.istimebased` come `false` e imposta il valore della proprietà `cq.dam.expiry.notification.scheduler.period.rule` con tempo in secondi.

<!-- TBD: Web Console not available in CS.

1. Open [!DNL Experience Manager] Configuration Manager.
1. Choose **[!UICONTROL Adobe CQ DAM Expiry Notification]**. By default, **[!UICONTROL Time-based Scheduler]** is selected, which 

1.  For example, the example expression '0 0 0 &ast; &ast; ?' triggers the job at 0000 hrs.

1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

1. In the **[!UICONTROL Prior notification in seconds]** field, specify the time in seconds before the asset expiry when you want to receive a notification. If you are an administrator or the asset creator, you receive a message before the expiration of the asset. After the asset expiry, you receive another notification that confirms the expiration. In addition, the expired asset is deactivated.

1. Select **[!UICONTROL Save]**.
-->

## Asset states {#asset-states}

La [!DNL Assets] La console può visualizzare vari stati delle risorse. Depending on the current state of a particular asset, its card view displays a label that describes its state, for example, Expired, Published, Approved, Rejected, and so on.

1. In [!DNL Assets] interfaccia utente, seleziona una risorsa.

1. Seleziona **[!UICONTROL Pubblica]** dalla barra degli strumenti. Se non vedi [!UICONTROL Pubblica] nella barra degli strumenti, fai clic su **[!UICONTROL Altro]** sulla barra degli strumenti e individua **[!UICONTROL Pubblica]** opzione .

1. Scegli **[!UICONTROL Pubblica]** dal menu , quindi chiudi la finestra di dialogo di conferma.

1. Esci dalla modalità di selezione. The publication status for the asset appears at the bottom of the asset thumbnail in the card view. In the list view, the Published column displays the time when the asset was published.

1. Per visualizzare la pagina dei dettagli della relativa risorsa, nella [!DNL Assets] interfaccia, seleziona una risorsa e fai clic su **[!UICONTROL Proprietà]**.

1. In [!UICONTROL Avanzate] imposta una data di scadenza per la risorsa dalla **[!UICONTROL Scadenza]** campo .

1. Fai clic su **[!UICONTROL Salva]** quindi fai clic su **[!UICONTROL Chiudi]** per visualizzare la console Risorse .

1. Lo stato di pubblicazione della risorsa indica uno stato scaduto nella parte inferiore della miniatura della risorsa nella vista a schede. Nella vista a elenco, lo stato della risorsa viene visualizzato come **[!UICONTROL Scaduto]**.

1. In [!DNL Assets] console, seleziona una cartella e crea un’attività di revisione nella cartella.

1. Rivedi e approva/rifiuta le risorse nell’attività di revisione e fai clic su **[!UICONTROL Completa]**.

1. Passare alla cartella per la quale è stata creata l&#39;attività di revisione. Lo stato delle risorse approvate o rifiutate viene visualizzato nella parte inferiore della vista a schede. In the list view, the approval and expiry statuses are displayed in appropriate columns.

1. Per cercare le risorse in base al loro stato, fai clic su **[!UICONTROL Ricerca]** per visualizzare la barra di ricerca.

1. Seleziona `Return` e fai clic su [!DNL Experience Manager].

1. Nel pannello di ricerca, fai clic su **[!UICONTROL Stato di pubblicazione]** e seleziona **[!UICONTROL Pubblicato]** per cercare le risorse pubblicate in [!DNL Assets].

1. Per cercare le risorse approvate o rifiutate, seleziona **[!UICONTROL Stato di approvazione]** e selezionare l&#39;opzione appropriata.

1. Per cercare le risorse in base al loro stato di scadenza, seleziona **[!UICONTROL Stato di scadenza]** nel pannello di ricerca e seleziona l’opzione appropriata.

1. Puoi anche cercare le risorse in base a una combinazione di stati in vari facet di ricerca. Ad esempio, puoi cercare le risorse pubblicate approvate in un’attività di revisione e non scadute. To search such assets, select the appropriate options in the search facets.

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
   >The **[!UICONTROL Download]** option is enabled only when you choose to agree to the license agreement for a protected asset. Tuttavia, se la selezione include sia risorse protette che non protette, solo le risorse protette sono elencate nel riquadro e nella **[!UICONTROL Scarica]** per scaricare le risorse non protette, è disponibile l’opzione . Per accettare in contemporanea i contratti di licenza per più risorse protette, seleziona le risorse dall’elenco e fai clic su **[!UICONTROL Accetto]**.

1. To download the asset or its renditions, select **[!UICONTROL Download]** in the dialog.
