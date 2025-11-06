---
title: Collegare AEM Forms a Adobe Experience Platform (AEP) | Guida all’integrazione dei dati
description: Scopri come integrare AEM Forms con Adobe Experience Platform per sfruttare i profili dei clienti, inviare dati dai moduli e creare esperienze personalizzate. Guida dettagliata.
contentOwner: Khushwant Singh
docset: CloudService
role: Admin, Developer, User
feature: Adaptive Forms, Core Components
exl-id: b0eb19d3-0297-4583-8471-edbb7257ded4
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2047'
ht-degree: 5%

---

# Integrazione di AEM Forms con Adobe Experience Platform (AEP) {#aem-forms-aep-integration}

<span class="preview"> La funzionalità di connessione di Adaptive Forms (AEM Forms) con Adobe Experience Platform (AEP) è inclusa nel programma di accesso anticipato. Per richiedere l&#39;accesso alla funzionalità, è sufficiente inviare un&#39;e-mail dal tuo indirizzo ufficiale a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com?subject=Request%20for%20Early%20Access%20to%20AEP%20Connector%20\(AEM%20Forms%20Integration%20with%20Adobe%20Experience%20Platform\)&body=Dear%20AEM%20Forms%20Team%2C%0D%0A%0D%0AI%20hope%20this%20message%20finds%20you%20well.%0D%0A%0D%0AI%20am%20writing%20to%20request%20access%20to%20the%20Early%20Access%20Program%20for%20the%20AEP%20Connector%2C%20which%20enables%20integration%20between%20AEM%20Forms%20and%20Adobe%20Experience%20Platform.%0D%0A%0D%0AOrganization%20Name%3A%20%5BYour%20organization%20name%5D%0D%0AOrganization%20ID%3A%20%5BYour%20organization%20ID%2C%20if%20available%5D%0D%0AUse%20Case%3A%20%5BBriefly%20describe%20your%20intended%20use%20case%2C%20including%20goals%20or%20benefits%20you%20aim%20to%20achieve%20with%20the%20integration%5D%0D%0A%0D%0AThank%20you%20for%20your%20time%20and%20consideration.%0D%0A%0D%0ABest%20regards%2C%0D%0A%5BYour%20Full%20Name%5D%0D%0A%5BYour%20Job%20Title%2C%20if%20applicable%5D%0D%0A%5BYour%20Contact%20Information%2C%20if%20appropriate%5D). Puoi anche visitare la pagina <a href="/help/forms/early-access-ea-features.md">Programma di accesso anticipato </a> per scoprire tutte le innovazioni e le funzionalità disponibili. . </span>

## Panoramica {#overview}

Puoi connettere AEM Forms a Adobe Experience Platform per trasformare le esperienze dei moduli. Questa potente integrazione consente alle organizzazioni di sfruttare i profili cliente in tempo reale per esperienze di moduli personalizzati, semplificare l&#39;invio di dati di **AEM Forms ad Experience Platform** e creare record cliente unificati nell&#39;ecosistema Adobe. Collegando i moduli adattivi con le solide funzionalità di gestione dei dati di Experience Platform, puoi creare esperienze più rilevanti e migliorare i tassi di conversione, mantenendo al contempo un’unica fonte di verità per i dati dei clienti.

### Cos’è il connettore AEM Forms per Adobe Experience Platform (AEP)? {#what-is-connector}

Il connettore AEM Forms per Adobe Experience Platform (AEP) è un connettore fornito da AEM Forms che consente l’integrazione diretta tra AEM Forms e Adobe Experience Platform (AEP). Questa integrazione ti consente di creare moduli utilizzando gli schemi XDM disponibili in AEP e di inviare nuovamente i dati ad AEP a scopo di personalizzazione e idratazione dei profili.

## Perché collegare AEM Forms a Adobe Experience Platform (AEP)? {#benefits}

La connessione del Forms adattivo con Adobe Experience Platform offre vantaggi significativi sia per la tua organizzazione che per i tuoi clienti:

