---
title: Note sulla versione 2025.4.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2025.4.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 48e09824-5c67-49d8-8896-358d679649fc
source-git-commit: 0664e5dc4a7619a52cd28c171a44ba02c592ea3d
workflow-type: tm+mt
source-wordcount: '1828'
ht-degree: 97%

---

# Note sulla versione 2025.4.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione funzionale 2025.4.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2023 o 2024.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Per ricevere una notifica e-mail mensile sugli aggiornamenti delle note sulla versione di Experience Cloud, abbonati ad [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).

## Data di pubblicazione {#release-date}

La data di rilascio della versione corrente della funzione di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2025.4.0) è venerdì 24 aprile 2025. La prossima versione funzionale (2025.5.0) è pianificata per il 5 giugno 2025.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica sulla versione di aprile 2025 per un riepilogo delle funzioni aggiunte alla versione 2025.4.0:

>[!VIDEO](https://video.tv.adobe.com/v/3463991?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in Experience Manager Sites {#enhancements-sites}

**Nuova interfaccia utente di amministrazione del modello per frammenti di contenuto**

A completamento dell’elenco delle nuove interfacce utente lato client quando si utilizzando i Frammenti di contenuto di AEM, è ora disponibile una nuova interfaccia utente di amministrazione per modelli per frammenti di contenuto. La nuova interfaccia utente fornisce una vista elenco moderna e pulita che consente di cercare i modelli con filtri e che mostra i tag dei modelli e quali frammenti di contenuto esistenti sono basati su un determinato modello. La documentazione è disponibile [qui](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md).

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media (Scene7) {#dynamic-media-scene7}

**Dynamic Media (Scene7) non è supportato negli ambienti di sicurezza avanzata**

Dynamic Media (Scene7) su AEM as a Cloud Service non è compatibile con HIPAA e non può essere utilizzato in ambienti AEM in cui è abilitata la sicurezza avanzata.

A partire dalla versione di AEM as a Cloud Service di aprile 2025, una restrizione tecnica impedisce la configurazione di Dynamic Media (Scene7) in ambienti con sicurezza avanzata. Di conseguenza, in questi ambienti la scheda **Configurazione Dynamic Media** in **Strumenti** > **Servizi cloud** non è più visibile.

Inoltre, la clientela che utilizza AEM 6.5 deve essere consapevole che lo stack Dynamic Media (Scene7) non è compatibile con HIPAA.

### Dynamic Media Classic {#dynamic-media-classic}

**Reporting**

La scheda Larghezza di banda nella dashboard di reporting di Dynamic Media Classic non è più supportata da aprile 2025.

Consulta [Larghezza di banda e archiviazione, tipi di rapporti](https://experienceleague.adobe.com/it/docs/dynamic-media-classic/using/setup/administration-setup#types-of-reports).

## Nuove funzioni nella vista Risorse {#new-features-assets-view}

**Relazioni risorsa**

La vista risorse ora supporta la visualizzazione e la modifica delle relazioni tra risorse in un pannello semplificato Dettagli risorsa. Aggiungi facilmente relazioni come Origine e Derivata ai contenuti in modo che gli utenti possano trovare più efficacemente contenuti principali rilevanti.

![Esempio di relazione risorse](/help/assets/assets/asset-relations-example.png)

**Visualizzare le versioni di una risorsa**

Ora puoi selezionare e confrontare rapidamente qualsiasi versione di una risorsa con la versione più recente utilizzando la vista Risorse.

![confronta le versioni della risorsa](/help/assets/assets/version-compare2.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Funzioni pre-release

* [Editor universale per moduli adattivi e frammenti di modulo](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md): l’editor universale ora supporta la creazione sia di moduli adattivi che di frammenti di modulo riutilizzabili. Gli autori possono creare moduli visivamente, configurare azioni di invio e aggiungere la convalida reCAPTCHA, il tutto in un ambiente di authoring WYSIWYG semplificato. Questa funzionalità accelera la creazione di moduli, ne incrementa la coerenza e ne migliora la protezione contro spam e abusi automatizzati.

* [Libreria documenti di SharePoint - Salva allegati con nomi file originali](/help/forms/connect-forms-to-sharepoint-document-library.md#connect-an-adaptive-form-to-microsoft-sharepoint-document-library): ora puoi salvare gli allegati del modulo utilizzando i nomi file originali durante l’archiviazione in una raccolta documenti di SharePoint. Questo miglioramento semplifica l’identificazione e la gestione dei file caricati.

* **Editor di regole**:
   * [Condizione binaria con evento clic nella clausola “When”](/help/forms/rule-editor-core-components-events-operators.md#available-operator-types-and-events-in-rule-editor): l’editor di regole consente ora di combinare un evento di clic su pulsante (_Is Clicked_) con altre condizioni all’interno della clausola “When”. Questo consente un controllo più preciso sull’esecuzione delle regole in base all’interazione utente e ad altri fattori. Nota: quando si utilizzano più condizioni, l’evento clic deve essere la prima condizione elencata.
   * [Condizioni di convalida per campi e pannelli](/help/forms/rule-editor-core-components-usecases.md): l’editor di regole ora include le condizioni _IsValid_ e _IsNotValid_. In questo modo è possibile verificare lo stato di convalida di campi specifici o interi pannelli (inclusi layout come Schede orizzontali, Schede verticali, Pannello a soffietto e Procedure guidate), semplificando la navigazione dei moduli e migliorando l’esperienza utente in base ai risultati della convalida.
* [È stata migliorata la gestione dell’ambito per gli elenchi SharePoint](/help/forms/connect-forms-to-sharepoint-list.md): i siti SharePoint ora supportano tutti i percorsi gestiti, ad esempio /sites e /teams. Questo miglioramento consente un’integrazione più ampia tra diverse strutture del sito SharePoint, offrendo maggiore flessibilità nella connessione ai contenuti organizzativi.
* [Supporto per il salvataggio del documento di record nell’elenco SharePoint](/help/forms/generate-document-of-record-core-components.md#bind-adaptive-form-components-with-template-fields): i moduli creati utilizzando un modello dati modulo (FDM) basato su elenco di SharePoint ora consentono di salvare il documento di record (DoR) negli elenchi di SharePoint configurando la proprietà del campo Riferimento di binding al documento di record. Questo miglioramento consente l’integrazione diretta dei dati e dei documenti dei moduli supportati con l’archiviazione SharePoint.
* [Supporto di mappatura automatica per frammenti di moduli adattivi](/help/forms/adaptive-form-fragments-core-components.md#auto-mapping-support-for-fragments-in-an-adaptive-form): Forms adattivo ora supporta l&#39;inserimento automatico dei frammenti corrispondenti quando gli oggetti dello schema vengono allineati a una struttura di frammenti definita, semplificando la creazione dei moduli e promuovendo il riutilizzo.

### Funzionalità per Accesso anticipato in AEM Forms {#forms-new-early-access-features}

Il programma per l’accesso anticipato ad AEM Forms offre un’opportunità unica per ottenere l’accesso esclusivo a innovazioni all’avanguardia e contribuire a modellarne lo sviluppo.

In queste note sulla versione sono elencate le innovazioni incluse nella versione corrente. Per l’elenco completo delle innovazioni disponibili nell’ambito del programma per l’accesso anticipato, consulta la [documentazione del programma per l’accesso anticipato ad AEM Forms](/help/forms/early-access-ea-features.md).

#### Integrazione di Adobe Experience Platform (AEP) con Forms

* [Integrazione di AEM Forms con Adobe Experience Platform](/help/forms/aem-forms-aep-connector.md): il connettore da AEM Forms a Adobe Experience Platform consente l’integrazione diretta tra i moduli adattivi e Adobe Experience Platform. Questa funzione consente di mappare i dati del modulo su schemi XDM e inviarli direttamente a AEP in tempo reale. Semplifica l’acquisizione dei dati per casi d’uso di personalizzazione e attivazione tra le soluzioni Adobe Experience Cloud.

## Componente aggiuntivo CIF {#cloud-services-cif}

### Miglioramenti {#enhancements-cif}

* È stata aggiunta la selezione della variante di prodotto per il tipo di dati di riferimento prodotto CIF
* **Sperimentale**: [JSON+LD nei componenti core CIF nei PDP](/help/commerce-cloud/cif-storefront/customizing/json-ld.md)
* **Sperimentale**: [CIF è in grado di cancellare la cache](/help/commerce-cloud/cif-storefront/configuring/clear-cache.md)

### Correzioni di bug {#bug-fixes-cif}

* Correzione del problema di ricerca nel campo del prodotto
* Il formato dell’URL del prodotto non funziona come previsto per #variant_sku.
* Impossibile aggiungere più di 20 SKU al componente Elenco prodotti.

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### API basate su OpenAPI {#open-apis}

Gli sviluppatori possono integrare in modo approfondito le funzionalità di AEM as a Cloud Service nelle proprie applicazioni e strumenti. Le nuove API di AEM as a Cloud Service seguono le specifiche OpenAPI, con l’obiettivo di essere coerenti, ben documentate e di facile utilizzo. Le credenziali per gli endpoint che richiedono l’autenticazione vengono generate creando progetti Adobe Developer Console e supportano OAuth server-to-server, app web e applicazioni a pagina singola.

[Consulta l’elenco completo](https://developer.adobe.com/experience-cloud/experience-manager-apis/#openapi-based-apis) di API basate su OpenAPI, [scopri di più](/help/implementing/developing/open-api-based-apis.md) e prova un [tutorial end-to-end](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/aem-apis/openapis/invoke-api-using-oauth-s2s) che ne illustra la configurazione e l’utilizzo.

Guarda questo video per scoprire come configurare un’API autenticata per un utilizzo successivo:

>[!VIDEO](https://video.tv.adobe.com/v/3457510?quality=12&learn=on)

### Miglioramenti relativi alla configurazione CDN {#cdn-enhancements}

La rete CDN gestita da Adobe offre opzioni di configurazione flessibili, come descritto nell’[articolo sulle pipeline di configurazione](/help/operations/config-pipeline.md#configurations). Di seguito sono riportate alcune funzioni recenti:

#### Includi proprietà aggiuntive nei registri CDN {#props-in-cdnlogs}

Utile per scenari quali il debug e l’analisi dei dati, consente di includere ulteriori informazioni nei registri CDN oltre alle proprietà predefinite impostando l’azione `logProperty` in [trasformazioni di richieste e risposte](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations).

#### Proprietà di area geografica, continente e organizzazione come condizioni corrispondenti {#matching-conditions}

Le regole CDN ora possono corrispondere in base all’area geografica, al continente e all’organizzazione per i casi d’uso tra cui il blocco del traffico e i reindirizzamenti. `clientRegion` e `clientContinent` incrementano il `clientCountry` già supportato per la corrispondenza basata sulla posizione geografica, mentre `clientAsName` e `clientAsNumber` corrispondono ai sistemi autonomi per identificare ISP, aziende o provider cloud di grandi dimensioni. Ulteriori informazioni su queste [proprietà di richiesta appena esposte](/help/security/traffic-filter-rules-including-waf.md#condition-structure).

#### Imposta valore dei cookie {#cookie-attributes}

È possibile impostare gli attributi dei cookie in [trasformazioni di risposte](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations).

### Supporto Java 21 {#java21}

A partire dalla versione di gennaio, è possibile generare codice con Java 21 e Java 17. È possibile accedere a nuove funzioni quali corrispondenza pattern, classi sigillate e vari miglioramenti delle prestazioni. Per i passaggi di configurazione, incluso l’aggiornamento delle versioni del progetto Maven e della libreria, consulta l’articolo [Ambiente di build](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support).

Il **runtime** Java 21, con prestazioni più elevate, verrà distribuito automaticamente quando viene rilevata una build Java 17 o 21. Tuttavia, è anche consigliabile optare per il runtime Java 21 per gli ambienti creati con Java 11, inviando un’e-mail a [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com). Informazioni sui [requisiti del runtime Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).

>[!IMPORTANT]
>
> Il **runtime** Java 21 è stato distribuito negli ambienti di sviluppo/RDE a febbraio; verrà applicato agli ambienti di staging/produzione il **28 e 29 aprile**. Tieni presente che **la generazione del codice** con Java 21 (o Java 17) è indipendente dal runtime di Java 21. È necessario eseguire in modo esplicito i passaggi per generare il codice con Java 21 (o Java 17).

### Applicazione dei criteri di configurazione della registrazione di AEM {#logconfig-policy}

Per garantire un monitoraggio efficace degli ambienti della clientela, i registri Java di AEM devono mantenere un formato coerente e non devono essere sostituiti da configurazioni personalizzate. L’output del registro deve rimanere indirizzato ai file predefiniti. Per il codice prodotto AEM, è necessario mantenere i livelli di registro predefiniti. Tuttavia, è accettabile regolare i livelli di registro per il codice sviluppato dalla clientela.

A tal fine, non è necessario apportare modifiche alle seguenti proprietà OSGi:
* **Configurazione registro Apache Sling** (PID: `org.apache.sling.commons.log.LogManager`): *tutte le proprietà*
* **Configurazione logger registrazione Sling Apache** (PID di fabbrica: `org.apache.sling.commons.log.LogManager.factory.config`):
   * `org.apache.sling.commons.log.file`
   * `org.apache.sling.commons.log.pattern`

A metà maggio, AEM applicherà un criterio in base al quale eventuali modifiche personalizzate a queste proprietà verranno ignorate. Rivedi e adegua di conseguenza i processi a valle. Ad esempio, se utilizzi la funzione di inoltro del registro:
* Se la destinazione di registrazione prevede un formato di registro personalizzato (non predefinito), potrebbe essere necessario aggiornare le regole di acquisizione.
* Se le modifiche ai livelli di registro ne riducono la verbosità, tieni presente che i livelli di registro predefiniti possono causare un aumento significativo del rispettivo volume.

### Funzionalità di inoltro del registro di AEM a più destinazioni: programma Beta {#log-forwarding-earlyadopter}

Ora, in versione Beta, è possibile inoltrare i registri di AEM a New Relic (utilizzando HTTPS), Amazon S3 e Sumo Logic. Sono supportati i registri di AEM (incluso Apache/Dispatcher), ma non i registri CDN. Invia un’e-mail a [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) per accedere.

Anche se i registri di AEM possono essere scaricati da Cloud Manager, molte organizzazioni trovano utile inviare in streaming tali registri a una destinazione di registrazione preferita. AEM supporta già l’inoltro dei registri CDN e AEM (disponibilità generale) all’archiviazione BLOB di Azure, Datadog, HTTPS, Elasticsearch (e OpenSearch) e Splunk. Questa funzione è configurata in modo autonomo e distribuita mediante la pipeline di configurazione.

Ulteriori informazioni sono disponibili nella [documentazione sull’inoltro dei registri](/help/implementing/developing/introduction/log-forwarding.md).

### Edge Computing - Richiesta di feedback! {#edge-computing-feedback}

L’Edge computing avvicina l’elaborazione dei dati al browser, il che offre vantaggi quali una latenza ridotta. Adobe desidera ricevere commenti sull’utilità di questa tecnologia per i progetti Pubblica cosegna AEM e Edge Delivery Services. Inoltre, il modo in cui pensi di utilizzarla per contribuire alla roadmap.

Alcuni possibili casi d’uso:

* Autenticazione con un IdP per ottenere l’accesso al contenuto
* Personalizzazione per il rendering di contenuti dinamici in base alla geolocalizzazione, al tipo di dispositivo, agli attributi utente e così via.
* Manipolazione avanzata delle immagini
* Middleware tra la rete CDN e un’origine
* Un livello tra il browser e un’API di terze parti, forse per riformattare la risposta API
* Aggregazione di dati da più origini per facilitare il rendering da parte del browser client

Invia un’e-mail a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con domande e commenti.

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
