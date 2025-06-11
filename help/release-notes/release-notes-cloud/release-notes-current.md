---
title: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 628d254ee130d436f0ac1728ab464d24db583b81
workflow-type: tm+mt
source-wordcount: '2074'
ht-degree: 31%

---

# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note specifiche sulla versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2023 o 2024.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Per ricevere una notifica e-mail mensile sugli aggiornamenti delle note sulla versione di Experience Cloud, abbonati ad [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).

## Data di pubblicazione {#release-date}


La data di rilascio della versione funzionale corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2025.5.0) è il venerdì 5 giugno 2025. La prossima versione funzionale (2025.6.0) è pianificata per il venerdì 26 giugno 2025.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440928?quality=12&captions=ita)

-->

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Metadati generati da IA**

AEM Assets ora utilizza [AI per generare automaticamente i metadati, inclusi Titolo, Descrizione e Parole chiave](/help/assets/metadata-assets-view.md#ai-smart-tags). Questi campi generati dall’intelligenza artificiale migliorano la precisione dei metadati, rendendo le risorse più facili da cercare, classificare e consigliare. Questo approccio non solo migliora l’efficienza eliminando l’assegnazione tag manuale, ma garantisce anche coerenza e scalabilità su grandi volumi di contenuti digitali.

![Metadati generati dall&#39;IA](/help/assets/assets/enhanced-smart-tags.png)

**Integrazione con Figma**

AEM Assets si integra in modo nativo con Figma, consentendo ai designer di accedere direttamente alle risorse memorizzate in AEM Assets dall’interfaccia utente Figma. Puoi inserire il contenuto gestito in AEM Assets nell’area di lavoro di Figma e quindi salvare il contenuto nuovo o modificato nell’archivio di AEM Assets. Per accedere al connettore AEM Assets disponibile nella pagina della community di Figma, fai clic [qui](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector).

>[!VIDEO](https://video.tv.adobe.com/v/3463828)


### Nuove funzioni in Content Hub {#new-features-content-hub}

**Controllo degli accessi basato su attributi (ABAC)**

[Content Hub ora consente di applicare restrizioni basate su regole per accedere alle risorse](/help/assets/attribute-based-access-control.md). Le autorizzazioni per le risorse garantiscono la governance e assicurano che solo le risorse pertinenti siano accessibili agli utenti.

Le regole di restrizione delle risorse si basano sui metadati e, se le condizioni definite nella regola corrispondono ai metadati della risorsa, la risorsa viene visualizzata ai gruppi di utenti.

Alcuni dei vantaggi principali del controllo degli accessi basato su attributi includono:

* Elimina la dipendenza dalla struttura di cartelle per le autorizzazioni

* Consente agli amministratori di caricare le risorse e determinare retroattivamente le strutture delle autorizzazioni

* Riduce il numero di duplicati, migliorando l&#39;integrità delle risorse. I duplicati sono necessari nelle autorizzazioni basate su cartelle quando le stesse risorse sono condivise con gruppi diversi.

**Branding interfaccia utente**

Content Hub ora consente agli amministratori di [personalizzare l&#39;interfaccia utente con elementi specifici del brand](/help/assets/configure-content-hub-ui-options.md##configure-branding-content-hub), tra cui immagini del banner, titoli dei banner e corpo del testo, nonché colori primari e secondari. Questi miglioramenti contribuiscono a garantire la coerenza del marchio, semplificare l’onboarding degli utenti e creare fiducia.

![Branding interfaccia utente](/help/assets/assets/content-hub-ui-branding.png)

**Condivisione di collegamenti pubblici**

Content Hub ora supporta [la generazione di collegamenti condivisibili per consentire agli utenti esterni](/help/assets/share-assets-content-hub.md##share-assets), senza accesso all&#39;applicazione, di visualizzare i metadati delle risorse o scaricare le risorse.

![Branding interfaccia utente](/help/assets/assets/public-and-private-link.png)

**Governance delle raccolte**

Content Hub ora consente di [controllare l&#39;accesso alle raccolte durante la creazione, in modo che solo gli utenti autorizzati possano visualizzare o gestire risorse raggruppate](/help/assets/collections-content-hub.md##create-collections). Garantisce maggiore sicurezza, migliore collaborazione, gestione organizzata delle risorse e governance semplificata.

>[!VIDEO](https://video.tv.adobe.com/v/3463336)

>[!NOTE]
>
>La governance delle raccolte è una funzione di disponibilità limitata. Per abilitarlo, crea un ticket di supporto.

**Scarica più risorse come file ZIP**

Content Hub ora consente anche di [scaricare le risorse selezionate e le relative rappresentazioni in un file ZIP](/help/assets/download-assets-content-hub.md#download-asset-renditions) e non come file separati, semplificando la gestione dei file.

**Rappresentazioni Dynamic Media in Content Hub**

Accedi a tutte le [copie trasformate predefinite di Dynamic Media e agli smart crop per il download direttamente dall&#39;interfaccia utente di Content Hub](/help/assets/download-assets-content-hub.md#download-asset-renditions).

&#x200B;![Rappresentazioni Dynamic Media](/help/assets/assets/dm-renditions-content-hub.png)

### Nuove funzioni di Dynamic Media {#new-features-dynamic-media}

**Integrazione nativa di Dynamic Media con AJO B2C&#x200B;**

[Integrazione nativa di Dynamic Media di Experience Manager (AEM) con Journey Optimizer (AJO) B2C](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/content-management/combine/aem-dynamic), per consentire agli addetti al marketing di incorporare facilmente le risorse di Dynamic Media di AEM (rendering e modello DM) nei contenuti di AJO e fornire aggiornamenti in tempo reale ed esperienze iperpersonalizzate su tutti i canali.

>[!VIDEO](https://video.tv.adobe.com/v/3463790/?learn=on&enablevpops=&autoplay=true&captions=ita)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Funzioni pre-release

* [Editor universale - Frammenti di modulo](/help/edge/docs/forms/universal-editor/creating-form-fragments.md): l’editor universale ora consente di creare e riutilizzare frammenti di modulo per i moduli adattivi. Questi frammenti sono sezioni di moduli riutilizzabili (ad esempio, dettagli di contatto, campi di consenso) che una volta creati possono essere e applicati a più moduli. Questa funzione semplifica la creazione dei moduli, garantisce la coerenza e migliora l’efficienza nell’authoring.

* [Libreria documenti di SharePoint - Salva allegati con nomi file originali](/help/forms/connect-forms-to-sharepoint-document-library.md#connect-an-adaptive-form-to-microsoft-sharepoint-document-library): ora puoi salvare gli allegati del modulo utilizzando i nomi file originali durante l’archiviazione in una raccolta documenti di SharePoint. Questo miglioramento semplifica l’identificazione e la gestione dei file caricati.

* **Editor di regole**:
   * [Condizione binaria con evento clic nella clausola “When”](/help/forms/rule-editor-core-components-events-operators.md#available-operator-types-and-events-in-rule-editor): l’editor di regole consente ora di combinare un evento di clic su pulsante (_Is Clicked_) con altre condizioni all’interno della clausola “When”. Questo consente un controllo più preciso sull’esecuzione delle regole in base all’interazione utente e ad altri fattori. Nota: quando si utilizzano più condizioni, l’evento clic deve essere la prima condizione elencata.
   * [Condizioni di convalida per campi e pannelli](/help/forms/rule-editor-core-components-usecases.md): l’editor di regole ora include le condizioni _IsValid_ e _IsNotValid_. In questo modo è possibile verificare lo stato di convalida di campi specifici o interi pannelli (inclusi layout come Schede orizzontali, Schede verticali, Pannello a soffietto e Procedure guidate), semplificando la navigazione dei moduli e migliorando l’esperienza utente in base ai risultati della convalida.
* [È stata migliorata la gestione dell’ambito per gli elenchi SharePoint](/help/forms/connect-forms-to-sharepoint-list.md): i siti SharePoint ora supportano tutti i percorsi gestiti, ad esempio /sites e /teams. Questo miglioramento consente un’integrazione più ampia tra diverse strutture del sito SharePoint, offrendo maggiore flessibilità nella connessione ai contenuti organizzativi.
* [Supporto per il salvataggio del documento di record nell’elenco SharePoint](/help/forms/generate-document-of-record-core-components.md#bind-adaptive-form-components-with-template-fields): i moduli creati utilizzando un modello dati modulo (FDM) basato su elenco di SharePoint ora consentono di salvare il documento di record (DoR) negli elenchi di SharePoint configurando la proprietà del campo Riferimento di binding al documento di record. Questo miglioramento consente l’integrazione diretta dei dati e dei documenti dei moduli supportati con l’archiviazione SharePoint.

### Funzionalità per Accesso anticipato in AEM Forms {#forms-new-early-access-features}

Il programma per l’accesso anticipato ad AEM Forms offre un’opportunità unica per ottenere l’accesso esclusivo a innovazioni all’avanguardia e contribuire a modellarne lo sviluppo.

In queste note sulla versione sono elencate le innovazioni incluse nella versione corrente. Per l’elenco completo delle innovazioni disponibili nell’ambito del programma per l’accesso anticipato, consulta la [documentazione del programma per l’accesso anticipato ad AEM Forms](/help/forms/early-access-ea-features.md).

#### Integrazione di Adobe Experience Platform (AEP) con Forms

Le funzionalità di integrazione tra Forms e AEP sono ora disponibili per i primi utilizzatori.

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Processo di obsolescenza aggiornato {#updated-deprecation-process}

Adobe esamina regolarmente funzioni, librerie, API e configurazioni per garantire che soddisfino gli standard in termini di prestazioni, sicurezza e valore. Quando le funzionalità non soddisfano più questi standard, vengono contrassegnate come obsolete e l’utilizzo deve essere interrotto entro una data di rimozione specificata. In attesa di tale data, Adobe ricorderà ai clienti le notifiche e-mail e le azioni da eseguire in Cloud Manager prima di procedere con le nuove build o di distribuirne di nuove. La mancata adozione delle misure necessarie può comportare l’impossibilità di eseguire l’aggiornamento a nuove versioni di AEM, con potenziali impatti su sicurezza, prestazioni, affidabilità e disponibilità.

Per ulteriori informazioni, vedere l&#39;[articolo deprecazione](/help/release-notes/deprecated-removed-features.md).

#### API Java obsolete e configurazione OSGi vicina alle date di rimozione {#deprecated-near-removals}

Espandi l’elenco seguente per visualizzare le API e le configurazioni OSGi obsolete che non devono più essere utilizzate. Per informazioni complete, comprese le timeline di rimozione, consulta l’articolo sugli elementi obsoleti.

<details>
  <summary>Espandi per visualizzare le deprecazioni</summary>

API Java:
* `org.apache.sling.commons.auth`
* `org.apache.felix.webconsole`
* `org.eclipse.jetty`
* `com.mongodb`
* `org.apache.abdera`
* `org.apache.felix.http.whiteboard`
* `org.apache.cocoon.xml`
* `ch.qos.logback`
* `org.slf4j.spi`
* `org.slf4j.event`
* `org.apache.log4j`
* `com.google.common`
* `com.drew`
* `org.bson`
* `org.apache.jackrabbit.oak.plugins.blob`
* `org.apache.jackrabbit.oak.plugins.memory`

Proprietà OSGi:

* `org.apache.sling.commons.log.LogManager` (tutte le proprietà)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)

</details>

### Deprecazione runtime Java 11 {#java11-runtime-deprecation}

Il runtime **Java 11** è ora obsoleto e la maggior parte degli ambienti è già stata aggiornata al runtime **Java 21** più performante.

Se non è stato possibile aggiornare l&#39;ambiente a causa di dipendenze non supportate (vedi [Requisiti di runtime Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)), dovresti aver ricevuto un&#39;e-mail da Adobe con i passaggi successivi specifici. Assicurati che tutti gli aggiornamenti richiesti siano completati entro il **28 agosto 2025**, in modo che l&#39;ambiente possa essere aggiornato senza interruzioni.

Nota: la versione di runtime è separata dalla versione di build del codice. Sebbene sia consigliabile creare con Java 21, le build Java 11 sono ancora supportate per il momento. In futuro verrà condiviso un avviso di rimozione separato per le build Java 11.

### Applicazione dei criteri di configurazione dei registri Java di AEM {#logconfig-policy}

Come indicato nelle note sulla versione di aprile, i registri Java di AEM devono seguire un formato standard per garantire un monitoraggio affidabile in tutti gli ambienti dei clienti. Le configurazioni di registro personalizzate, ad esempio modifiche alla formattazione del registro, ai file di output o ai livelli di registro predefiniti, non sono più supportate. I registri devono rimanere indirizzati ai file predefiniti e i livelli di registro predefiniti per il codice prodotto AEM devono essere mantenuti. Vedi tutti i dettagli nell&#39;articolo [Registrazione](/help/implementing/developing/introduction/logging.md#configuration-loggers).

A partire dalla **fine di agosto**, le sostituzioni di registrazione personalizzate non supportate verranno ignorate. In base alla nostra analisi, la maggior parte dei clienti non sarà interessata e Adobe contatterà direttamente tutti i clienti la cui configurazione corrente potrebbe essere interessata.

Rivedi e aggiorna eventuali processi a valle che si basano su un comportamento di registrazione personalizzato. Ad esempio:

* Se il sistema di inoltro dei registri prevede un formato di registro personalizzato, potrebbe essere necessario modificare le regole di acquisizione.
* Se in precedenza è stato ridotto il livello di dettaglio del registro modificando i livelli del registro, il ripristino dei livelli predefiniti potrebbe aumentare il volume del registro.

### Rimozione predefinita delle versioni precedenti e dei registri di controllo {#mt-defaults}

Attualmente, le *attività di manutenzione dell&#39;eliminazione* associate alle versioni di contenuto e ai registri di audit sono disabilitate per impostazione predefinita, pertanto nessun dato viene rimosso a meno che non sia configurato in modo esplicito tramite le rispettive proprietà OSGi.

Tuttavia, per ottimizzare le prestazioni dell’archivio, a partire da **fine giugno 2025**, la rimozione sarà abilitata per impostazione predefinita, seguendo queste linee guida:

#### Versioni contenuto {#mt-content}

* **Nuovi ambienti** (creati dopo una data futura (da comunicare in un secondo momento)
   * Le versioni precedenti a **30 giorni** verranno eliminate periodicamente.
   * Vengono mantenute le cinque versioni più recenti degli ultimi 30 giorni, insieme alla versione più recente e a quella corrente, indipendentemente dalla loro età.

* **Ambienti esistenti** (creati prima di questa data):
   * Le versioni precedenti a **7 anni** verranno eliminate periodicamente.
   * Vengono mantenute tutte le versioni degli ultimi 7 anni.
   * Questa soglia predefinita elevata impedisce la rimozione involontaria dei dati recenti. Tuttavia, si consiglia di configurare valori inferiori per ottimizzare le prestazioni dell’archivio.

* Puoi modificare queste impostazioni predefinite tramite sostituzioni della configurazione OSGi.

#### Registro di controllo {#mt-auditlogs}

* **Nuovi ambienti** (creati dopo una data futura, che verrà comunicata separatamente):
   * I registri di replica, DAM e di controllo delle pagine precedenti a **7 giorni** verranno eliminati periodicamente.
   * Tutti gli eventi vengono registrati per impostazione predefinita.

* **Ambienti esistenti** (creati prima di questa data):
   * I registri di replica, DAM e controllo delle pagine più vecchi di **7 anni** verranno eliminati periodicamente.
   * Tutti gli eventi vengono registrati per impostazione predefinita.
   * Questa soglia predefinita elevata impedisce la rimozione involontaria dei dati recenti. Tuttavia, si consiglia di configurare valori inferiori per ottimizzare le prestazioni dell’archivio.

* Puoi modificare queste impostazioni predefinite tramite sostituzioni della configurazione OSGi.

Per ulteriori dettagli, vedere l&#39;articolo [Attività di manutenzione](/help/operations/maintenance.md#defaults).

### Elaborazione Edge (programma Alpha) {#edge-computing}

Il computing Edge consente di eseguire JavaScript a livello CDN, avvicinando l’elaborazione dei dati all’utente finale. Questo riduce la latenza e consente esperienze dinamiche reattive ai margini.

I casi d’uso comuni includono:

* Autenticazione degli utenti con un provider di identità prima di concedere l’accesso al contenuto
* Personalizzazione dei contenuti in base alla geolocalizzazione, al tipo di dispositivo o agli attributi utente
* Funge da middleware tra la rete CDN e l’origine
* Riformattazione delle risposte da API di terze parti (e forse aggregazione di più risposte API) prima di distribuirle al browser
* Composizione e distribuzione di HTML con rendering server alla rete Edge tramite contenuti uniti da vari back-end

Abbiamo un numero limitato di opportunità disponibili per i progetti AEM Publish Delivery o Edge Delivery Services per i siti di produzione live. Se sei interessato a partecipare o desideri saperne di più, invia un&#39;e-mail a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descrizione del tuo caso d&#39;uso.

### Configurazione CDN per Edge Delivery Services (programma Beta) {#cdn-eds-beta}

La rete CDN gestita da Adobe offre opzioni di configurazione flessibili, come descritto nell&#39;articolo [Pipeline di configurazione](/help/operations/config-pipeline.md#configurations).

Ora in versione beta, distribuisci una pipeline di configurazione per le funzioni che includono i selettori di origine CDN, le trasformazioni di risposta e richiesta e altro ancora. Rivolgiti a [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) con i dettagli del tuo caso d&#39;uso.

### Inoltro dei registri di AEM a più destinazioni (programma Beta) {#log-forwarding-beta}

Anche se i registri di AEM possono essere scaricati da Cloud Manager, molte organizzazioni trovano utile inviare in streaming tali registri a una destinazione di registrazione preferita. AEM supporta già l’inoltro dei registri AEM e CDN ad Azure Blob Storage, Datadog, HTTPS, Elasticsearch (e OpenSearch) e Splunk. Questa funzione è configurata in modo autonomo e distribuita mediante la pipeline di configurazione.

Ora in versione beta, puoi inoltrare i registri di AEM a Amazon S3, Sumo Logic e al tuo account New Relic (non a quello fornito da Adobe). I registri di AEM (incluso Apache/Dispatcher) sono supportati per queste destinazioni di registrazione, ma non per i registri CDN. Invia un’e-mail a [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) per accedere.

Ulteriori informazioni sono disponibili nella [documentazione sull’inoltro dei registri](/help/implementing/developing/introduction/log-forwarding.md).

## Guide di [!DNL Experience Manager] {#guides}

L’elenco completo delle funzioni nuove e migliorate dell’ultima versione delle Guide di Adobe Experience Manager è disponibile [qui](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Editor universale {#universal-editor}

L’elenco completo dei rilasci dell’editor universale è disponibile [qui](/help/release-notes/universal-editor/current.md).

## Generare varianti {#generate-variations}

L’elenco completo dei rilasci di generare varianti è disponibile [qui](/help/generative-ai/release-notes-generate-variations.md).

## Note sulla versione di Experience Cloud {#experience-cloud}

Informazioni sulle versioni di altre applicazioni Experience Cloud sono disponibili [qui](https://experienceleague.adobe.com/it/docs/release-notes/experience-cloud/current).
