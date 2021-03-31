---
title: Digital Rights Management in [!DNL Assets]
description: Scopri come gestire gli stati di scadenza delle risorse e le informazioni per le risorse con licenza in [!DNL Experience Manager] come a [!DNL Cloud Service].
contentOwner: AG
feature: Gestione risorse, DRM
role: Business Practices, Amministratore
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 7%

---


# Digital Rights Management per le risorse {#digital-rights-management-in-assets}

Le risorse digitali sono spesso associate a una licenza che specifica i termini e la durata dell’utilizzo. Poiché [!DNL Adobe Experience Manager Assets] è completamente integrato con la piattaforma [!DNL Experience Manager], puoi gestire in modo efficiente le informazioni sulla scadenza delle risorse e gli stati delle risorse. È inoltre possibile associare le informazioni sulle licenze alle risorse.

## Scadenza risorsa {#asset-expiration}

La scadenza delle risorse è un modo efficace per applicare i requisiti di licenza per le risorse. In questo modo la risorsa pubblicata viene annullata quando scade, evitando così la possibilità di eventuali violazioni della licenza. Un utente senza autorizzazioni di amministratore non può modificare, copiare, spostare, pubblicare e scaricare una risorsa scaduta.

Puoi visualizzare lo stato di scadenza di una risorsa nei seguenti punti:

* **Vista** a schede: Per una risorsa scaduta, un flag sulla scheda indica che è scaduta.
* **Vista** a elenco: Per le risorse scadute, nella colonna  **** Statusvengono visualizzati i  **** caratteri Expiredbanner.
* **Timeline**: Puoi visualizzare lo stato di scadenza di una risorsa nella timeline. Seleziona la risorsa e scegli Timeline.
* **Barra** Riferimenti: Puoi anche visualizzare lo stato di scadenza delle risorse nella barra  **** Riferimenti. Gestisce gli stati di scadenza delle risorse e le relazioni tra le risorse composte e le risorse secondarie, le raccolte e i progetti a cui si fa riferimento.

1. Passa alla risorsa per la quale desideri visualizzare i riferimenti alle pagine web e alle risorse composte.
1. Seleziona la risorsa e fai clic sul logo [!DNL Experience Manager].
1. Scegli **[!UICONTROL Riferimenti]** dal menu .
1. Per le risorse scadute, nella barra Riferimenti viene visualizzato lo stato di scadenza **[!UICONTROL Risorsa scaduta]** nella parte superiore. Se la risorsa è scaduta, nella barra Riferimenti viene visualizzato lo stato **[!UICONTROL Risorse secondarie scadute]**.

### Cerca risorse scadute {#search-expired-assets}

Puoi cercare le risorse scadute, incluse le risorse secondarie scadute, nel pannello Ricerca.

1. Nella console [!DNL Assets], fai clic su **[!UICONTROL Cerca]** nella barra degli strumenti per visualizzare la casella di ricerca Omnisearch.

1. Con il cursore nella casella Omnisearch, selezionare il tasto `Enter` per visualizzare la pagina dei risultati della ricerca.

1. Fai clic sull’icona Navigazione globale per visualizzare il pannello Ricerca .

1. Tocca o fai clic sull’opzione **[!UICONTROL Stato scadenza]** per espanderla.

1. Selezionare **[!UICONTROL Scaduto]**. Le risorse scadute vengono visualizzate nei risultati della ricerca.

Quando scegli l’opzione **[!UICONTROL Expired]** , nella console [!DNL Assets] vengono visualizzate solo le risorse e le risorse secondarie scadute a cui fanno riferimento le risorse composte. Le risorse composte che fanno riferimento a risorse secondarie scadute non vengono visualizzate immediatamente dopo la scadenza delle risorse secondarie. Vengono invece visualizzati dopo che [!DNL Experience Manager] rileva che fanno riferimento a risorse secondarie scadute al successivo avvio della pianificazione.

Se modifichi la data di scadenza di una risorsa pubblicata a una data precedente al ciclo di pianificazione corrente, la pianificazione rileva comunque questa risorsa come una risorsa scaduta la prossima volta che viene eseguita e ne riflette lo stato di conseguenza. La data di scadenza di una risorsa viene visualizzata in modo diverso per gli utenti con diversi valori orari.

