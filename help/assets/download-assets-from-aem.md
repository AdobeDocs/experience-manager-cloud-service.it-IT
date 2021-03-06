---
title: Scaricare le risorse
description: Scaricare le risorse da [!DNL Adobe Experience Manager Assets] e abilitare o disabilitare la funzionalit√† di download.
contentOwner: Vishabh Gupta
feature: Asset Management
role: User
exl-id: f68b03ba-4ca1-4092-b257-16727fb12e13
source-git-commit: cf6cfb38a43004c8ac0c1d1e99153335a47860a8
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 4%

---

# Scaricare le risorse da [!DNL Adobe Experience Manager] {#download-assets-from-aem}

Puoi scaricare le risorse, compresi i rendering statici e dinamici. In alternativa, puoi inviare e-mail con collegamenti alle risorse direttamente da [!DNL Adobe Experience Manager Assets]. Le risorse scaricate sono raggruppate in un file ZIP. <!-- The compressed ZIP file has a maximum file size of 1 GB for the export job. A maximum of 500 total assets per export job are allowed. -->

<!--
>[!NOTE]
>
>Recipients of emails must be members of the `dam-users` group to access the ZIP download link in the email message. To be able to download the assets, the members must have permissions to launch workflows that trigger downloading of assets.
-->

Non √® possibile scaricare i tipi di risorse Set immagini, Set 360 gradi, Set di file multimediali diversi e Set carosello.

Per scaricare le risorse di Experience Manager, utilizza i seguenti metodi:

