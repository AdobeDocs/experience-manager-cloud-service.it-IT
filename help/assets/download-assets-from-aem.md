---
title: Scaricare le risorse
description: Scaricare risorse da [!DNL Adobe Experience Manager Assets] e abilitare o disabilitare la funzionalità di download.
contentOwner: Vishabh Gupta
feature: Asset Management
role: User
exl-id: f68b03ba-4ca1-4092-b257-16727fb12e13
source-git-commit: d25d433203b8ec6787dec87a9ec35092a247096e
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 6%

---

# Scaricare risorse da [!DNL Adobe Experience Manager] {#download-assets-from-aem}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/download-assets-from-aem.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

Puoi scaricare risorse, incluse le rappresentazioni statiche e dinamiche. In alternativa, puoi inviare e-mail con collegamenti alle risorse direttamente da [!DNL Adobe Experience Manager Assets]. Le risorse scaricate sono incluse in un file ZIP. <!-- The compressed ZIP file has a maximum file size of 1 GB for the export job. A maximum of 500 total assets per export job are allowed. -->

<!--
>[!NOTE]
>
>Recipients of emails must be members of the `dam-users` group to access the ZIP download link in the email message. To be able to download the assets, the members must have permissions to launch workflows that trigger downloading of assets.
-->

Non è possibile scaricare i seguenti tipi di risorse: Set di immagini, Set 360 gradi, Set di file multimediali diversi e Set carosello.

Puoi scaricare le risorse da Experience Manager utilizzando i seguenti metodi:

<!-- * [Link Share](#link-share-download) -->

* [Interfaccia utente di Experience Manager](#download-assets)
* [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
* [App desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets)

## Scaricare le risorse tramite [!DNL Experience Manager] Interfaccia {#download-assets}

Experience Manager ottimizza l’esperienza di download in base alla quantità e alle dimensioni della risorsa. I file più piccoli vengono scaricati dall’interfaccia utente in tempo reale. [!DNL Experience Manager] scarica direttamente le richieste di singole risorse per il file originale, anziché racchiudere le singole risorse in un archivio ZIP per velocizzare i download. Experience Manager supporta i download di grandi dimensioni con richieste asincrone. Le richieste di download di dimensioni superiori a 100 GB vengono suddivise in più archivi ZIP con una dimensione massima di 100 GB ciascuno.

Per impostazione predefinita, [!DNL Experience Manager] attiva una notifica in [[!DNL Experience Manager] Casella in entrata](/help/sites-cloud/authoring/getting-started/inbox.md) al momento della generazione di un archivio di download.

![Notifica casella in entrata](assets/inbox-notification-for-large-downloads.png)


### Abilitare le notifiche e-mail per i download di grandi dimensioni {#enable-emails-for-large-downloads}

I download asincroni vengono attivati in uno dei seguenti casi:

* Se il numero delle attività è superiore a dieci
* Se la dimensione del download è superiore a 100 MB
* Se la preparazione del download richiede più di 30 secondi

Mentre il download asincrono viene eseguito nel backend, l’utente può continuare a esplorare e lavorare ulteriormente in Experience Manager. Oltre alle notifiche della casella in entrata dell’Experience Manager, Experience Manager può inviare e-mail per avvisare l’utente al termine del processo di download. Per abilitare questa funzione, gli amministratori possono configurare il servizio e-mail tramite [configurazione di una connessione al server SMTP](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html#sending-email).

Una volta configurato il servizio e-mail, gli amministratori e gli utenti possono abilitare le notifiche e-mail dall’interfaccia di Experience Manager.

Per abilitare le notifiche e-mail:

1. Accedi a [!DNL Experience Manager Assets].
1. Fai clic sull’icona utente in alto a destra, quindi fai clic su **[!UICONTROL Le mie preferenze]** per aprire la finestra Preferenze utente.
1. Seleziona la **[!UICONTROL Notifiche e-mail per il download delle risorse]** e fai clic su **[!UICONTROL Accetta]**.

   ![enable-email-notifications-for-large-downloads](/help/assets/assets/enable-email-for-large-downloads.png)


Per scaricare le risorse, effettua le seguenti operazioni:

1. In entrata [!DNL Experience Manager] interfaccia utente, fai clic su **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. Passa alle risorse da scaricare. Seleziona la cartella o una o più risorse all’interno della cartella. Sulla barra degli strumenti, fai clic su **[!UICONTROL Scarica]**.

   ![Opzioni disponibili per il download di risorse da [!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)

1. Nella finestra di dialogo Scarica selezionare le opzioni di download desiderate.

   | Opzione di download | Descrizione |
   |---|---|
   | **[!UICONTROL Crea una cartella separata per ogni risorsa]** | Seleziona questa opzione per creare una cartella per ogni risorsa contenente tutte le relative rappresentazioni scaricate. Se non è selezionata, ogni risorsa (e le relative rappresentazioni se sono selezionate per il download) è contenuta nella cartella principale dell’archivio generato. |
   | **[!UICONTROL E-mail]** | Seleziona questa opzione per inviare una notifica e-mail (contenente un collegamento al download) a un altro utente. L&#39;utente destinatario deve essere membro di `dam-users` gruppo. I modelli di e-mail standard sono disponibili nelle seguenti posizioni:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> I modelli personalizzati durante la distribuzione sono disponibili nelle posizioni seguenti: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Puoi memorizzare modelli personalizzati specifici del tenant nelle seguenti posizioni:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Risorsa/e]** | Seleziona questa opzione per scaricare la risorsa nella sua forma originale.<br>L’opzione Risorse secondarie è disponibile se la risorsa originale contiene risorse secondarie. |
   | **[!UICONTROL Rappresentazione/i]** | Una rappresentazione è la rappresentazione binaria di una risorsa. Le risorse hanno una rappresentazione primaria, quella del file caricato. Possono avere un numero qualsiasi di rappresentazioni. <br> Con questa opzione, puoi selezionare le rappresentazioni da scaricare. Le rappresentazioni disponibili dipendono dalla risorsa selezionata. |
   | **[!UICONTROL Ritagli avanzati]** | Seleziona questa opzione per scaricare tutte le rappresentazioni con ritaglio avanzato della risorsa selezionata da [!DNL Experience Manager]. Nel computer locale viene creato e scaricato un file zip con le rappresentazioni di Ritaglio avanzato. |
   | **[!UICONTROL Rappresentazioni dinamiche]** | Selezionare questa opzione per generare in tempo reale una serie di rappresentazioni alternative. Quando si seleziona questa opzione, si selezionano anche le copie trasformate che si desidera creare in modo dinamico selezionandole dalla [Predefinito immagine](/help/assets/dynamic-media/image-presets.md) elenco. <br>Inoltre, è possibile selezionare le dimensioni e l&#39;unità di misura, il formato, lo spazio colore, la risoluzione ed eventuali modificatori di immagine opzionali, ad esempio l&#39;inversione dell&#39;immagine. L’opzione è disponibile solo se [!DNL Dynamic Media] abilitato. |

1. Nella finestra di dialogo, fai clic su **[!UICONTROL Scarica]**.

   Se la notifica e-mail è abilitata per i download di grandi dimensioni, nella casella in entrata viene visualizzato un messaggio e-mail contenente l’URL di download della cartella zip archiviata. Fai clic sul collegamento di download dall’e-mail per scaricare l’archivio zip.

   ![notifiche e-mail per download di grandi dimensioni](/help/assets/assets/email-for-large-notification.png)

   Puoi anche visualizzare la notifica nel tuo [!DNL Experience Manager] Casella in entrata.

   ![casella in entrata-notifiche-per-download di grandi dimensioni](/help/assets/assets/inbox-notification-for-large-downloads.png)

## Scaricare le risorse condivise tramite la condivisione di collegamenti {#link-share-download}

La condivisione delle risorse tramite un collegamento è un modo pratico per renderlo disponibile agli utenti interessati senza dover accedere a [!DNL Assets]. Consulta [Funzionalità di condivisione collegamenti](/help/assets/share-assets.md#sharelink).

Quando gli utenti scaricano risorse da collegamenti condivisi, [!DNL Assets] utilizza un servizio asincrono che offre download più rapidi e ininterrotti. Le risorse da scaricare vengono accodate in background in una casella in entrata in archivi ZIP di dimensioni file gestibili. Per i download di dimensioni maggiori, il download viene suddiviso in file da 100 GB.

Il [!UICONTROL Casella in entrata download] visualizza lo stato di elaborazione di ciascun archivio. Una volta completata l’elaborazione, puoi scaricare gli archivi dalla casella in entrata.

![Casella in entrata download](assets/link-sharing-download-inbox.png)

## Abilita servlet di download risorse {#enable-asset-download-servlet}

Il servlet predefinito in [!DNL Experience Manager] consente agli utenti autenticati di inviare richieste di download simultanee di grandi dimensioni e arbitrarie per creare file ZIP di risorse. La preparazione del download può avere implicazioni sulle prestazioni o può addirittura sovraccaricare il server e la rete. Per mitigare tali potenziali rischi di tipo DoS causati da questa funzione, `AssetDownloadServlet` Il componente OSGi è disabilitato per le istanze di pubblicazione. Se non hai bisogno della funzione di download nelle istanze di authoring, disabilita il servlet in Author.

Per consentire il download di risorse dal DAM, ad esempio quando utilizzi qualcosa come Asset Share Commons o un’altra implementazione simile a un portale, abilita manualmente il servlet tramite una configurazione OSGi. L’Adobe consiglia di impostare la dimensione di download consentita il più bassa possibile senza influire sui requisiti di download giornalieri. Un valore elevato può influire sulle prestazioni.

1. Crea una cartella con una convenzione di denominazione che esegua il targeting della modalità di esecuzione di pubblicazione, ovvero `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. Nella cartella di configurazione, crea un nuovo file di tipo `nt:file` denominato `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Popolare `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` con quanto segue. Imposta una dimensione massima (in byte) per il download come valore `asset.download.prezip.maxcontentsize`. L’esempio seguente configura la dimensione massima del download ZIP a un massimo di 100 KB.

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Disabilita servlet di download risorse {#disable-asset-download-servlet}

Se non hai bisogno della funzionalità di download, disattiva il servlet per evitare rischi di tipo DoS. Il `Asset Download Servlet` può essere disabilitato su un [!DNL Experience Manager] crea e pubblica le istanze aggiornando la configurazione di dispatcher per bloccare eventuali richieste di download di risorse. Il servlet può anche essere disabilitato manualmente tramite la console OSGi direttamente.

1. Per bloccare le richieste di download di risorse tramite una configurazione del dispatcher, modifica `dispatcher.any` e aggiungi una nuova regola al [sezione filtro](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring).

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

## Rappresentazione OnTime o OffTime {#on-off-time-rendition}

Per attivare `OnOffTimeAssetAccessFilter` servizio, è necessario creare una configurazione OSGi. Questo servizio consente di bloccare l’accesso alle rappresentazioni e ai metadati, oltre che alla risorsa stessa, in base alle impostazioni di ora di attivazione/disattivazione. La configurazione OSGi deve essere per `com.day.cq.dam.core.impl.servlet.OnOffTimeAssetAccessFilter`. Effettua le seguenti operazioni:

1. Nel codice del progetto in Git, crea un file di configurazione in `/apps/system/config/com.day.cq.dam.core.impl.servlet.OnOffTimeAssetAccessFilter.cfg.json`. Il file deve contenere `{}` come contenuto, a indicare una configurazione OSGi vuota per il componente OSGi corrispondente. Questa azione abilita il servizio.
1. Distribuisci il codice, inclusa la nuova configurazione, tramite [!DNL Cloud Manager].
1. Una volta implementati, i rendering e i metadati sono accessibili in base alle impostazioni di orario di attivazione/disattivazione delle risorse. Se la data o l’ora corrente cade prima dell’ora di attivazione o dopo l’ora di disattivazione, viene visualizzato un messaggio di errore.
Per ulteriori dettagli sull’aggiunta di una configurazione OSGi vuota, consulta [guida](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=en).

## Suggerimenti e limitazioni {#tips-limitations}

* se si scarica una cartella vuota, [!DNL Experience Manager] trasmette un messaggio di operazione riuscita della creazione di un archivio ZIP, ma l’archivio non viene creato.

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi metadati](metadata-schemas.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [Scaricare risorse protette DRM](drm.md)
>* [Scaricare risorse utilizzando l’app desktop Experience Manager su desktop Win o Mac](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Scaricare risorse tramite Adobe Assets Link dalle app Adobe Creative Cloud supportate](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html)