Inoltre, se un errore o un errore impedisce al programmatore di rilevare le risorse scadute nel ciclo corrente, lo scheduler riesamina tali risorse nel ciclo successivo e ne rileva lo stato scaduto.

Per abilitare la console [!DNL Assets] affinché visualizzi le risorse composte di riferimento insieme alle risorse secondarie scadute, configura un flusso di lavoro **[!UICONTROL Adobe CQ DAM Expiry Notification]** in [!DNL Experience Manager] Configuration Manager.

1. Apri [!DNL Experience Manager] Configuration Manager.
1. Scegli **[!UICONTROL Notifica di scadenza Adobe CQ DAM]**. Per impostazione predefinita, è selezionata l&#39;opzione **[!UICONTROL Utilità di pianificazione basata sul tempo]**, che consente di pianificare un processo per verificare in un momento specifico se una risorsa è scaduta per le risorse secondarie. Al termine del processo, le risorse con risorse secondarie scadute e risorse di riferimento vengono visualizzate come scadute nei risultati della ricerca.

1. Per eseguire il processo periodicamente, cancella il campo **[!UICONTROL Time Based Scheduler Rule (Regola modulo di pianificazione basato sul tempo)]** e modifica il tempo in secondi nel campo **[!UICONTROL Periodic Scheduler (Modulo di pianificazione periodica)]**. L’espressione di esempio ‘0 0 0 &amp;ast; &amp;ast; ?’ attiva il processo alle ore 00.

<!-- 1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

   >[!NOTE]
   >
   >Only the asset creator (the person who uploads a particular asset to AEM Assets) receives an email when the asset expires. See how to configure email notification for additional details around configuring email notifications at the overall AEM level.
-->

1. Nel campo **[!UICONTROL Notifica preventiva in secondi]** , specifica il tempo in secondi prima della scadenza di una risorsa quando desideri ricevere una notifica relativa alla scadenza. Gli amministratori o i creatori di risorse ricevono un messaggio prima della scadenza della risorsa che ti informa che la risorsa sta per scadere dopo il tempo specificato.

   Dopo la scadenza della risorsa, riceverai un’altra notifica che conferma la scadenza. Inoltre, le risorse scadute vengono disattivate.

1. Fai clic su **[!UICONTROL Salva]**.

## Stati delle risorse {#asset-states}

La console [!DNL Assets] può visualizzare vari stati delle risorse. A seconda dello stato corrente di una particolare risorsa, nella relativa vista a schede viene visualizzata un’etichetta che ne descrive lo stato, ad esempio Scaduto, Pubblicato, Approvato, Rifiutato e così via.

1. Nell’interfaccia utente di [!DNL Assets] , seleziona una risorsa.

1. Fai clic su **[!UICONTROL Pubblica]** nella barra degli strumenti. Se non trovi **Pubblica** sulla barra degli strumenti, fai clic su **[!UICONTROL Altro]** sulla barra degli strumenti e individua l&#39;opzione **[!UICONTROL Pubblica]** .

1. Scegli **[!UICONTROL Pubblica]** dal menu, quindi chiudi la finestra di dialogo di conferma.
1. Esci dalla modalità di selezione. Lo stato di pubblicazione della risorsa viene visualizzato nella parte inferiore della miniatura della risorsa nella vista a schede. Nella vista a elenco, la colonna Pubblicato visualizza l’ora in cui è stata pubblicata la risorsa.

1. Per visualizzare la pagina dei dettagli della risorsa, nell’interfaccia [!DNL Assets] seleziona una risorsa e fai clic su **[!UICONTROL Proprietà]**.

1. Nella scheda [!UICONTROL Avanzate] , imposta una data di scadenza per la risorsa dal campo **[!UICONTROL Scade]** .

1. Fai clic su **[!UICONTROL Salva]**, quindi fai clic su **[!UICONTROL Chiudi]** per visualizzare la console delle risorse.
1. Lo stato di pubblicazione della risorsa indica uno stato scaduto nella parte inferiore della miniatura della risorsa nella vista a schede. Nella vista a elenco, lo stato della risorsa viene visualizzato come **[!UICONTROL Scaduto]**.