<!-- * [Link Share](#link-share-download) -->

* [Interfaccia utente di Experience Manager](#download-assets)
* [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
* [App desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets)

## Scaricare le risorse utilizzando [!DNL Experience Manager] interfaccia {#download-assets}

Il servizio di download asincrono fornisce un framework per il download senza soluzione di continuit√† delle risorse di grandi dimensioni. Il download consente di archiviare file di dimensioni superiori a 100 GB in pi√Ļ archivi zip con dimensioni massime di 100 GB ciascuno. Questi possono essere scaricati singolarmente. I file pi√Ļ piccoli vengono scaricati dall‚Äôinterfaccia utente in tempo reale. [!DNL Experience Manager] non archivia i download di singole risorse in cui viene scaricato il file originale. Questa funzionalit√† consente download pi√Ļ rapidi.

Per impostazione predefinita, [!DNL Experience Manager] attiva una notifica al completamento del flusso di lavoro di download. La notifica di download viene visualizzata nella  [[!DNL Experience Manager] Inbox](/help/sites-cloud/authoring/getting-started/inbox.md).

![Notifica casella in entrata](assets/inbox-notification-for-large-downloads.png)


### Abilita notifiche e-mail per download di grandi dimensioni {#enable-emails-for-large-downloads}

I download asincroni vengono attivati in uno dei seguenti casi:

* Se ci sono pi√Ļ di dieci risorse
* Se la dimensione del download √® superiore a 100 MB
* Se il download richiede pi√Ļ di 30 secondi per prepararsi

Mentre il download asincrono viene eseguito sul backend , l‚Äôutente pu√≤ continuare a esplorare e lavorare ulteriormente in Experience Manager. √ą necessario un meccanismo preconfigurato per informare l‚Äôutente al termine del processo di download. Per raggiungere questo obiettivo, gli amministratori possono configurare il servizio e-mail configurando un server SMTP. Vedi [configura servizio posta](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html#sending-email).

Una volta configurato il servizio e-mail, gli amministratori e gli utenti possono abilitare le notifiche e-mail dall‚Äôinterfaccia di Experience Manager.

Per abilitare le notifiche e-mail:

1. Accedi a [!DNL Experience Manager Assets].
1. Fai clic sull‚Äôicona utente nell‚Äôangolo in alto a destra, quindi fai clic su **[!UICONTROL Preferenze]**. Viene visualizzata la finestra Preferenze utente.
1. Seleziona la **[!UICONTROL Notifiche e-mail per il download delle risorse]** e fai clic su **[!UICONTROL Accetta]**.

   ![enable-email-notifications-for-large-downloads](/help/assets/assets/enable-email-for-large-downloads.png)


Per scaricare le risorse, effettua le seguenti operazioni:

1. In [!DNL Experience Manager] interfaccia utente, fai clic su **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. Passa alle risorse da scaricare. Seleziona la cartella o seleziona una o pi√Ļ risorse all‚Äôinterno della cartella. Sulla barra degli strumenti, fai clic su **[!UICONTROL Scarica]**.

   ![Opzioni disponibili durante il download delle risorse da [!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)

1. Nella finestra di dialogo scarica selezionare le opzioni di download desiderate.

   | Opzione di download | Descrizione |
   |---|---|
   | **[!UICONTROL Crea una cartella separata per ogni risorsa]** | Seleziona questa opzione per includere ogni risorsa scaricata, incluse le risorse in cartelle secondarie nidificate sotto la cartella padre della risorsa, in un‚Äôunica cartella sul computer locale. Quando questa opzione √® *not* seleziona, per impostazione predefinita, la gerarchia delle cartelle viene ignorata e tutte le risorse vengono scaricate in una cartella del computer locale. |
   | **[!UICONTROL E-mail]** | Seleziona questa opzione per inviare una notifica e-mail (contenente un collegamento al download) a un altro utente. L&#39;utente destinatario deve essere membro del gruppo `dam-users` gruppo. I modelli e-mail standard sono disponibili nelle seguenti posizioni:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> I modelli personalizzati durante la distribuzione sono disponibili nelle seguenti posizioni: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>√ą possibile archiviare modelli personalizzati specifici per il tenant nelle seguenti posizioni:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Risorsa/e]** | Seleziona questa opzione per scaricare la risorsa nel modulo originale senza rendering.<br>L‚Äôopzione Risorse secondarie √® disponibile se la risorsa originale include risorse secondarie. |
   | **[!UICONTROL Rappresentazione/i]** | Rappresentazione binaria di una risorsa. Le risorse hanno una rappresentazione principale, ossia quella del file caricato. Possono avere diverse rappresentazioni. <br> Con questa opzione, puoi selezionare le rappresentazioni da scaricare. Le rappresentazioni disponibili dipendono dalla risorsa selezionata. |
   | **[!UICONTROL Ritagli avanzati]** | Seleziona questa opzione per scaricare tutte le rappresentazioni di ritaglio avanzato della risorsa selezionata dall‚Äôinterno di [!DNL Experience Manager]. Viene creato e scaricato nel computer locale un file zip con le rappresentazioni di ritaglio avanzato. |
   | **[!UICONTROL Rappresentazioni dinamiche]** | Seleziona questa opzione per generare una serie di rappresentazioni alternative in tempo reale. Quando selezioni questa opzione, selezioni anche le rappresentazioni che desideri creare in modo dinamico selezionando dalla [Predefinito immagine](/help/assets/dynamic-media/image-presets.md) elenco. <br>√ą inoltre possibile selezionare le dimensioni e l&#39;unit√† di misura, il formato, lo spazio colore, la risoluzione e qualsiasi modificatore di immagine opzionale, ad esempio l&#39;inversione dell&#39;immagine. L‚Äôopzione √® disponibile solo se √® disponibile [!DNL Dynamic Media] abilitato. |

1. Nella finestra di dialogo, fai clic su **[!UICONTROL Scarica]**.

   Se la notifica e-mail √® abilitata per i download di grandi dimensioni, nella casella in entrata viene visualizzato un messaggio e-mail contenente l‚ÄôURL di download della cartella zip archiviata. Fai clic sul collegamento di download dall&#39;e-mail per scaricare la cartella zip.

   ![e-mail-notifications-for-large-downloads](/help/assets/assets/email-for-large-notification.png)

   Puoi anche visualizzare la notifica nel tuo [!DNL Experience Manager] Casella in entrata.

   ![inbox-notifications-for-large-downloads](/help/assets/assets/inbox-notification-for-large-downloads.png)

## Scaricare le risorse condivise tramite la condivisione dei collegamenti {#link-share-download}

La condivisione di risorse tramite un collegamento √® un modo conveniente per renderle disponibili alle persone interessate senza che queste debbano accedere a [!DNL Assets]. Vedi [Funzionalit√† Condivisione collegamenti](/help/assets/share-assets.md#sharelink).

Quando gli utenti scaricano risorse dai collegamenti condivisi, [!DNL Assets] utilizza un servizio asincrono che offre download pi√Ļ rapidi e ininterrotti. Le risorse da scaricare vengono messe in coda in background in una casella in entrata in archivi ZIP di dimensioni file gestibili. Per i download di grandi dimensioni, il download viene suddiviso in file di dimensioni pari a 100 GB.

La [!UICONTROL Scarica casella in entrata] visualizza lo stato di elaborazione di ciascun archivio. Una volta completata l‚Äôelaborazione, puoi scaricare gli archivi dalla casella in entrata.

![Scarica casella in entrata](assets/link-sharing-download-inbox.png)

## Abilita il servlet di download delle risorse {#enable-asset-download-servlet}

Il servlet predefinito in [!DNL Experience Manager] consente agli utenti autenticati di emettere richieste di download simultanee di grandi dimensioni arbitrarie per creare file ZIP di risorse. La preparazione del download pu√≤ avere implicazioni di prestazioni o pu√≤ anche sovraccaricare il server e la rete. Per attenuare tali rischi potenziali simili a quelli di DoS causati da questa funzione, `AssetDownloadServlet` Il componente OSGi √® disabilitato per le istanze di pubblicazione. Se non hai bisogno della funzione di download sulle istanze dell&#39;autore, disattiva il servlet sull&#39;autore.

Per consentire il download delle risorse dal tuo DAM, ad esempio quando utilizzi qualcosa come Asset Share Commons o un‚Äôaltra implementazione simile a un portale, abilita manualmente il servlet tramite una configurazione OSGi. L‚ÄôAdobe consiglia di impostare la dimensione del download consentito il pi√Ļ possibile bassa senza influire sui requisiti di download giornalieri. Un valore elevato pu√≤ influire sulle prestazioni.

1. Crea una cartella con una convenzione di denominazione che esegue il targeting della modalit√† di esecuzione di pubblicazione, ovvero `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. Nella cartella di configurazione, crea un nuovo file di tipo `nt:file` denominato `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Popolare `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` con le seguenti caratteristiche. Imposta una dimensione massima (in byte) per il download come valore di `asset.download.prezip.maxcontentsize`. L&#39;esempio seguente configura la dimensione massima del download ZIP in modo che non superi 100 kB.

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Disattiva il servlet di download delle risorse {#disable-asset-download-servlet}

Se non hai bisogno della funzionalit√† di download, disattiva il servlet per evitare rischi simili a quelli di DoS. La `Asset Download Servlet` pu√≤ essere disabilitato su un [!DNL Experience Manager] crea e pubblica le istanze aggiornando la configurazione del dispatcher per bloccare eventuali richieste di download delle risorse. Il servlet pu√≤ anche essere disabilitato manualmente tramite la console OSGi direttamente.

1. Per bloccare le richieste di download delle risorse tramite una configurazione del dispatcher, modifica la `dispatcher.any` e aggiungi una nuova regola al [sezione filtro](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring).

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

## Suggerimenti e limitazioni {#tips-limitations}

* se si scarica una cartella vuota, [!DNL Experience Manager] trasmette un messaggio di operazione riuscita della creazione di un archivio ZIP, ma l‚Äôarchivio non viene creato.

>[!MORELIKETHIS]
>
>* [Scaricare risorse protette DRM](drm.md)
>* [Scaricare risorse utilizzando l‚Äôapp desktop Experience Manager su desktop Win o Mac](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Scaricare le risorse utilizzando il collegamento Risorse di Adobe dalle app Adobe Creative Cloud supportate](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html)

