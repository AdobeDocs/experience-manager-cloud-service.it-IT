---
title: Note sulla versione 2020.4.0
description: Note sulla versione 2020.4.0
translation-type: tm+mt
source-git-commit: c6c0e93d881762a2b501abb3d8c8356046a5f082

---


# Note sulla versione di AEM as a Cloud Service 2020.4.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di Experience Manager as a Cloud Service 2020.4.0.

## Release Date {#release-date}

La data di rilascio per Experience Manager come servizio cloud 2020.4.0 è il 9 aprile 2020.

## Assets {#assets}

Segui questa sezione per scoprire le novità e gli aggiornamenti per Experience Manager Assets e Dynamic Media in AEM come servizio cloud versione 2020.4.0.

### Novità {#assets-what-is-new}

* [Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) è disponibile per AEM come risorse di servizio cloud, che supporta i casi di utilizzo della distribuzione delle risorse. Con Brand Portal le organizzazioni possono soddisfare le loro esigenze di marketing e distribuire in sicurezza le risorse approvate relative a prodotti e marchi, che potranno essere scaricate da agenzie esterne, partner, team interni e rivenditori.
   * La configurazione del Brand Portal viene eseguita tramite la console Adobe I/O
   * L&#39;origine delle risorse in Brand Portal non è ancora supportata con AEM come servizio cloud
* La nuova versione di [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html) 2.0 è supportata con AEM come servizio cloud. Adobe Asset Link semplifica la collaborazione tra creativi e professionisti del marketing nel processo di creazione dei contenuti collegando AEM Assets alle app desktop Creative Cloud Photoshop, Illustrator e InDesign tramite il pannello Collegamento risorse in-app.
   * AEM come servizio cloud è preconfigurato per Adobe Asset Link, con conseguente configurazione [](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html)semplificata.
   * Asset Link ora supporta uno switcher [di ambiente](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink)AEM, che consente agli utenti creativi di connettersi più facilmente a diversi ambienti AEM (ad esempio, nel caso di designer di agenzie che lavorano con più client con AEM Assets)
* L’avvio automatico per i flussi di lavoro [post-elaborazione](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) può essere configurato nell’interfaccia utente Proprietà cartella per gerarchie di cartelle specifiche.
   * L’interfaccia utente Proprietà cartella è stata semplificata: la nuova scheda Elaborazione risorse contiene il profilo metadati, il profilo di elaborazione e la nuova configurazione del flusso di lavoro di avvio automatico
* La finestra di dialogo di rielaborazione delle risorse consente di selezionare un profilo di elaborazione specifico e decidere di rielaborarlo nelle sottocartelle
* Elemento multimediale dinamico: È stata aggiunta la configurazione Pubblicazione selettiva, che significa che le risorse vengono pubblicate automaticamente solo per la visualizzazione in anteprima protetta e possono essere esplicitamente pubblicate in AEM senza la pubblicazione in DMS7 per la distribuzione nel dominio pubblico.

### Correzioni di bug {#assets-bug-fixes}

* Problemi risolti nell’elaborazione delle risorse
* Problemi risolti nella configurazione e pubblicazione di risorse per contenuti multimediali dinamici e servizi di distribuzione
