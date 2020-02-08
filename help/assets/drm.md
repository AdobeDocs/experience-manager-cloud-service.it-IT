---
title: Digital Rights Management in Adobe Experience Manager Assets
description: Scoprite come gestire gli stati di scadenza delle risorse e le informazioni per le risorse con licenza in AEM.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Gestione dei diritti digitali in Experience Manager Assets {#digital-rights-management-in-assets}

Le risorse digitali sono spesso associate a una licenza, che specifica i termini e la durata di utilizzo. Poiché Risorse Adobe Experience Manager (AEM) è completamente integrato con la piattaforma AEM, puoi gestire in modo efficiente le informazioni sulla scadenza delle risorse e gli stati delle risorse. Potete anche associare le informazioni sulla licenza alle risorse.

## Scadenza risorsa {#asset-expiration}

La scadenza delle risorse è un modo efficace per imporre i requisiti di licenza per le risorse. Garantisce che la risorsa pubblicata non venga pubblicata alla scadenza, evitando così la possibilità di eventuali violazioni della licenza. Un utente senza diritti di amministratore non può modificare, copiare, spostare, pubblicare e scaricare una risorsa scaduta.

Potete visualizzare lo stato di scadenza di una risorsa nei seguenti punti:

* **Vista** a schede: Per una risorsa scaduta, un flag sulla scheda indica che è scaduta.
* **Visualizzazione** elenco: Per le risorse scadute, nella colonna **[!UICONTROL Stato]** viene visualizzato il banner **[!UICONTROL Scaduto]** .
* **Timeline**: Potete visualizzare lo stato di scadenza di una risorsa nella timeline. Selezionate la risorsa e scegliete Timeline.
* **Barra** dei riferimenti: Potete inoltre visualizzare lo stato di scadenza delle risorse nella barra **[!UICONTROL Riferimenti]** . Gestisce gli stati di scadenza delle risorse e le relazioni tra le risorse composte e le risorse secondarie, le raccolte e i progetti a cui viene fatto riferimento.

1. Andate alla risorsa per la quale desiderate visualizzare il riferimento a pagine Web e risorse composte.
1. Selezionate la risorsa e toccate o fate clic sull’icona di navigazione globale.
1. Scegliete **[!UICONTROL Riferimenti]** dal menu.
1. Per le risorse scadute, nella barra laterale Riferimenti viene visualizzato lo stato di scadenza **[!UICONTROL Risorsa scaduto]** nella parte superiore. Se la risorsa è scaduta, nella barra laterale Riferimenti viene visualizzato lo stato Risorse secondarie scadute della **[!UICONTROL risorsa]**.

### Cercare le risorse scadute {#search-expired-assets}

Potete cercare le risorse scadute, comprese le risorse secondarie scadute, nel pannello Ricerca.

1. Nella console Risorse, fate clic sull’icona Ricerca nella barra degli strumenti per visualizzare la casella Ricerca Omni.

1. Con il cursore nella casella Cerca Omni, premi il tasto Invio per visualizzare la pagina Risultati ricerca.

1. Fate clic sull’icona GlobalNav per visualizzare il pannello di ricerca.

1. Tocca o fai clic sull’opzione Stato **** scadenza per espanderla.

1. Selezionare **[!UICONTROL Scaduto]**. Le risorse scadute vengono visualizzate nei risultati della ricerca.

Quando scegliete l’opzione **Scaduto** , nella console Risorse vengono visualizzate solo le risorse e le risorse secondarie scadute a cui fanno riferimento le risorse composte. Le risorse composte che fanno riferimento a risorse secondarie scadute non vengono visualizzate subito dopo la scadenza delle risorse secondarie. Vengono invece visualizzati dopo che Risorse AEM rileva che fanno riferimento a risorse secondarie scadute al successivo esecuzione del programma.

Se modificate la data di scadenza di una risorsa pubblicata in una data precedente al ciclo di pianificazione corrente, la pianificazione rileva comunque la risorsa come una risorsa scaduta al successivo esecuzione e ne riflette lo stato di conseguenza.

Inoltre, se un problema o un errore impedisce al pianificatore di rilevare le risorse scadute nel ciclo corrente, il pianificatore riesamina tali risorse nel ciclo successivo e ne rileva lo stato scaduto.

Per abilitare la console Risorse per visualizzare le risorse composte di riferimento insieme alle risorse secondarie scadute, configura un flusso di lavoro **Adobe CQ DAM Expiry Notification** in AEM Configuration Manager.

1. Apri Gestione configurazione AEM.
1. Scegliete **[!UICONTROL Adobe CQ DAM Expiry Notification]**. Per impostazione predefinita, è selezionata l’opzione Pianificatore **[!UICONTROL basato su]** tempo, che pianifica un processo per verificare in un momento specifico se una risorsa ha risorse secondarie scadute. Al termine del processo, le risorse con risorse secondarie scadute e risorse di riferimento vengono visualizzate come scadute nei risultati della ricerca.

1. Per eseguire il processo periodicamente, cancellare il campo Regola **[!UICONTROL pianificazione basata su]** tempo e modificare il tempo in secondi nel campo Programmazione **** periodica. Ad esempio, l&#39;espressione di esempio &#39;0 0 &amp;ast; &amp;ast; ?&#39; attiva il processo a 00 ore.
1. Selezionate **[!UICONTROL Invia e-mail]** per ricevere e-mail alla scadenza di una risorsa.

   >[!NOTE]
   >
   >Alla scadenza della risorsa, solo l’autore della risorsa (l’utente che carica una particolare risorsa in Risorse AEM) riceve un messaggio e-mail. Scopri come configurare la notifica e-mail per ulteriori dettagli sulla configurazione delle notifiche e-mail a livello globale di AEM.

1. Nel campo Notifica **[!UICONTROL precedente in secondi]** , specificate l’ora in secondi prima della scadenza di una risorsa quando desiderate ricevere una notifica relativa alla scadenza. Se siete un amministratore o creatore di risorse, riceverete un messaggio prima della scadenza della risorsa per informarvi che la risorsa sta per scadere dopo l’ora specificata.

   Dopo la scadenza della risorsa, riceverete un’altra notifica che conferma la scadenza. Inoltre, le risorse scadute sono disattivate.

1. Fai clic su **[!UICONTROL Salva]**.

## Stati risorsa {#asset-states}

La console Risorse di Adobe Experience Manager (AEM) Assets può visualizzare vari stati per le risorse. A seconda dello stato corrente di una particolare risorsa, nella vista a schede viene visualizzata un&#39;etichetta che ne descrive lo stato, ad esempio Scaduto, Pubblicato, Approvato, Rifiutato e così via.

1. Nell’interfaccia utente Risorse, seleziona una risorsa.

1. Tap/click the **[!UICONTROL Publish]** icon from the toolbar. Se l’icona **Pubblica** non è visibile sulla barra degli strumenti, toccate o fate clic su **[!UICONTROL Altro]** sulla barra degli strumenti e individuate l’icona **[!UICONTROL Pubblica]** .

1. Scegliete **[!UICONTROL Pubblica]** dal menu, quindi chiudete la finestra di dialogo di conferma.
1. Esci dalla modalità di selezione. Lo stato di pubblicazione della risorsa viene visualizzato nella parte inferiore della miniatura della risorsa nella vista a schede. Nella vista a elenco, la colonna Pubblicato mostra l’ora in cui la risorsa è stata pubblicata.

1. Nell’interfaccia utente Risorse, seleziona una risorsa e tocca o fai clic sull’icona **[!UICONTROL Proprietà]** per visualizzare la pagina dei dettagli della risorsa.

1. Nella scheda Avanzate, quindi imposta una data di scadenza per la risorsa dal campo **[!UICONTROL Scade]** in.

1. Fate clic su **[!UICONTROL Salva]** , quindi su **[!UICONTROL Chiudi]** per visualizzare la console Risorse.
1. Lo stato di pubblicazione della risorsa indica uno stato scaduto nella parte inferiore della miniatura della risorsa nella vista a schede. Nella vista a elenco, lo stato della risorsa viene visualizzato come **[!UICONTROL Scaduto]**.

1. Nella console Risorse, selezionate una cartella e create un’attività di revisione sulla cartella.
1. Rivedete e approvate/rifiutate le risorse nell’attività di revisione e fate clic su **[!UICONTROL Completato]**.
1. Passate alla cartella per la quale avete creato l&#39;attività di revisione. Lo stato delle risorse approvate/rifiutate viene visualizzato nella parte inferiore della vista a schede. Nella vista a elenco, gli stati di approvazione e scadenza sono visualizzati nelle colonne appropriate.

1. Per cercare le risorse in base al loro stato, toccate o fate clic sull’icona **[!UICONTROL Cerca]** per visualizzare la barra di ricerca Omnico.

1. Premi il tasto Invio, quindi tocca o fai clic sull’icona **[!UICONTROL GlobalNav]** per visualizzare il pannello Ricerca.
1. Nel pannello Ricerca, tocca o fai clic su Stato **** pubblicazione e seleziona **[!UICONTROL Pubblicato]** per cercare le risorse pubblicate in Risorse AEM.

1. Toccate/fate clic su Stato **** approvazione e fate clic sull&#39;opzione appropriata per cercare le risorse approvate o rifiutate.

1. Per cercare le risorse in base al loro stato di scadenza, selezionate Stato **** scadenza nel pannello di ricerca e scegliete l’opzione appropriata.

1. Potete anche cercare le risorse in base a una combinazione di stati in vari facet di ricerca. Ad esempio, potete cercare le risorse pubblicate che sono state approvate in un’attività di revisione e che non sono ancora scadute selezionando le opzioni appropriate nei facet di ricerca.

## Gestione dei diritti digitali in Experience Manager Assets {#digital-rights-management-in-assets-1}

Questa funzione applica l’accettazione del contratto di licenza prima che possiate scaricare una risorsa con licenza da Risorse Adobe Experience Manager (AEM).

Se selezionate una risorsa protetta e fate clic sull&#39;icona **[!UICONTROL Scarica]** , verrete reindirizzati a una pagina di licenza in cui accettate il contratto di licenza. Se non accettate il contratto di licenza, il pulsante **[!UICONTROL Scarica]** è disattivato.

Se la selezione contiene più risorse protette, selezionate una risorsa alla volta, accettate il contratto di licenza e continuate a scaricare la risorsa.

Una risorsa è considerata protetta se una delle seguenti condizioni è soddisfatta:

* La proprietà dei metadati della risorsa `xmpRights:WebStatement` indica il percorso della pagina CQ che contiene il contratto di licenza per la risorsa.
* Il valore della proprietà di metadati della risorsa `adobe_dam:restrictions` è un codice HTML non elaborato che specifica il contratto di licenza.

>[!NOTE]
>
>Il percorso `/etc/dam/drm/licences` utilizzato per memorizzare le licenze nelle versioni precedenti di AEM non è più valido.
>
>Se create o modificate le pagine delle licenze o le rimuovete dalle precedenti versioni di AEM, Adobe consiglia di memorizzarle in `/apps/settings/dam/drm/licenses` o `/conf/*/settings/dam/drm/licenses`.

### Scaricare risorse DRM {#downloading-drm-assets}

1. Nella vista Scheda, selezionate le risorse da scaricare e fate clic sull’icona **[!UICONTROL Scarica]** .
1. Nella pagina Gestione **** copyright, selezionate dall’elenco la risorsa da scaricare.
1. Nel riquadro Licenza, scegliere **[!UICONTROL Accetto]**. Accanto alla risorsa per la quale accettate il contratto di licenza viene visualizzato un segno di spunta. Toccate o fate clic sul pulsante **[!UICONTROL Scarica]** .

   >[!NOTE]
   >
   >Il pulsante **[!UICONTROL Scarica]** è attivato solo quando decidi di accettare il contratto di licenza per una risorsa protetta. Tuttavia, se la selezione include sia risorse protette che risorse non protette, nel riquadro a sinistra vengono elencate solo le risorse protette e il pulsante **[!UICONTROL Scarica]** consente di scaricare le risorse non protette. Per accettare simultaneamente contratti di licenza per più risorse protette, selezionate le risorse dall’elenco e scegliete **[!UICONTROL D’accordo]**.

1. Nella finestra di dialogo, toccate o fate clic su **[!UICONTROL Scarica]** per scaricare la risorsa o le relative rappresentazioni.
