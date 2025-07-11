---
title: Note sulla versione 2025.5.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2025.5.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
feature: Release Information
role: Admin
exl-id: b7a21533-9db1-4111-814c-cab917041be4
source-git-commit: c8391e09b7e2888423187f48360423c52b18fe0a
workflow-type: tm+mt
source-wordcount: '2162'
ht-degree: 93%

---

# Note sulla versione 2025.5.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione funzionale 2025.5.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2023 o 2024.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Per ricevere una notifica e-mail mensile sugli aggiornamenti delle note sulla versione di Experience Cloud, abbonati ad [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).

## Data di pubblicazione {#release-date}

La data di rilascio della versione funzionale corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2025.5.0) è il 5 giugno 2025. La prossima versione funzionale (2025.6.0) è pianificata per il 26 giugno 2025.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica della versione di maggio 2025 per un riepilogo delle funzioni aggiunte alla versione 2025.5.0:

>[!VIDEO](https://video.tv.adobe.com/v/3464358?quality=12&captions=ita)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Metadati generati dall’IA**

AEM Assets ora utilizza l’[IA per generare automaticamente i metadati, inclusi Titolo, Descrizione e Parole chiave](/help/assets/metadata-assets-view.md#ai-smart-tags). Questi campi generati dall’IA migliorano la precisione dei metadati, rendendo le risorse più facili da ricercare, classificare e consigliare. Questo approccio non solo migliora l’efficienza eliminando l’assegnazione tag manuale, ma garantisce anche coerenza e scalabilità su grandi volumi di contenuto digitale.

![Metadati generati dall’IA](/help/assets/assets/enhanced-smart-tags.png)

**Integrazione con Figma**

AEM Assets si integra in modo nativo con Figma, che consente agli sviluppatori di accedere direttamente alle risorse memorizzate in AEM Assets dall’interfaccia utente. Puoi posizionare il contenuto gestito in AEM Assets nell’area di lavoro di Figma e quindi salvare il nuovo o quello modificato in un archivio AEM Assets. Per accedere al connettore AEM Assets disponibile nella pagina della community di Figma, fai clic [qui](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector).

>[!VIDEO](https://video.tv.adobe.com/v/3463828)


### Nuove funzioni in Content Hub {#new-features-content-hub}

**Controllo degli accessi basato su attributi (ABAC)**

[Content Hub ora consente di applicare restrizioni basate su regole per accedere alle risorse](/help/assets/attribute-based-access-control.md). Le autorizzazioni per le risorse garantiscono la governance e assicurano che solo le risorse pertinenti siano accessibili agli utenti.

Le regole di limitazione delle risorse si basano sui metadati e, se le condizioni definite nella regola corrispondono ai metadati della risorsa, la risorsa viene visualizzata ai gruppi di utenti.

Alcuni dei vantaggi principali del controllo degli accessi basato su attributi includono:

* Eliminazione della dipendenza dalla struttura di cartelle per le autorizzazioni

* Consenso agli amministratori di caricare le risorse e determinare retroattivamente le strutture delle autorizzazioni

* Riduzione del numero di duplicati, migliorando l’integrità della risorsa. I duplicati sono necessari nelle autorizzazioni basate su cartelle quando le stesse risorse sono condivise con gruppi diversi.

**Branding interfaccia utente**

Content Hub ora consente agli amministratori di [personalizzare l’interfaccia utente con elementi specifici del brand](/help/assets/configure-content-hub-ui-options.md##configure-branding-content-hub), tra cui immagini del banner, titoli dei banner e corpo del testo, nonché colori primari e secondari. Questi miglioramenti contribuiscono a garantire la coerenza del brand, semplificare l’onboarding degli utenti e creare fiducia.

![Branding interfaccia utente](/help/assets/assets/content-hub-ui-branding.png)

**Condivisione del collegamento pubblico**

Content Hub ora supporta la [generazione di collegamenti condivisibili per consentire agli utenti esterni](/help/assets/share-assets-content-hub.md##share-assets), senza accesso all’applicazione, di visualizzare i metadati delle risorse o scaricarle.

![Branding interfaccia utente](/help/assets/assets/public-and-private-link.png)

**Governance delle raccolte**

Content Hub ora consente di [controllare l’accesso alle raccolte durante la creazione, in modo che solo gli utenti autorizzati possano visualizzare o gestire risorse raggruppate](/help/assets/collections-content-hub.md##create-collections). Ciò garantisce maggiore sicurezza, migliore collaborazione, gestione risorse organizzata e governance semplificata.

>[!VIDEO](https://video.tv.adobe.com/v/3463336)

>[!NOTE]
>
>La governance delle raccolte è una funzione di disponibilità limitata. Per abilitarla, crea un ticket di supporto.

**Scarica più risorse come file ZIP**

Content Hub ora consente anche di [scaricare le risorse selezionate e le relative rappresentazioni in un file ZIP](/help/assets/download-assets-content-hub.md#download-asset-renditions) e non come file separati, semplificandone la gestione.

**Rappresentazioni Dynamic Media in Content Hub**

Accedi a tutte le [rappresentazioni predefinite di Dynamic Media e ai ritagli avanzati per il download direttamente dall’interfaccia utente di Content Hub](/help/assets/download-assets-content-hub.md#download-asset-renditions).

![Rappresentazioni di Dynamic Media](/help/assets/assets/dm-renditions-content-hub.png)

### Nuove funzioni in Dynamic Media {#new-features-dynamic-media}

**Integrazione nativa di Dynamic Media con AJO B2C**

[Integrazione nativa di Dynamic Media di Experience Manager (AEM) con Journey Optimizer (AJO) B2C](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/content-management/combine/aem-dynamic), per consentire agli addetti marketing di incorporare facilmente le risorse di Dynamic Media di AEM (rappresentazione e modello DM) nel contenuto di AJO e consegnare aggiornamenti in tempo reale ed esperienze iperpersonalizzate su tutti i canali.

>[!VIDEO](https://video.tv.adobe.com/v/3463790/?learn=on&enablevpops=&autoplay=true&captions=ita)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Funzioni pre-release

* [Editor universale per Forms adattivo e frammenti di modulo](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md): l&#39;editor universale ora supporta la creazione sia di Forms adattivo che di frammenti di modulo riutilizzabili. Gli autori possono creare moduli visivamente, configurare azioni di invio e aggiungere la convalida reCAPTCHA, il tutto in un ambiente di authoring WYSIWYG semplificato. Questa funzionalità accelera la creazione dei moduli, migliora la coerenza e migliora la protezione contro spam e abusi automatizzati.

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

* [Integrazione di AEM Forms con Adobe Experience Platform](/help/forms/aem-forms-aep-connector.md): il connettore da AEM Forms a Adobe Experience Platform consente l&#39;integrazione diretta tra Adaptive Forms e Adobe Experience Platform. Questa funzione consente di mappare i dati del modulo su schemi XDM e inviarli direttamente ad AEP in tempo reale. Semplifica l’acquisizione dei dati per casi di utilizzo di personalizzazione e attivazione tra le soluzioni Adobe Experience Cloud.

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Processo di rimozione aggiornato {#updated-deprecation-process}

Adobe esamina regolarmente funzioni, librerie, API e configurazioni per garantire che soddisfino gli standard in termini di prestazioni, sicurezza e valore. Quando le funzionalità non soddisfano più questi standard, vengono contrassegnate come obsolete e l’utilizzo ne deve essere interrotto entro una data di rimozione specificata. In attesa di tale data, Adobe lo ricorderà alla clientela tramite notifiche e-mail e azioni da eseguire in Cloud Manager, prima di procedere con le nuove build o di distribuirne di nuove. La mancata adozione delle misure necessarie può comportare l’impossibilità di eseguire l’aggiornamento a nuove versioni di AEM, generando potenziali impatti su sicurezza, prestazioni, affidabilità e disponibilità.

Per ulteriori informazioni, consulta l’articolo [Rimozione](/help/release-notes/deprecated-removed-features.md).

#### API Java obsolete e configurazione OSGi prossime alle date di rimozione {#deprecated-near-removals}

Espandi l’elenco seguente per visualizzare le API e le configurazioni OSGi obsolete che non devono più essere utilizzate. Per informazioni complete, comprese le timeline di rimozione, consulta l’articolo sulla rimozione.

<details>
  <summary>Espandi per visualizzare le rimozioni</summary>

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

### Rimozione runtime Java 11 {#java11-runtime-deprecation}

Il **runtime Java 11** è ora obsoleto e la maggior parte degli ambienti è stata già aggiornata al runtime **Java 21** più performante.

Se non è stato possibile aggiornare l’ambiente a causa di dipendenze non supportate (consulta [Requisiti di runtime Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)), dovresti aver ricevuto un’e-mail da Adobe con i passaggi successivi specifici. Assicurati che tutti gli aggiornamenti richiesti siano completati entro il **28 agosto 2025**, in modo che l’ambiente possa essere aggiornato senza interruzioni.

Nota: la versione di runtime è separata dalla versione di build del codice. Sebbene consigliamo di creare con Java 21, le build Java 11 sono ancora supportate per il momento. In futuro verrà condiviso un avviso di rimozione separato per le build Java 11.

### Applicazione dei criteri di configurazione dei registri Java di AEM {#logconfig-policy}

Come indicato nelle note sulla versione di aprile, i registri Java di AEM devono seguire un formato standard per garantire un monitoraggio affidabile in tutti gli ambienti del cliente. Le configurazioni di registro personalizzate, ad esempio modifiche alla formattazione del registro, ai file di output o ai livelli di registro predefiniti, non sono più supportate. I registri devono rimanere indirizzati ai file predefiniti e i livelli di registro predefiniti per il codice prodotto AEM devono essere mantenuti. Consulta tutti i dettagli nell’articolo [Registrazione](/help/implementing/developing/introduction/logging.md#configuration-loggers).

A partire dalla **fine di agosto**, qualsiasi sostituzione di registrazione personalizzata non supportate verrà ignorata. In base alla nostra analisi, la maggior parte della clientela non sarà interessata e Adobe contatterà direttamente tutti coloro la cui configurazione corrente potrebbe essere interessata.

Rivedi e aggiorna eventuali processi a valle che si basano su un comportamento di registrazione personalizzato. Ad esempio:

* Se il sistema di inoltro dei registri prevede un formato di registro personalizzato, potrebbe essere necessario modificare le regole di acquisizione.
* Se in precedenza è stato ridotto il livello di verbosità del registro modificando i livelli del registro, il ripristino dei livelli predefiniti potrebbe aumentare il volume del registro.

### Eliminazione predefinita delle versioni precedenti e dei registri di controllo {#mt-defaults}

Attualmente, le *attività di manutenzione dell’eliminazione* associate alle versioni di contenuto e ai registri di controllo sono disabilitate per impostazione predefinita, pertanto nessun dato viene rimosso, a meno che questo non sia configurato in modo esplicito.

Tuttavia, per ottimizzare le prestazioni dell’archivio, a partire da **fine giugno 2025**, l’eliminazione sarà abilitata per impostazione predefinita, seguendo queste linee guida:

#### Versioni di contenuto {#mt-content}

* **Nuovi ambienti** (creati dopo una data prossima (da comunicare in un secondo momento)
   * Le versioni precedenti a **30 giorni** verranno eliminate periodicamente.
   * Vengono mantenute le cinque versioni più recenti degli ultimi 30 giorni, insieme alla versione più recente e a quella corrente, indipendentemente dalla loro età.

* **Ambienti esistenti** (creati prima di questa data):
   * Le versioni precedenti a **7 anni** verranno eliminate periodicamente.
   * Vengono mantenute tutte le versioni degli ultimi 7 anni.
   * Questa soglia predefinita elevata impedisce la rimozione involontaria dei dati recenti. Tuttavia, si consiglia di configurare valori inferiori per ottimizzare le prestazioni dell’archivio.

* Puoi modificare questi valori predefiniti tramite la configurazione YAML, distribuita mediante la pipeline di configurazione.

#### Registro di controllo {#mt-auditlogs}

* **Nuovi ambienti** (creati dopo una data prossima, che verrà comunicata separatamente):
   * I registri di controllo della pagina, DAM e di replica precedenti a **7 giorni** verranno eliminati periodicamente.
   * Tutti gli eventi vengono registrati per impostazione predefinita.

* **Ambienti esistenti** (creati prima di questa data):
   * I registri di controllo della pagina, DAM e di replica precedenti a **7 anni** verranno eliminati periodicamente.
   * Tutti gli eventi vengono registrati per impostazione predefinita.
   * Questa soglia predefinita elevata impedisce la rimozione involontaria dei dati recenti. Tuttavia, si consiglia di configurare valori inferiori per ottimizzare le prestazioni dell’archivio.

* Puoi modificare questi valori predefiniti tramite la configurazione YAML, distribuita mediante la pipeline di configurazione.

Per ulteriori dettagli, consulta l’articolo [Attività di manutenzione](/help/operations/maintenance.md#defaults).

### Edge Computing (programma Alpha) {#edge-computing}

Edge Computing consente di eseguire JavaScript a livello CDN, avvicinando l’elaborazione dati all’utente finale. Questo riduce la latenza e consente esperienze dinamiche reattive ai margini.

I casi d’uso comuni includono:

* Autenticazione degli utenti con un provider di identità prima di concedere l’accesso al contenuto
* Personalizzazione del contenuto in base alla geolocalizzazione, al tipo di dispositivo o agli attributi utente
* Funge da middleware tra la rete CDN e l’origine
* Riformattazione delle risposte da API di terze parti (e forse aggregazione di più risposte API) prima di distribuirle al browser
* Composizione e trasmissione di HTML con rendering del server alla rete Edge tramite contenuti uniti da vari back-end

Abbiamo un numero limitato di opportunità disponibili per i progetti AEM Publish Delivery o Edge Delivery Services per i siti di produzione live. Se sei interessato a partecipare o desideri saperne di più, invia un’e-mail a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descrizione del tuo caso d’uso.

### Configurazione rete CDN per Edge Delivery Services (programma Beta) {#cdn-eds-beta}

La rete CDN gestita da Adobe offre opzioni di configurazione flessibili, come descritto nell’articolo [Pipeline di configurazione](/help/operations/config-pipeline.md#configurations).

Ora in versione beta, distribuisci una pipeline di configurazione per le funzioni che includono i selettori di origine CDN, le trasformazioni di risposta e richiesta e altro ancora. Rivolgiti a [aemcs-cdn-config-adopter@adobe.com](mailto:aemcs-cdn-config-adopter@adobe.com) con i dettagli del tuo caso d’uso.

### Funzionalità di inoltro del registro di AEM a più destinazioni (programma Beta) {#log-forwarding-beta}

Anche se i registri di AEM possono essere scaricati da Cloud Manager, molte organizzazioni trovano utile inviare in streaming tali registri a una destinazione di registrazione preferita. AEM supporta già l’inoltro dei registri CDN e AEM all’archiviazione BLOB di Azure, Datadog, HTTPS, Elasticsearch (e OpenSearch) e Splunk. Questa funzione è configurata in modo autonomo e distribuita mediante la pipeline di configurazione.

Ora in versione Beta, puoi inoltrare i registri di AEM a Amazon S3, Sumo Logic e al tuo account New Relic (non a quello fornito da Adobe). Per queste destinazioni di registrazione, sono supportati i registri di AEM (incluso Apache/Dispatcher), ma non i registri CDN. Invia un’e-mail a [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) per accedere.

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
