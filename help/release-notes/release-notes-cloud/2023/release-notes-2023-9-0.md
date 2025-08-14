---
title: Note sulla versione 2023.9.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2023.9.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: d747f58b-8d6c-418d-9d2b-ec3ae4b6dc03
feature: Release Information
role: Admin
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 81%

---


# Note sulla versione 2023.9.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione funzionale 2023.9.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2021 o 2022.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio della versione corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2023.9.0) è il venerdì 28 settembre 2023. La prossima versione funzionale (2023.10.0) è pianificata per il venerdì 26 ottobre 2023.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica della versione di settembre 2023 per un riepilogo delle funzioni aggiunte alla versione 2023.9.0:

>[!VIDEO](https://video.tv.adobe.com/v/3424826/?quality=12)

## AEM Edge Delivery Services {#edge-delivery}

Edge Delivery è una nuova serie di servizi componibili incentrati sulla massimizzazione dell’impatto dei contenuti per promuovere risultati aziendali misurabili al momento dell’interazione con il cliente.

Ulteriori informazioni su Edge Delivery Services sono disponibili nell&#39;articolo [qui](/help/edge/overview.md).

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni nella Vista risorse {#assets-view-features}

**Assegnare un modulo di metadati a una cartella**

Ora puoi assegnare il modulo metadati a una cartella specifica all’interno della distribuzione. Per tutte le risorse nella cartella, comprese le risorse nelle sottocartelle, vengono quindi visualizzate le proprietà definite nel modulo di metadati assegnato.

![assegnare un modulo di metadati a una cartella](/help/release-notes/assets/assign-to-folder.png)

### Nuove funzioni nella vista Amministratore {#admin-view-features}

* **Integrare AEM Assets as a Cloud Service con l&#39;authoring basato su documenti per Edge Delivery Services**: integrare AEM Assets con l&#39;authoring basato su documenti per Edge Delivery Services per consentire agli autori di siti Web di [utilizzare le immagini disponibili negli archivi AEM Assets durante l&#39;authoring di documenti in Microsoft Word o Google Docs](/help/edge/overview.md).

* **Estrai archivi ZIP**: possibilità di selezionare archivi ZIP gestiti in Experience Manager e [di estrarre i file direttamente in Experience Manager](/help/assets/manage-digital-assets.md#extract-zip-archives) senza scaricarli.

  ![Fissa elementi per gruppi](/help/release-notes/assets/extract-archive.png)

### Funzioni pre-release disponibili in [!DNL Experience Manager Assets] {#prerelease-features-assets}

* **Dynamic Media**: [supporto di tracce con più didascalie e multi-audio per video in Dynamic Media](/help/assets/dynamic-media/video.md#about-msma): è ora possibile aggiungere facilmente più didascalie e tracce audio a un video principale. Grazie a questa funzionalità, i video sono accessibili a un pubblico globale. È possibile personalizzare un singolo video principale pubblicato per un pubblico globale in più lingue e rispettare le linee guida sull’accessibilità per diverse aree geografiche. Gli autori possono gestire anche le didascalie e le tracce audio da una singola scheda nell’interfaccia utente.

  ![Scheda Didascalie e Tracce audio nella pagina Proprietà di una risorsa video selezionata.](/help/release-notes/assets/msma-aem-cs.png)*Scheda Didascalie e Tracce audio nella pagina delle Proprietà di una risorsa video selezionata.*

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni in [!DNL Experience Manager Forms] {#forms-features}

* [**Supporto reCAPTCHA di Google Enterprise**](/help/forms/captcha-adaptive-forms-core-components.md): utilizza Google reCAPTCHA Enterprise in un modulo adattivo per fornire una protezione avanzata contro le attività fraudolente e lo spam, fornendo un’esperienza utente più sicura. Grazie all’analisi avanzata dei rischi e all’integrazione diretta, gli utenti autentici possono inviare facilmente i moduli mentre i bot vengono bloccati in modo efficace.

* [**Adobe Analytics con Configurazione dell’automazione di Experience Cloud per Forms**](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md): ora è possibile abilitare Adobe Analytics con la configurazione dell’automazione di Experience grazie a un paio di pulsanti. Consente di collegare AEM Forms as a Cloud Service con i tag Experience Platform e Adobe Analytics per acquisire e tenere traccia delle metriche di prestazione per i moduli pubblicati.

  >[!VIDEO](https://video.tv.adobe.com/v/3424577/enable-adobe-analytics/?quality=12&learn=on)

* [**Modello di rapporto di Adobe Analytics per moduli adattivi**](/help/forms/view-understand-aem-forms-analytics-reports.md): Forms as a Cloud Service ora fornisce un rapporto OOTB di Adobe Analytics. Consente di comprendere facilmente le prestazioni dei moduli. Le metriche a livello di modulo forniscono informazioni approfondite sulle prestazioni del modulo per più indicatori di prestazioni chiave (KPI, Key Performance Indicator), come rappresentazioni, visitatori, invii e tempo medio di riempimento. Monitorando il comportamento degli utenti e i feedback ricevuti, è possibile identificare le aree del modulo che creano confusione e promuovere i miglioramenti alla progettazione e alle funzionalità del modulo.

  ![Rapporti di Adobe Analytics sul coinvolgimento dell’utente nei moduli adattivi](/help/forms/assets/forms-analytics-report.png)

* **[Frammento di modulo in moduli adattivi basati su componenti core](/help/forms/adaptive-form-fragments-core-components.md)**: elimina la duplicazione, ottimizza l’inventario digitale e migliora la collaborazione migliorando l’esperienza di creazione dei moduli con i Frammenti di modulo. Questi componenti riutilizzabili si integrano perfettamente in più moduli, semplificando la creazione di moduli coerenti e dall’aspetto professionale. I Frammenti di modulo garantiscono riutilizzabilità, standardizzazione e coerenza del brand attraverso la funzionalità “cambia una volta e rifletti ovunque”. Migliora la manutenzione e l’efficienza, poiché gli aggiornamenti apportati in un’unica posizione vengono propagati automaticamente in tutti i moduli che utilizzano questi frammenti.

* **[Passaggio del flusso di lavoro Adobe Sign migliorato](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)**: il passaggio del flusso di lavoro di Adobe Sign è stato migliorato per includere quanto segue:
   * **Autenticazione basata su ID della Pubblica amministrazione per Adobe Sign**: l’autenticazione basata su ID della Pubblica amministrazione di Adobe Acrobat Sign offre un ulteriore livello di verifica, consentendo agli utenti di autenticare la propria identità utilizzando gli ID della pubblica amministrazione (patente di guida, carta d’identità, passaporto). Utilizzando documenti di identificazione attendibili, questo miglioramento aggiunge un ulteriore livello di affidabilità al processo di firma, rendendolo ideale per scenari che richiedono maggiore sicurezza, conformità e convalida degli utenti.

   * **Audit Trail per documenti di Adobe Sign**: utilizzo della funzione Audit Trail per ottenere informazioni dettagliate sul ciclo di vita dei documenti di Adobe Sign. Con l’Audit Trail è ora possibile mantenere un record completo di tutte le azioni e interazioni relative ai documenti. Tali azioni e interazioni includono dettagli quali visualizzazioni, modifiche o firme del documento, nonché le marche temporali di ciascun evento. Questo miglioramento è fondamentale per mantenere la conformità, risolvere le controversie e garantire l’integrità degli accordi digitali.

   * **Nuovi ruoli per i destinatari dell’accordo oltre al solo firmatario**: al fine di soddisfare meglio i requisiti del flusso di lavoro, Adobe Acrobat Sign può espandere i ruoli dei destinatari dell’accordo oltre al solo firmatario. Quando questa opzione è abilitata, ogni destinatario di un accordo può configurare il proprio ruolo singolarmente, in cui il Firmatario è l’impostazione predefinita.

* **Supporto del conteggio delle pagine nelle API di comunicazione**: ora, oltre a recuperare il documento tramite le API di comunicazione, è possibile ricevere anche le preziose informazioni sul numero di pagine contenute all’interno del documento.

* **[Gestione degli errori con handler degli errori personalizzati nell’editor delle regole](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)**: ora è possibile richiamare una funzione personalizzata a fronte di un errore restituito da un servizio esterno e fornire una risposta personalizzata agli utenti finali. Ad esempio, puoi richiamare un flusso di lavoro personalizzato nel back-end per codici di errore specifici o informare il cliente che il servizio non è disponibile.

* **[Versione a 64 bit di AEM Forms Designer](/help/forms/installing-configuring-designer.md)**: la versione a 64 bit di AEM Forms Designer offre prestazioni, scalabilità e gestione della memoria migliorate per migliorare l&#39;esperienza di creazione dei moduli. Grazie all&#39;architettura a 64 bit, è possibile gestire con facilità progetti ancora più grandi e complessi, garantendo flussi di lavoro di progettazione ottimizzati ed efficienza. Migliora le funzionalità di progettazione dei moduli e abbraccia il futuro di AEM Forms Designer con questa versione all’avanguardia.

### Programma per i primi utilizzatori {#forms-early-adopter}

* **[Proteggere i documenti con le API DocAssurance (parte di API Communication)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: le API DocAssurance consentono di proteggere le informazioni riservate firmando e crittografando i documenti. Tramite crittografia, il contenuto di un documento viene trasformato in un formato illeggibile, in modo che solo gli utenti autorizzati possano accedervi. Questo strato di protezione fortificato non solo protegge i dati preziosi da persone non autorizzate, ma offre anche la massima tranquillità. Le API di firma consentono all’organizzazione di proteggere la sicurezza e la privacy dei documenti Adobe PDF che distribuisce e riceve. Questo servizio utilizza firme digitali e certificazione per garantire che solo i destinatari desiderati possano modificare i documenti.

  Per partecipare al programma per i primi utilizzatori e richiedere l’accesso alla funzionalità, è possibile inviare una e-mail all’indirizzo `aem-forms-ea@adobe.com` dal proprio ID e-mail ufficiale.

* **[Forms adattivo headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=it)**: utilizza Forms adattivo headless per consentire agli sviluppatori di creare, pubblicare e gestire moduli interattivi a cui è possibile accedere e interagire tramite API, anziché tramite un&#39;interfaccia utente grafica tradizionale. I moduli adattivi headless consentono di:

   * creare moduli multi-canale di alta qualità nel linguaggio di programmazione desiderato
   * integrare in modo nativo i moduli nelle app desktop e per dispositivi mobili, nei siti web e nelle applicazioni chat
   * riutilizzare i componenti proprietari dell’interfaccia utente con le applicazioni di Forms
   * sfruttare la potenza di Adobe Experience Manager Forms

  È possibile inviare un’e-mail a `aem-forms-headless@adobe.com` dal proprio ID e-mail ufficiale per aderire al programma per i primi utilizzatori.

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Nuovo comportamento di caching CDN per i parametri URL relativi alla campagna {#cache-url-params}

Per i nuovi ambienti, la rete CDN rimuoverà i parametri di query relativi al marketing per impostazione predefinita, al fine di aumentare le prestazioni della campagna di marketing e i rapporti di hit della cache. Gli ambienti esistenti non subiscono modifiche. [Ulteriori informazioni](/help/implementing/dispatcher/caching.md#marketing-parameters).

### Regole del filtro del traffico (incluse le regole di WAF) programma di adozione anticipata {#waf-early-adopter}

Filtra il traffico sulla rete CDN in base a:

* intestazioni e proprietà delle richieste (ad esempio, indirizzo IP)
* modelli di traffico noti associati a traffico dannoso

Ti interessa provare questa funzione e condividere con noi un tuo feedback? Invia un messaggio e-mail a **aemcs-waf-adopter@adobe.com** dal tuo ID e-mail ufficiale per ulteriori informazioni sul programma per i primi utilizzatori. Lo spazio è limitato.

Ulteriori informazioni sulla funzione nell’articolo sono disponibili [qui](/help/security/traffic-filter-rules-including-waf.md).

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