* **Profili cliente unificati** - Arricchisci i profili dei clienti con i dati di invio dei moduli, creando una visualizzazione completa delle interazioni e delle preferenze dei clienti
* **Esperienze modulo personalizzate** - Sfrutta i dati del profilo esistenti per precompilare i campi e personalizzare i moduli in base alle informazioni note del cliente
* **Raccolta dati semplificata** - Acquisisci i dati del modulo direttamente nei set di dati di AEP senza creare connettori personalizzati o codice di integrazione
* **Attivazione dati in tempo reale** - Invia dati di invio modulo ad altre applicazioni Adobe tramite Real-Time CDP per l&#39;attivazione immediata
* **Gestione semplificata della conformità** - Gestione centralizzata del consenso e delle policy di governance dei dati tramite AEP
* **Tempi di sviluppo ridotti** - Elimina il lavoro di integrazione personalizzata con un connettore predefinito che segue le best practice
* **Arricchimento del profilo cliente con i dati del modulo**: aggiorna e migliora automaticamente i profili cliente con ogni invio del modulo, creando informazioni più approfondite sul cliente

## Funzioni principali {#key-features}

* Creare moduli utilizzando schemi XDM di AEP
* Inviare i dati del modulo ad AEP per la personalizzazione
* Supporto per l’acquisizione di dati in streaming
* Abilitare l’idratazione del profilo per esperienze utente avanzate
* Integrazione con il sistema di profili di AEP
* Integrazione dello schema XDM con moduli adattivi per la raccolta dati standardizzata
* Connessione streaming di AEP per moduli che consente l’elaborazione di dati in tempo reale

Il video seguente offre una guida dettagliata sui prerequisiti (come creazione di uno schema, configurazione dei dati e autenticazione) e mostra come creare e collegare Forms adattivo a Adobe Experience Platform (AEP)

