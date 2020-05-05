---
title: 'Adobe Experience Manager as a Cloud Service: note sulla versione 2020.4.0'
description: Note sulla versione 2020.4.0 di Experience Manager
translation-type: ht
source-git-commit: 98de3a6674aaef5228e96e0bf72e67de861f858e

---


# Note sulla versione 2020.4.0 di Adobe Experience Manager as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione di [!DNL Experience Manager] as a Cloud Service 2020.4.0.

## Data di rilascio {#release-date}

La data di rilascio per [!DNL Experience Manager] as a Cloud Service 2020.4.0 è il 9 aprile 2020.

## Novità di Assets {#assets}

Scopri nuove funzioni, miglioramenti e correzioni di bug per [!DNL Experience Manager Assets] e [!DNL Dynamic Media] nella versione corrente.

* [Brand Portal](https://docs.adobe.com/content/help/it-IT/experience-manager-brand-portal/using/home.html) supporta i casi di utilizzo della distribuzione delle risorse per Experience Manager Assets. Con [!DNL Brand Portal] le organizzazioni possono soddisfare le esigenze di marketing aziendali e distribuire in sicurezza le risorse approvate relative a prodotti e marchi, che potranno essere scaricate da agenzie esterne, partner, team interni e rivenditori.
   * La configurazione di [!DNL Brand Portal] viene completata tramite la console [!DNL Adobe I/O]. Consulta le informazioni per la [configurazione di Brand Portal](https://docs.adobe.com/content/help/it-IT/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html).
   * L’origine da Asset in [!DNL Brand Portal] non è ancora supportata con [!DNL Experience Manager] as a Cloud Service.

* [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html) v2.0 funziona con [!DNL Experience Manager] as a Cloud Service. [!DNL Adobe Asset Link] consente di ottimizzare la collaborazione tra creativi e professionisti del marketing nel processo di creazione dei contenuti mediante il collegamento di [!DNL Experience Manager Assets] con le app desktop di [!DNL Creative Cloud],[!DNL Adobe Photoshop], [!DNL Adobe Illustrator] e [!DNL Adobe InDesign] tramite il pannello in-app di [!DNL Asset Link].
   * [!DNL Experience Manager] è preconfigurato per [!DNL Adobe Asset Link], ciò consente una [configurazione semplificata](https://helpx.adobe.com/it/enterprise/using/configure-aem-assets-for-asset-link.html) e un’implementazione più rapida per i creativi.
   * [!DNL Asset Link] ora supporta una funzione per [passare a un altro ambiente in Experience Manager](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) che consente ai creativi di connettersi in modo semplice a un ambiente [!DNL Experience Manager] diverso. Questa funzione è utile, ad esempio, per i designer di un’agenzia che lavorano per più clienti utilizzando implementazioni diverse di [!DNL Experience Manager Assets].

* Gli utenti possono configurare [flussi di lavoro di post-elaborazione](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) da avviare automaticamente tramite l’interfaccia utente per le [!UICONTROL Proprietà] della cartella, nelle gerarchie di cartelle specifiche.
   * L’interfaccia utente per le [!UICONTROL Proprietà] della cartella è stata semplificata: la nuova scheda [!UICONTROL Elaborazione risorse] contiene il profilo di metadati, il profilo di elaborazione e la nuova configurazione del flusso di lavoro con avvio automatico.

      ![I profili di elaborazione possono essere facilmente applicati alle cartelle e tutte le risorse caricate nelle cartelle vengono elaborate utilizzando questi profili](/help/assets/assets/asset-processing-folder-properties.png)

   * L’opzione di rielaborazione delle risorse consente di selezionare uno specifico profilo di elaborazione con cui rielaborare le risorse selezionate dall’utente nelle sottocartelle.

      ![Rielaborazione di risorse selezionate mediante un profilo di elaborazione specifico](/help/assets/assets/fpo-existing-asset-reprocess.gif)

   * [!DNL Dynamic Media]: è stata aggiunta la configurazione di pubblicazione selettiva in modo che le risorse vengano pubblicate automaticamente solo per l’anteprima protetta. Inoltre, le risorse possono essere pubblicate in modo esplicito in Experience Manager senza pubblicare contenuti in DMS7 per la distribuzione nel dominio pubblico.

### Correzioni di bug {#assets-bug-fixes}

* Correzioni dei problemi relativi all’elaborazione delle risorse.
* Correzioni nella configurazione di [!DNL Dynamic Media] e nella pubblicazione delle risorse nel servizio di distribuzione di [!DNL Dynamic Media].

>[!MORELIKETHIS]
>
>* [Informazioni su Adobe Asset Link](https://www.adobe.com/creativecloud/business/enterprise/adobe-asset-link.html)
>* [Configurazione di Brand Portal](https://docs.adobe.com/content/help/it-IT/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)
>* [Configurazione di Experience Manager per l’utilizzo con Asset Link](https://helpx.adobe.com/it/enterprise/using/configure-aem-assets-for-asset-link.html)
>* [Creazione di un flusso di lavoro in Experience Manager utilizzando i microservizi delle risorse](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html#post-processing-workflows)


## Novità di Cloud Manager {#whats-new-cloud-manager}

* Gli URL dell’editore sono ora disponibili nella pagina Ambiente dell’interfaccia utente di Cloud Manager.
* Sono state apportate modifiche al sistema di navigazione per consentire agli utenti di modificare, cambiare o aggiungere un programma dalla pagina di panoramica di Cloud Manager.
* Sono state apportate modifiche per consentire all’utente di modificare il programma dalla scheda del programma nella pagina di destinazione di Cloud Manager.
* È stato introdotto il nuovo stato di pipeline “**In esecuzione**”, visualizzato per l’ambiente a cui la pipeline è associata.
* Sono stati introdotti miglioramenti nella pagina di esecuzione della pipeline, che ne facilitano la comprensione. Questi includono la visualizzazione del nome della pipeline (solo per pipeline non di produzione) e del tipo, oltre all’indicazione dello stato della pipeline (In corso, Annullato, Non riuscito).
* Sono state aggiunte descrizioni per migliorare l’esperienza utente e spiegare perché il pulsante Aggiungi programma/ambiente è disattivato.
* Gli ambienti con errore possono ora essere eliminati tramite l’interfaccia utente e l’API.
* Il processo utilizzato per generare password git è stato reso più flessibile per affrontare eventuali problemi nel livello di servizio sottostante.

### Correzioni di bug {#bug-fixes-cloud-manager}

* I collegamenti all’ambiente Stage nella pagina dei dettagli di esecuzione della pipeline non passavano alla posizione corretta in modo regolare.
* Singoli passaggi del processo di creazione dell’ambiente venivano interrotti per timeout prima del necessario, causando errori del processo.
* La configurazione Maven utilizzata nel contenitore di build è stata aggiornata per evitare deadlock durante il download dei metadati dell’artefatto.
* In alcuni casi, il passaggio di generazione dell’immagine non eseguiva il download dei pacchetti dei clienti.
* Alcune condizioni poco frequenti impedivano l’eliminazione degli ambienti.
* Le notifiche di Experience Cloud non venivano ricevute in modo costante.
