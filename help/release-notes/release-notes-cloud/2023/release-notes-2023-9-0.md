---
title: Note sulla versione 2023.9.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione 2023.9.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: d747f58b-8d6c-418d-9d2b-ec3ae4b6dc03
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1441'
ht-degree: 18%

---

# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note specifiche sulla versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2021 o 2022.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] la versione corrente (2023.9.0) è il 28 settembre 2023. La prossima versione (2023.10.0) è prevista per il 26 ottobre 2023.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica sulla versione di settembre 2023 per un riepilogo delle funzioni aggiunte alla versione 2023.9.0:

>[!VIDEO](https://video.tv.adobe.com/v/3424826/?quality=12)

## Edge Delivery Services AEM {#edge-delivery}

Edge Delivery è una nuova serie di servizi componibili incentrati sulla massimizzazione dell’impatto dei contenuti per promuovere risultati aziendali misurabili al momento dell’interazione con il cliente.

Per ulteriori informazioni sui Edge Delivery Services, consulta l’articolo [qui](/help/edge/overview.md).

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni nella Vista risorse {#assets-view-features}

**Assegnare il modulo metadati a una cartella**

Ora puoi assegnare il modulo metadati a una cartella specifica all’interno della distribuzione. Tutte le risorse nella cartella, comprese le risorse nelle sottocartelle, quindi visualizzano le proprietà definite nel modulo metadati assegnato.

![assegnare il modulo metadati a una cartella](/help/release-notes/assets/assign-to-folder.png)

### Nuove funzioni nella visualizzazione Amministratore {#admin-view-features}

* **Integrare AEM Assets as a Cloud Service con l’authoring basato su documenti per i Edge Delivery Services**: integra AEM Assets con l’authoring basato su documenti per i Edge Delivery Services per consentire agli autori di siti web di [utilizzare le immagini disponibili negli archivi di AEM Assets durante la creazione di documenti nei documenti di Microsoft Word o Google](/help/edge/using.md#integrate-assets-edge).

* **Estrai archivi ZIP**: possibilità di selezionare archivi ZIP gestiti in Experience Manager e [estrazione diretta dei file in Experience Manager](/help/assets/manage-digital-assets.md#extract-zip-archives) senza scaricarli.

  ![Fissa elementi per gruppi](/help/release-notes/assets/extract-archive.png)

### Funzioni pre-release disponibili in [!DNL Experience Manager Assets] {#prerelease-features-assets}

* **Dynamic Medie**: [Supporto di tracce multi-sottotitolo e multi-audio per video in Dynamic Medie](/help/assets/dynamic-media/video.md#about-msma)- È ora possibile aggiungere facilmente più sottotitoli e tracce audio a un video principale. Grazie a questa funzionalità, i video sono accessibili a un pubblico globale. Puoi personalizzare un singolo video principale pubblicato per un pubblico globale in più lingue e rispettare le linee guida sull’accessibilità per diverse aree geografiche. Gli autori possono anche gestire i sottotitoli e le tracce audio da una singola scheda nell’interfaccia utente.

  ![Scheda Sottotitoli e tracce audio nella pagina Proprietà di una risorsa video selezionata.](/help/release-notes/assets/msma-aem-cs.png)*Scheda Sottotitoli e tracce audio nella pagina Proprietà di una risorsa video selezionata.*

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni in [!DNL Experience Manager Forms] {#forms-features}

* [**Supporto aziendale Google reCAPTCHA**](/help/forms/captcha-adaptive-forms-core-components.md): utilizza Google reCAPTCHA Enterprise in un modulo adattivo per fornire una protezione avanzata contro le attività fraudolente e lo spam, fornendo un’esperienza utente più sicura. Grazie all’analisi avanzata dei rischi e all’integrazione perfetta, gli utenti autentici possono inviare facilmente i moduli mentre i bot vengono bloccati in modo efficace.

* [**Adobe Analytics con Experience Cloud Setup Automation per Forms**](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md): ora puoi abilitare Adobe Analytics con Experience Cloud Setup Automation con un paio di pulsanti. Consente di collegare AEM Forms as a Cloud Service con i tag Experienci Platform e Adobe Analytics per acquisire e tenere traccia delle metriche delle prestazioni per i moduli pubblicati.

  >[!VIDEO](https://video.tv.adobe.com/v/3424577/enable-adobe-analytics/?quality=12&learn=on)

* [**Modello di rapporto Adobe Analytics per Adaptive Forms**](/help/forms/view-understand-aem-forms-analytics-reports.md): Forms as a Cloud Service ora fornisce un rapporto Adobe Analytics OOTB. Consente di comprendere facilmente le prestazioni dei moduli. Le metriche a livello di modulo forniscono informazioni approfondite sulle prestazioni del modulo per più indicatori di prestazioni chiave (KPI, Key Performance Indicator), come rappresentazioni, visitatori, invii e tempo medio di riempimento. Monitorando il comportamento degli utenti e i feedback ricevuti, è possibile identificare le aree del modulo che causano confusione e guidare i miglioramenti alla progettazione e alle funzionalità del modulo.

  ![Report Adobe Analytics sul coinvolgimento degli utenti dei moduli adattivi](/help/forms/assets/forms-analytics-report.png)

* **[Frammento di modulo in Forms adattivo basato su componenti core](/help/forms/adaptive-form-fragments-core-components.md)**: puoi dire addio alla duplicazione, ottimizzare l’inventario digitale e migliorare la collaborazione migliorando l’esperienza di creazione dei moduli con i frammenti di modulo. Questi componenti riutilizzabili si integrano perfettamente in più moduli, semplificando la creazione di moduli coerenti e dall’aspetto professionale. I frammenti di modulo garantiscono riutilizzabilità, standardizzazione e coerenza del brand attraverso la funzionalità &quot;cambia una volta e riflette ovunque&quot;. Aumenta la manutenibilità e l’efficienza, poiché gli aggiornamenti apportati in un’unica posizione vengono propagati automaticamente in tutti i moduli che utilizzano questi frammenti.

* **[Passaggio del flusso di lavoro Adobe Sign migliorato](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)**: il passaggio del flusso di lavoro di Adobe Sign è stato migliorato per includere quanto segue:
   * **Autenticazione basata su documento ufficiale per Adobe Sign**: l’autenticazione basata su documento ufficiale di Adobe Acrobat Sign offre un ulteriore livello di verifica, consentendo agli utenti di autenticare la propria identità utilizzando gli ID governativi (patente di guida, carta d’identità, passaporto). Utilizzando documenti di identificazione attendibili, questo miglioramento aggiunge un ulteriore livello di affidabilità al processo di firma, rendendolo ideale per scenari che richiedono maggiore sicurezza, conformità e convalida degli utenti.

   * **Audit Trail per documenti Adobe Sign**: utilizza la funzione Audit Trail per ottenere informazioni dettagliate sul ciclo di vita dei documenti Adobe Sign. Con Audit Trail è ora possibile mantenere un registro completo di tutte le azioni e interazioni relative ai documenti. Questo include dettagli quali chi ha visualizzato, modificato o firmato il documento, insieme ai timestamp di ogni evento. Questo miglioramento è fondamentale per mantenere la conformità, risolvere le controversie e garantire l’integrità degli accordi digitali.

   * **Nuovi ruoli per i destinatari del contratto oltre al solo firmatario**: Adobe Acrobat Sign può espandere i ruoli dei destinatari del contratto oltre al solo firmatario, per soddisfare meglio i requisiti del flusso di lavoro. Quando questa opzione è abilitata, ogni destinatario di un contratto ha il proprio ruolo configurabile singolarmente, con Firmatario come impostazione predefinita.

* **Supporto del conteggio delle pagine nelle API di comunicazione**: ora, oltre a recuperare il documento tramite le API di comunicazione, puoi ricevere anche le preziose informazioni sul numero di pagine contenute all’interno del documento.

* **[Gestione degli errori con gestori degli errori personalizzati nell’editor di regole](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)**: ora puoi richiamare una funzione personalizzata in risposta a un errore restituito da un servizio esterno e fornire una risposta personalizzata agli utenti finali. Ad esempio, puoi richiamare un flusso di lavoro personalizzato nel back-end per codici di errore specifici o informare il cliente che il servizio non è disponibile.

* **[Versione a 64 bit di AEM Forms Designer](/help/forms/installing-configuring-designer.md)**: la versione a 64 bit di AEM Forms Designer offre prestazioni, scalabilità e gestione della memoria migliorate per migliorare l’esperienza di creazione dei moduli. Grazie all&#39;architettura a 64 bit, è possibile gestire con facilità progetti ancora più grandi e complessi, garantendo flussi di lavoro di progettazione ottimizzati ed efficienza. Migliora le funzionalità di progettazione dei moduli e abbraccia il futuro di AEM Forms Designer con questa versione all’avanguardia.

### Programma di adozione anticipata {#forms-early-adopter}

* **[Protect i tuoi documenti con le API DocAssurance (parte delle API di comunicazione)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: le API DocAssurance ti consentono di proteggere le informazioni riservate firmando e crittografando i documenti. Tramite la crittografia, il contenuto di un documento viene trasformato in un formato illeggibile, in modo che solo gli utenti autorizzati possano accedervi. Questo strato di protezione fortificato non solo protegge i dati preziosi da occhi non autorizzati, ma offre anche la massima tranquillità. Le API di firma consentono all’organizzazione di proteggere la sicurezza e la privacy dei documenti Adobe PDF che distribuisce e riceve. Questo servizio utilizza firme digitali e certificazione per garantire che solo i destinatari desiderati possano modificare i documenti.

  Puoi scrivere a `aem-forms-early-adopter-program@adobe.com` dal tuo id e-mail ufficiale per partecipare al programma early adopter e richiedere l’accesso alla funzionalità.

* **[Forms adattivo headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=it)**: utilizza Forms adattivo headless per consentire agli sviluppatori di creare, pubblicare e gestire moduli interattivi a cui è possibile accedere e interagire tramite API, anziché tramite un’interfaccia utente grafica tradizionale. I moduli adattivi headless consentono di:

   * creare moduli multi-canale di alta qualità nel linguaggio di programmazione desiderato
   * integrare in modo nativo i moduli nelle app desktop e per dispositivi mobili, nei siti web e nelle applicazioni chat
   * riutilizzare i componenti proprietari dell’interfaccia utente con le applicazioni di Forms
   * sfruttare la potenza di Adobe Experience Manager Forms

  È possibile inviare un’e-mail a `aem-forms-headless@adobe.com` dal proprio ID e-mail ufficiale per aderire al programma per i primi utilizzatori.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Nuovo comportamento di caching CDN per i parametri URL relativi alla campagna {#cache-url-params}

Per i nuovi ambienti, la rete CDN rimuoverà i parametri di query relativi al marketing per impostazione predefinita, al fine di aumentare le prestazioni della campagna di marketing e i rapporti di hit della cache. Gli ambienti esistenti non subiscono modifiche. [Ulteriori informazioni.](/help/implementing/dispatcher/caching.md#marketing-parameters)

### Regole filtro traffico (incluse le regole WAF) programma per l’adozione anticipata {#waf-early-adopter}

Filtra il traffico sulla rete CDN in base a:
* intestazioni e proprietà della richiesta (ad esempio, indirizzo IP)
* modelli di traffico noti per essere associati a traffico dannoso

Ti interessa provare questa funzione e condividere feedback? Invia un messaggio e-mail a **aemcs-waf-adopter@adobe.com** dal tuo ID e-mail ufficiale per ulteriori informazioni sul programma early adopter. Lo spazio è limitato.

Ulteriori informazioni sulla funzione nell’articolo [qui](/help/security/traffic-filter-rules-including-waf.md).

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