>[!VIDEO](https://video.tv.adobe.com/v/3457850/)

<span> Questo video è applicabile solo ai Componenti core. Per i componenti UE/Foundation, fare riferimento all&#39;articolo.</span>

## Prerequisiti {#prerequisites}

Prima di configurare il connettore AEP in AEM Forms, assicurati di aver completato quanto segue in Adobe Experience Platform:

1. Configurazione schema
   * [Creare uno schema XDM](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/tutorials/create-schema-ui)
   * [Abilita schema per la profilatura](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/tutorials/create-schema-ui#profile)
   * [Definisci campo identità](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/tutorials/create-schema-ui#profile)

2. Configurazione dati
   * [Crea un set di dati](https://experienceleague.adobe.com/it/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/create-datasets)
   * [Configura la connessione in streaming](https://experienceleague.adobe.com/it/docs/experience-platform/ingestion/tutorials/create-streaming-connection) (è necessario l&#39;URL dell&#39;endpoint in streaming in un secondo momento, quindi prendi nota adesso.)

3. Autenticazione
   * [Genera credenziali API](https://experienceleague.adobe.com/it/docs/experience-platform/landing/platform-apis/api-authentication#generate-credentials) (ID client e Segreto client) da Adobe Developer Console


## Passaggi di implementazione

### &#x200B;1. Creare una configurazione cloud di AEP

1. Passa alla **istanza Adobe Experience Manager** > **Strumenti** > **Servizi cloud** > **Adobe Experience Platform**.
1. Selezionare un **Contenitore configurazione** per archiviare la configurazione.
1. Fai clic su **Crea** per aprire la configurazione guidata di AEP
1. Immetti i seguenti dettagli:
   * Titolo
   * ID client (ottenuto dalla console per sviluppatori)
   * Segreto client (ottenuto dalla console per sviluppatori)
   * URL OAuth (esiste un URL predefinito, ma può essere ottenuto anche dalla console per sviluppatori)

   ![Configurazione cloud AEP](/help/forms/assets/aep-cloud-configuration.png)

1. Fai clic su **Connetti** per stabilire la connessione. Dopo aver stabilito la connessione, configura le seguenti impostazioni aggiuntive:
   * URL di base: platform.adobe.io (questo è un URL predefinito che può essere ottenuto anche dalla console per sviluppatori; per impostazione predefinita, gli URL di oauth e della piattaforma vengono impostati su URL di produzione. In questo caso, è necessario connettersi all&#39;area di visualizzazione - utilizzare gli URL dell&#39;area di visualizzazione.)
   * ID organizzazione (ottenuto dalla console per sviluppatori insieme all’ID/segreto client)
   * Nome sandbox (richiesto per gli ambienti di sviluppo e produzione)

### &#x200B;2. Creazione di moduli con integrazione di schema XDM {#form-creation}

>[!BEGINTABS]

>[!TAB Componente di base]

Per creare un modulo adattivo basato su componenti di base con integrazione dello schema, effettua le seguenti operazioni:

1. Accedi alla procedura guidata di creazione del modulo:
   * Passa alla **istanza Adobe Experience Manager** > **Forms** > **Forms e documenti**.
   * Fai clic su **Crea** > **Modulo adattivo**.
1. Nella scheda **source**, seleziona un modello di base.
1. Nella scheda **Dati**, seleziona l&#39;opzione **Adobe Experience Platform**.
1. Nel riquadro delle proprietà, seleziona la configurazione cloud.

   ![](/help/forms/assets/xdm-schema-integration.png)

   Il sistema carica tutti gli schemi disponibili da Adobe Experience Platform

   >[!NOTE]
   >
   >
   > * Vengono recuperati solo gli schemi abilitati per il profilo e non generati dal sistema.
   > * Il caricamento iniziale dello schema potrebbe richiedere del tempo durante la prima configurazione.

1. Seleziona i campi appropriati/obbligatori dello schema. (Guarda il video per i passaggi dettagliati)
1. Nella scheda invio:
   * Seleziona l&#39;azione di invio **Invia a Adobe Experience Platform**
   * Configura le impostazioni di invio del modulo per l&#39;invio dei dati di **AEM Forms ad Experience Platform**
1. Nel riquadro delle proprietà:
   * Aggiungi l’URL di streaming (ottenuto da AEP Sources > Streaming Connection)
   * Aggiungi l’ID del flusso di dati (disponibile in AEP Sources > Flow > API Usage Information)
1. Fai clic su **Salva**. Fornisci i dettagli del modulo:
   * Titolo
   * Nome
   * Percorso di archiviazione
1. Aggiungi il pulsante Invia al modulo. Il modulo è pronto per inviare dati ad AEP.

>[!TAB Componente core]

Per creare un modulo adattivo basato su componenti core con integrazione dello schema, effettua le seguenti operazioni:

1. Accedi alla procedura guidata di creazione del modulo:
   * Passa alla **istanza Adobe Experience Manager** > **Forms** > **Forms e documenti**.
   * Fai clic su **Crea** > **Modulo adattivo**.
1. Nella scheda **source**, seleziona un modello basato su Componente core.
1. Nella scheda **Dati**, seleziona l&#39;opzione **Adobe Experience Platform**.
1. Nel riquadro delle proprietà, seleziona la configurazione cloud.

   ![](/help/forms/assets/xdm-schema-integration.png)

   Il sistema carica tutti gli schemi disponibili da Adobe Experience Platform

   >[!NOTE]
   >
   >
   > * Vengono recuperati solo gli schemi abilitati per il profilo e non generati dal sistema.
   > * Il caricamento iniziale dello schema potrebbe richiedere del tempo durante la prima configurazione.

1. Seleziona i campi appropriati/obbligatori dello schema. (Guarda il video per i passaggi dettagliati)
1. Nella scheda invio:
   * Seleziona l&#39;azione di invio **Invia a Adobe Experience Platform**
   * Configura le impostazioni di invio del modulo per l&#39;invio dei dati di **AEM Forms ad Experience Platform**
1. Nel riquadro delle proprietà:
   * Aggiungi l’URL di streaming (ottenuto da AEP Sources > Streaming Connection)
   * Aggiungi l’ID del flusso di dati (disponibile in AEP Sources > Flow > API Usage Information)
1. Fai clic su **Salva**. Fornisci i dettagli del modulo:
   * Titolo
   * Nome
   * Percorso di archiviazione
1. Aggiungi il pulsante Invia al modulo. Il modulo è pronto per inviare dati ad AEP.

>[!TAB Editor universale]

Per creare un modulo adattivo creato utilizzando l’editor universale con integrazione di schema, effettua le seguenti operazioni:

1. Accedi alla procedura guidata di creazione del modulo:
   * Passa alla **istanza Adobe Experience Manager** > **Forms** > **Forms e documenti**.
   * Fai clic su **Crea** > **Modulo adattivo**.
1. Nella scheda **source**, seleziona un modello basato su Edge Delivery.
1. Nella scheda **Dati**, seleziona l&#39;opzione **Adobe Experience Platform**.
1. Nel riquadro delle proprietà, seleziona la configurazione cloud.

   ![integrazione schema](/help/forms/assets/xdm-schema-integration.png)

   Il sistema carica tutti gli schemi disponibili da Adobe Experience Platform

   >[!NOTE]
   >
   >
   > * Vengono recuperati solo gli schemi abilitati per il profilo e non generati dal sistema.
   > * Il caricamento iniziale dello schema potrebbe richiedere del tempo durante la prima configurazione.

1. Seleziona i campi appropriati/obbligatori dello schema. (Guarda il video per i passaggi dettagliati)
1. Nella scheda invio:
   * Seleziona l&#39;azione di invio **Invia a Adobe Experience Platform**
   * Configura le impostazioni di invio del modulo per l&#39;invio dei dati di **AEM Forms ad Experience Platform**

     >[!NOTE]
     >
     >* Se l&#39;icona Origini dati non è visibile nell&#39;interfaccia di Universal Editor o nella proprietà Associa riferimento nel pannello delle proprietà appropriato, abilitare l&#39;estensione **Origine dati** in Extension Manager.
     >* Se non visualizzi l’icona **Modifica le proprietà del modulo** nell’interfaccia dell’editor universale, abilita l’estensione **Modifica le proprietà del modulo** in Extension Manager.
     > 
     >* Per scoprire come abilitare e disabilitare le estensioni nell’editor universale, fai riferimento all’articolo [Caratteristiche principali delle funzioni di Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions).

   Il servizio di precompilazione dei moduli nell’editor universale non è attualmente supportato.

1. Nel riquadro delle proprietà:
   * Aggiungi l’URL di streaming (ottenuto da AEP Sources > Streaming Connection)
   * Aggiungi l’ID del flusso di dati (disponibile in AEP Sources > Flow > API Usage Information)
1. Fai clic su **Salva**. Fornisci i dettagli del modulo:
   * Titolo
   * Nome
   * Percorso di archiviazione
1. Aggiungi il pulsante Invia al modulo. Il modulo è pronto per inviare dati ad AEP.

>[!ENDTABS]

## Note importanti {#important-notes}

* I dati inviati tramite i moduli diventano visibili in AEP dopo circa 10-15 minuti
* Per impostazione predefinita, sono elencati solo gli schemi abilitati per il profilo
* Mentre l’invio dei dati funziona per tutti gli schemi, la funzionalità di precompilazione è limitata agli schemi abilitati per il profilo
* I dati negli schemi non abilitati per il profilo non verranno utilizzati per la creazione del profilo, anche se lo schema viene successivamente abilitato per la profilatura
* **L&#39;arricchimento del profilo cliente con i dati del modulo** richiede la corretta configurazione del campo di identità nello schema XDM
* **L&#39;invio di dati AEM Forms ad Experience Platform** utilizza **la connessione streaming AEP per i moduli** per garantire il flusso di dati in tempo reale

## Best practice {#best-practices}

1. Pianifica attentamente la struttura dello schema prima di abilitare la profilatura
1. Prendere in considerazione i requisiti relativi al volume dei dati e alla scalabilità del sistema durante la configurazione di **connessione streaming AEP per i moduli**
1. Test approfondito dell’integrazione prima dell’implementazione di produzione
1. Monitorare i processi di acquisizione dei dati e creazione dei profili
1. Progetta l&#39;integrazione dello schema **XDM con moduli adattivi** per raccogliere solo i dati necessari
1. Utilizza **l&#39;arricchimento del profilo cliente con i dati del modulo** in modo strategico per migliorare la personalizzazione

## Considerazioni tecniche {#technical-considerations}

* Il connettore utilizza API di streaming pubbliche per l’invio dei dati
* La creazione del profilo si basa sul campo identità
* L’unificazione dei dati si verifica automaticamente in AEP
* L’integrazione supporta sia la creazione di nuovi moduli che la modifica di moduli esistenti
* L’integrazione dello schema XDM con i moduli adattivi standardizza la struttura dei dati tra diversi punti di contatto
* La connessione streaming di AEP per Forms fornisce funzionalità di acquisizione dati in tempo reale

## Domande frequenti (FAQ) {#faq}

### Domande generali {#general-questions}

**D: &quot;Questo connettore è disponibile con più offerte di AEM Forms?**
R: No, questa integrazione è disponibile solo per AEM Forms as a Cloud Service e si trova nel programma di accesso anticipato.

**D: questo connettore funziona sia con i componenti core Adaptive Forms che con i componenti di base?**
R: questo connettore funziona sia con i componenti core Adaptive Forms che con i componenti Forms Foundation adattivi.

**D: posso inviare dati a più set di dati AEP da un singolo modulo?**
R: Attualmente, ogni modulo può inviare solo un set di dati.

**D: esiste un limite al numero di invii di moduli che è possibile elaborare?**
R: L’invio di moduli è soggetto alle [quote e ai limiti di tariffa](https://experienceleague.adobe.com/it/docs/experience-platform/data-lifecycle/api/quota) per l’acquisizione in streaming da parte di AEP.

<!-- 
>
**Q: Can form attachments be sent to AEP?**
A: No, form attachments cannot be directly sent to AEP. You would need to store attachments separately and only send metadata to AEP. -->

### Domande sull’implementazione {#implementation-questions}

**D: come posso risolvere i problemi di connessione tra AEM Forms e AEP?**
R: Verifica le impostazioni di configurazione cloud, verifica che le credenziali API siano corrette e controlla che l’URL dell’endpoint di streaming sia configurato correttamente.

**D: posso utilizzare schemi XDM personalizzati con questa integrazione?**
R: Sì, puoi utilizzare qualsiasi schema XDM personalizzato purché sia configurato correttamente in AEP e, per la funzionalità di precompilazione, abilitato per i profili.

**D: come si abilita la precompilazione dei moduli con i dati del profilo di AEP?**
R: Assicurati che lo schema sia abilitato per il profilo e che il modulo sia configurato per utilizzare lo stesso campo di identità definito nello schema.

**D: cosa succede se devo trasformare i dati prima di inviarli ad AEP?**
R: È possibile utilizzare regole modulo o funzioni personalizzate per trasformare i dati prima dell’invio. Per trasformazioni complesse, puoi utilizzare un’azione di invio personalizzata.

**D: posso utilizzare questa integrazione in un modello di distribuzione ibrida?**
R: No, questa integrazione è specifica di AEM Forms as a Cloud Service.

## Riepilogo e passaggi successivi {#summary-next-steps}

L’integrazione di AEM Forms con Adobe Experience Platform consente alle organizzazioni di creare un flusso di dati senza soluzione di continuità tra i moduli e l’ecosistema più ampio di Experience Platform. Questa integrazione ti consente di creare esperienze di moduli più personalizzate, semplificare la raccolta dei dati e migliorare i profili dei clienti con dati importanti per l’invio dei moduli.

Per iniziare a utilizzare questa integrazione:

1. **Richiedi accesso** - Se non lo hai già fatto, partecipa al programma di Accesso anticipato contattando [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com?subject=Request%20for%20Early%20Access%20to%20AEP%20Connector%20\(AEM%20Forms%20Integration%20with%20Adobe%20Experience%20Platform\)&body=Dear%20AEM%20Forms%20Team%2C%0D%0A%0D%0AI%20hope%20this%20message%20finds%20you%20well.%0D%0A%0D%0AI%20am%20writing%20to%20request%20access%20to%20the%20Early%20Access%20Program%20for%20the%20AEP%20Connector%2C%20which%20enables%20integration%20between%20AEM%20Forms%20and%20Adobe%20Experience%20Platform.%0D%0A%0D%0AOrganization%20Name%3A%20%5BYour%20organization%20name%5D%0D%0AOrganization%20ID%3A%20%5BYour%20organization%20ID%2C%20if%20available%5D%0D%0AUse%20Case%3A%20%5BBriefly%20describe%20your%20intended%20use%20case%2C%20including%20goals%20or%20benefits%20you%20aim%20to%20achieve%20with%20the%20integration%5D%0D%0A%0D%0AThank%20you%20for%20your%20time%20and%20consideration.%0D%0A%0D%0ABest%20regards%2C%0D%0A%5BYour%20Full%20Name%5D%0D%0A%5BYour%20Job%20Title%2C%20if%20applicable%5D%0D%0A%5BYour%20Contact%20Information%2C%20if%20appropriate%5D)
2. **Prepara l&#39;ambiente** - Assicurati di disporre delle autorizzazioni e delle configurazioni necessarie sia in AEM Forms che in Adobe Experience Platform
3. **Segui i passaggi per l&#39;implementazione**. Utilizza la guida precedente per configurare la configurazione cloud e creare il tuo primo modulo connesso ad AEP con l&#39;integrazione dello schema XDM.
4. **Verifica approfondita** - Convalida le funzionalità di invio e precompilazione dei dati in un ambiente di sviluppo
5. **Piano per la produzione** - Collabora con il team di implementazione per pianificare la distribuzione dell&#39;invio di dati AEM Forms ad Experience Platform in produzione

## Risorse correlate {#related-resources}

* [Documentazione di AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=it)
* [Documentazione di Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/home.html?lang=it)
* [Panoramica del sistema XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=it)
* [Acquisizione in streaming in Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=it)
* [Panoramica del profilo cliente in tempo reale](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=it)
* [Funzioni di accesso anticipato di AEM Forms](/help/forms/early-access-ea-features.md)
* [Creazione di Forms adattivo con i componenti core](/help/forms/creating-adaptive-form-core-components.md)
* [Utilizzo dei modelli di dati dei moduli in AEM Forms](/help/forms/using-form-data-model.md)

<!--
Schema markup for technical documentation
{
  "@context": "https://schema.org",
  "@type": "TechArticle",
  "headline": "Connect AEM Forms with Adobe Experience Platform (AEP) | Data Integration Guide",
  "description": "Learn how to integrate AEM Forms with Adobe Experience Platform to leverage customer profiles, submit form data, and create personalized experiences.",
  "datePublished": "2025-05-28",
  "author": {
    "@type": "Corporation",
    "name": "Adobe"
  },
  "publisher": {
    "@type": "Organization",
    "name": "Adobe Experience League",
    "logo": {
      "@type": "ImageObject",
      "url": "https://experienceleague.adobe.com/assets/img/favicons/apple-touch-icon.png"
    }
  },
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/aem-forms-aep-connector.html"
  },
  "articleSection": "AEM Forms",
  "keywords": "AEM Forms, Adobe Experience Platform, XDM schema, data integration, form submission, customer profiles, personalization"
}
-->
