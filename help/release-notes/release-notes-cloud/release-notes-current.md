---
title: Adobe Experience Manager come servizio Cloud - Note sulla versione 2020.4.0
description: Note sulla versione di Experience Manager per la versione 2020.4.0
translation-type: tm+mt
source-git-commit: 49137535f4f6a6b62e697de6a7a9934f5b861bbc

---


# Release Notes for Adobe Experience Manager as a Cloud Service 2020.4.0 {#release-notes}

The following section outlines the general release notes for [!DNL Experience Manager] as a Cloud Service 2020.4.0.

## Release Date {#release-date}

La data di rilascio per [!DNL Experience Manager] il servizio cloud 2020.4.0 è il 9 aprile 2020.

## What&#39;s New in Assets {#assets}

Scopri nuove funzioni, miglioramenti e correzioni di bug per [!DNL Experience Manager Assets] e [!DNL Dynamic Media] nella versione corrente.

* [Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) supporta i casi di utilizzo della distribuzione delle risorse per Experience Manager Assets. [!DNL Brand Portal]Con le organizzazioni possono soddisfare le loro esigenze di marketing e distribuire in sicurezza le risorse approvate relative a prodotti e marchi, che potranno essere scaricate da agenzie esterne, partner, team interni e rivenditori.
   * [!DNL Brand Portal] la configurazione è completata tramite [!DNL Adobe I/O] la console.
   * L&#39;origine delle risorse in non [!DNL Brand Portal] è ancora supportata con [!DNLEExperience Manager] come servizio cloud.

* [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html) v2.0 funziona con [!DNL Experience Manager] un servizio cloud. [!DNL Adobe Asset Link] ottimizza la collaborazione tra creativi e professionisti del marketing nel processo di creazione dei contenuti, collegandosi [!DNL Experience Manager Assets] con [!DNL Creative Cloud] le app desktop [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]e [!DNL Adobe InDesign] tramite il [!DNL Asset Link] pannello in-app.
   * [!DNL Experience Manager] è preconfigurata per [!DNL Adobe Asset Link], con conseguente [facile configurazione](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html) e implementazione più rapida per i creativi professionisti.
   * [!DNL Asset Link] ora supporta uno switcher [ambiente](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) Experience Manager che consente agli utenti creativi di connettersi facilmente a un altro [!DNL Experience Manager] ambiente. Un esempio in cui questa funzionalità è utile è rappresentato dai designer di agenzie che lavorano con più client utilizzando [!DNL Experience Manager Assets] distribuzioni diverse.

* Gli utenti possono configurare i flussi di lavoro [di](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) post-elaborazione per avviare automaticamente l’interfaccia utente [!UICONTROL Proprietà] cartella per le gerarchie di cartelle specifiche.
   * L’interfaccia utente [!UICONTROL Proprietà] cartella è semplificata e la nuova scheda Elaborazione  risorse contiene il profilo di metadati, il profilo di elaborazione e la nuova configurazione del flusso di lavoro con avvio automatico.
   * La finestra di dialogo di rielaborazione delle risorse consente di selezionare un profilo di elaborazione specifico e di decidere di rielaborarlo nelle sottocartelle.
   * [!DNL Dynamic Media]: È stata aggiunta la configurazione di pubblicazione selettiva in modo che le risorse vengano pubblicate automaticamente solo per l’anteprima protetta. Inoltre, le risorse possono essere pubblicate in modo esplicito in Experience Manager senza pubblicare contenuti in DMS7 per la distribuzione nel dominio pubblico.

### Correzioni di bug {#assets-bug-fixes}

* Correzioni dei problemi di elaborazione delle risorse.
* Correzioni nella [!DNL Dynamic Media] configurazione e nella pubblicazione delle risorse sul servizio di [!DNL Dynamic Media] distribuzione.

>[!MORELIKETHIS]
>
>* [Informazioni su Adobe Asset Link](https://www.adobe.com/creativecloud/business/enterprise/adobe-asset-link.html)
>* [Configura Portale marchio](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html)
>* [Configurare Experience Manager per l’utilizzo del collegamento delle risorse](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html)
>* [Creare un flusso di lavoro in Experience Manager utilizzando i microservizi delle risorse](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html#post-processing-workflows)


## Novità in Cloud Manager {#whats-new-cloud-manager}

* Gli URL dell&#39;editore sono ora disponibili nella pagina Ambiente dell&#39;interfaccia utente di Cloud Manager.
* Modifiche alla navigazione per consentire agli utenti di modificare, cambiare o aggiungere un programma dalla pagina di panoramica di Cloud Manager.
* Modifiche per consentire all&#39;utente di modificare il programma dalla scheda del programma sulla pagina di destinazione di Cloud Manager.
* Nuovo stato **pipeline In esecuzione** visualizzata rispetto all&#39;ambiente a cui è associata.
* Miglioramenti alla comprensibilità della pagina di esecuzione della pipeline. Questo include la visualizzazione del nome della pipeline (solo non di produzione) e del tipo e un contrassegno per indicare se lo stato della pipeline è In corso/Annullato/Non riuscito.
* Descrizioni comandi per migliorare l’esperienza e la comprensibilità degli utenti in merito al motivo per cui il pulsante Aggiungi programma/ambiente è disattivato.
* Gli ambienti con errore possono ora essere eliminati tramite l&#39;interfaccia utente e l&#39;API.
* Il processo utilizzato per generare password git è stato reso più flessibile ai problemi nel livello di servizio sottostante.

### Correzioni di bug {#bug-fixes-cloud-manager}

* I collegamenti all&#39;ambiente di passaggio nella pagina dei dettagli di esecuzione della pipeline non si spostavano in modo coerente nella posizione corretta.
* I singoli passaggi all&#39;interno del processo di creazione dell&#39;ambiente potrebbero essere timeout prima del necessario, causando il fallimento del processo.
* La configurazione Maven utilizzata nel contenitore di build è stata aggiornata per evitare il blocco critico durante il download dei metadati dell&#39;artifact.
* In alcuni casi, il passaggio Genera immagine non può scaricare correttamente i pacchetti dei clienti.
* Alcune condizioni che si verificano raramente impedirebbero l&#39;eliminazione degli ambienti.
* Notifiche Experience Cloud non ricevute in modo coerente.