1. Nella console [!DNL Assets], seleziona una cartella e crea un’attività di revisione sulla cartella.
1. Rivedi e approva/rifiuta le risorse nell’attività di revisione e fai clic su **[!UICONTROL Completa]**.
1. Passare alla cartella per la quale è stata creata l&#39;attività di revisione. Lo stato delle risorse approvate o rifiutate viene visualizzato nella parte inferiore della vista a schede. Nella vista a elenco, gli stati di approvazione e scadenza vengono visualizzati nelle colonne appropriate.

1. Per cercare le risorse in base al loro stato, fai clic su **[!UICONTROL Cerca]** per visualizzare la barra di ricerca Omnisearch.

1. Seleziona `Return` e fai clic su [!DNL Experience Manager] per visualizzare il pannello di ricerca.
1. Nel pannello di ricerca, fai clic su **[!UICONTROL Stato pubblicazione]** e seleziona **[!UICONTROL Pubblicato]** per cercare le risorse pubblicate in [!DNL Assets].

1. Fai clic su **[!UICONTROL Stato approvazione]** e fai clic sull&#39;opzione appropriata per cercare le risorse approvate o rifiutate.

1. Per cercare le risorse in base al loro stato di scadenza, seleziona **[!UICONTROL Stato scadenza]** nel pannello di ricerca e scegli l’opzione appropriata.

1. Puoi anche cercare le risorse in base a una combinazione di stati in vari facet di ricerca. Ad esempio, puoi cercare le risorse pubblicate che sono state approvate in un’attività di revisione e che non sono ancora scadute selezionando le opzioni appropriate nei facet di ricerca.

## Digital Rights Management in [!DNL Assets] {#digital-rights-management-in-assets-1}

Questa funzione impone l’accettazione del contratto di licenza prima di poter scaricare una risorsa con licenza da [!DNL Adobe Experience Manager Assets].

Se selezioni una risorsa protetta e fai clic su **[!UICONTROL Scarica]**, vieni reindirizzato a una pagina di licenza per accettare il contratto di licenza. Se non accetti il contratto di licenza, l&#39;opzione **[!UICONTROL Scarica]** non è disponibile.

Se la selezione contiene più risorse protette, seleziona una risorsa alla volta, accetta il contratto di licenza e procedi con il download.

Un’attività è considerata protetta se una di queste condizioni è soddisfatta:

* La proprietà metadati della risorsa `xmpRights:WebStatement` punta al percorso della pagina che contiene il contratto di licenza per la risorsa.
* Il valore della proprietà metadati risorsa `adobe_dam:restrictions` è un codice HTML non elaborato che specifica il contratto di licenza.

>[!NOTE]
>
>La posizione `/etc/dam/drm/licences` utilizzata per memorizzare le licenze nelle versioni precedenti di [!DNL Experience Manager] è obsoleta.
>
>Se crei o modifichi pagine di licenza o le porti dalle versioni precedenti di [!DNL Experience Manager], Adobe consiglia di memorizzarle in `/apps/settings/dam/drm/licenses` o `/conf/*/settings/dam/drm/licenses`.

### Scaricare risorse protette da DRM {#downloading-drm-assets}

1. Nella vista a schede, seleziona le risorse da scaricare e fai clic su **[!UICONTROL Scarica]**.
1. Nella pagina **[!UICONTROL Gestione copyright]**, seleziona dall’elenco la risorsa da scaricare.
1. Nel riquadro [!UICONTROL Licenza], scegli **[!UICONTROL Accetto]**. Accanto alla risorsa viene visualizzato un segno di spunta. Fai clic sull&#39;opzione **[!UICONTROL Scarica]** .

   >[!NOTE]
   >
   >L’opzione **[!UICONTROL Scarica]** è abilitata solo quando scegli di accettare il contratto di licenza per una risorsa protetta. Tuttavia, se la selezione include sia risorse protette che non protette, solo le risorse protette sono elencate nel riquadro e l’opzione **[!UICONTROL Scarica]** è abilitata per scaricare le risorse non protette. Per accettare in contemporanea i contratti di licenza per più risorse protette, seleziona le risorse dall’elenco e fai clic su **[!UICONTROL Accetto]**.

1. Nella finestra di dialogo, fai clic su **[!UICONTROL Scarica]** per scaricare la risorsa o le relative rappresentazioni.
