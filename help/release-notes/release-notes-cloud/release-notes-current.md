---
title: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 11d019e10dc9246e5560f7fe27472d047cdc7caa
workflow-type: tm+mt
source-wordcount: '1551'
ht-degree: 48%

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

La data di rilascio della versione corrente della funzione di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2025.4.0) è il venerdì 24 aprile 2025. La prossima versione funzionale (2025.5.0) è pianificata per il venerdì 29 maggio 2025.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the February 2025 Release Overview video for a summary of the features added in the 2025.2.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni di Experience Manager Sites {#enhancements-sites}

**Interfaccia utente di amministrazione nuovo modello per frammenti di contenuto**

A completamento dell’elenco delle nuove interfacce utente lato client quando si lavora con Frammenti di contenuto di AEM, è ora disponibile una nuova interfaccia utente amministratore per i modelli di frammenti di contenuto. La nuova interfaccia utente fornisce una vista elenco moderna e pulita che consente di cercare modelli con filtri e che mostra i tag dei modelli e quali frammenti di contenuto esistono basati su un determinato modello. La documentazione è disponibile [qui](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md).

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media (Scene7) {#dynamic-media-scene7}

**Dynamic Media (Scene7) non supportato negli ambienti di sicurezza avanzata**

Dynamic Media (Scene7) su AEM as a Cloud Service non è compatibile con HIPAA e non può essere utilizzato in ambienti AEM in cui è abilitata la sicurezza avanzata.

A partire dalla versione di aprile 2025 di AEM as a Cloud Service, una restrizione tecnica impedisce la configurazione di Dynamic Media (Scene7) in ambienti con sicurezza avanzata. Di conseguenza, la scheda **Configurazione elemento multimediale dinamico** in **Strumenti** > **Servizi cloud** non è più visibile in questi ambienti.

Inoltre, i clienti che utilizzano AEM 6.5 devono essere consapevoli che lo stack Dynamic Media (Scene7) non è compatibile con HIPAA.

### Dynamic Media Classic {#dynamic-media-classic}

**Reporting**

La scheda Larghezza di banda nella dashboard di reporting di Dynamic Media Classic non è più supportata da aprile 2025.

Consulta [Larghezza di banda e archiviazione, tipi di rapporti](https://experienceleague.adobe.com/it/docs/dynamic-media-classic/using/setup/administration-setup#types-of-reports).


## Nuove funzioni nella vista Assets {#new-features-assets-view}

**Relazioni risorsa**

La vista risorse ora supporta la visualizzazione e la modifica delle relazioni tra risorse in un pannello semplificato Dettagli risorsa. Aggiungi facilmente relazioni come Source e Derivate ai contenuti in modo che gli utenti possano trovare in modo più efficace i contenuti principali rilevanti.

![Esempio di relazione Assets](/help/assets/assets/asset-relations-example.png)

**Confronta versioni di una risorsa**

Ora puoi selezionare e confrontare rapidamente qualsiasi versione di una risorsa con la sua versione più recente utilizzando la vista Assets.

![confronta le versioni della risorsa](/help/assets/assets/version-compare2.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Funzioni pre-release

* [Editor universale - Frammenti di modulo](/help/edge/docs/forms/universal-editor/creating-form-fragments.md): l&#39;editor universale ora consente di creare e riutilizzare frammenti di modulo per Forms adattivo. Questi frammenti sono sezioni di moduli riutilizzabili (ad esempio, dettagli di contatto, campi di consenso) che possono essere create una volta e applicate a più moduli. Questa funzione semplifica la creazione dei moduli, garantisce la coerenza e migliora l’efficienza nell’authoring.

* [Raccolta documenti di SharePoint - Salva allegati con nomi di file originali](/help/forms/connect-forms-to-sharepoint-document-library.md#connect-an-adaptive-form-to-microsoft-sharepoint-document-library): è ora possibile salvare gli allegati del modulo utilizzando i nomi di file originali quando vengono memorizzati in una raccolta documenti di SharePoint. Questo miglioramento semplifica l’identificazione e la gestione dei file caricati.

* **Editor regole**:
   * [Condizione binaria con evento di clic nella clausola &quot;When&quot;](/help/forms/rule-editor-core-components-events-operators.md#available-operator-types-and-events-in-rule-editor): l&#39;editor di regole consente ora di combinare un evento di clic su pulsante (_Is Clicked_) con altre condizioni all&#39;interno della clausola &quot;When&quot;. Questo consente un controllo più preciso sull’esecuzione delle regole in base all’interazione dell’utente e ad altri fattori. Nota: quando si utilizzano più condizioni, l’evento clic deve essere la prima condizione elencata.
   * [Condizioni di convalida per campi e pannelli](/help/forms/rule-editor-core-components-usecases.md): l&#39;editor di regole ora include _IsValid_ e _IsNotValid_ condizioni. Consente di controllare lo stato di convalida di campi specifici o interi pannelli (inclusi layout come Schede orizzontali, Schede verticali, Pannello a soffietto e Creazioni guidate), semplificando la navigazione dei moduli e migliorando l’esperienza utente in base ai risultati della convalida.
* **È stata migliorata la gestione dell&#39;ambito per gli elenchi SharePoint**: i siti SharePoint ora supportano tutti i percorsi gestiti, ad esempio /sites e /teams. Questo miglioramento consente un’integrazione più ampia tra diverse strutture del sito SharePoint, offrendo maggiore flessibilità nella connessione ai contenuti organizzativi.
* **Supporto per il salvataggio del documento di record nell&#39;elenco SharePoint**: Forms creato utilizzando un modello dati modulo basato su elenco di SharePoint (FDM) può ora salvare il documento di record (DoR) negli elenchi di SharePoint configurando la proprietà del campo Riferimento associazione documento di record. Questo miglioramento consente l’integrazione diretta dei dati e dei documenti dei moduli supportati con lo storage SharePoint.

### Funzioni di accesso anticipato in AEM Forms {#forms-new-early-access-features}

Il programma per l’accesso anticipato ad AEM Forms offre un’opportunità unica per ottenere l’accesso esclusivo a innovazioni all’avanguardia e contribuire a modellarne lo sviluppo.

In queste note sulla versione sono elencate le innovazioni incluse nella versione corrente. Per l’elenco completo delle innovazioni disponibili nell’ambito del programma per l’accesso anticipato, consulta la [documentazione del programma per l’accesso anticipato ad AEM Forms](/help/forms/early-access-ea-features.md).

#### Integrazione di Adobe Experience Platform (AEP) con Forms

Le funzionalità di integrazione tra Forms e AEP sono ora disponibili per i primi utenti.

## Componente aggiuntivo CIF {#cloud-services-cif}

### Miglioramenti {#enhancements-cif}

* Aggiunta della selezione della variante di prodotto per il tipo di dati di riferimento prodotto CIF
* [Sperimentale]: JSON+LD nei componenti core CIF nei PDP
* [Sperimentale]: possibilità di CIF di cancellare la cache

### Correzioni di bug {#bug-fixes-cif}

* Correggi il problema di ricerca nel campo del prodotto
* Il formato dell’URL del prodotto non funziona come previsto per la #variant_sku
* Impossibile aggiungere più di 20 SKU al componente Elenco prodotti

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### API basate su OpenAPI {#open-apis}

Gli sviluppatori possono integrare in modo approfondito le funzionalità di AEM as a Cloud Service nelle proprie applicazioni e strumenti. Le nuove API di AEM as a Cloud Service seguono le specifiche OpenAPI, con l’obiettivo di essere coerenti, ben documentate e di facile utilizzo. Le credenziali per gli endpoint che richiedono l’autenticazione vengono generate creando progetti Adobe Developer Console e supportano server-to-server, app web e app a pagina singola OAuth.

[Visualizza l&#39;elenco completo](https://developer.adobe.com/experience-cloud/experience-manager-apis/#openapi-based-apis) delle API basate su OpenAPI, [Ulteriori informazioni](/help/implementing/developing/open-api-based-apis.md) e prova un [tutorial end-to-end](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/aem-apis/openapis/invoke-api-using-oauth-s2s) che illustra la configurazione e l&#39;utilizzo.

Guarda questo video per scoprire come configurare un’API autenticata per un utilizzo successivo:

>[!VIDEO](https://video.tv.adobe.com/v/3457510?quality=12&learn=on)

### Miglioramenti relativi alla configurazione CDN {#cdn-enhancements}

La rete CDN gestita da Adobe offre opzioni di configurazione flessibili, come descritto nell&#39;articolo [Pipeline di configurazione](/help/operations/config-pipeline.md#configurations). Di seguito sono riportate alcune funzioni recenti:

#### Includi proprietà aggiuntive nei registri CDN {#props-in-cdnlogs}

Utile per scenari quali il debug e l&#39;analisi dei dati, è possibile includere ulteriori informazioni nei registri CDN oltre alle proprietà predefinite impostando l&#39;azione `logProperty` in [trasformazioni di richiesta e risposta](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations).

#### Proprietà dell&#39;area geografica, del continente e dell&#39;organizzazione come condizioni corrispondenti {#matching-conditions}

Le regole CDN ora possono corrispondere in base all’area geografica, al continente e all’organizzazione per i casi d’uso, tra cui il blocco del traffico e i reindirizzamenti. `clientRegion` e `clientContinent` incrementano il già supportato `clientCountry` in base alla posizione geografica, mentre `clientAsName` e `clientAsNumber` corrispondono ai sistemi autonomi per identificare ISP, aziende o provider cloud di grandi dimensioni. Ulteriori informazioni su queste [proprietà di richiesta appena esposte](/help/security/traffic-filter-rules-including-waf.md#condition-structure).

#### Imposta valore cookie {#cookie-attributes}

È possibile impostare gli attributi dei cookie in [trasformazioni di risposta](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations).

### Supporto Java 21 {#java21}

A partire dalla versione di gennaio, è possibile generare codice con Java 21 e Java 17. È possibile accedere a nuove funzioni quali corrispondenza pattern, classi sigillate e vari miglioramenti delle prestazioni. Per i passaggi di configurazione, incluso l’aggiornamento delle versioni del progetto Maven e della libreria, consulta l’articolo [Ambiente di build](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support).

Il **runtime** Java 21, con prestazioni più elevate, verrà distribuito automaticamente quando viene rilevata una build Java 17 o 21. Tuttavia, è anche consigliabile optare per il runtime Java 21 per gli ambienti creati con Java 11, inviando un’e-mail a [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com). Informazioni sui [requisiti del runtime Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).

>[!IMPORTANT]
>
> Il **runtime** Java 21 è stato distribuito negli ambienti di sviluppo/RDE a febbraio; verrà applicato agli ambienti di staging/produzione il **28 e 29 aprile**. Tieni presente che **la generazione del codice** con Java 21 (o Java 17) è indipendente dal runtime di Java 21. È necessario eseguire in modo esplicito i passaggi per generare il codice con Java 21 (o Java 17).

### Inoltro dei registri di AEM a più destinazioni - Programma Beta {#log-forwarding-earlyadopter}

Ora, in versione Beta, è possibile inoltrare i registri di AEM a New Relic (utilizzando HTTPS), Amazon S3 e Sumo Logic. Sono supportati i registri di AEM (incluso Apache/Dispatcher), ma non i registri CDN. Invia un’e-mail a [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) per accedere.

Anche se i registri di AEM possono essere scaricati da Cloud Manager, molte organizzazioni trovano utile inviare in streaming tali registri a una destinazione di registrazione preferita. AEM supporta già l’inoltro dei registri CDN e AEM (disponibilità generale) all’archiviazione BLOB di Azure, Datadog, HTTPS, Elasticsearch (e OpenSearch) e Splunk. Questa funzione è configurata in modo autonomo e distribuita mediante la pipeline di configurazione.

Ulteriori informazioni sono disponibili nella [documentazione sull’inoltro dei registri](/help/implementing/developing/introduction/log-forwarding.md).

### Edge Computing - Richiesta di feedback! {#edge-computing-feedback}

L’Edge computing avvicina l’elaborazione dei dati al browser, il che offre vantaggi quali una latenza ridotta. Adobe desidera ricevere commenti sull’utilità di questa tecnologia per i progetti Pubblica cosegna AEM e Edge Delivery Services. Inoltre, il modo in cui pensi di utilizzarla per contribuire alla roadmap.

Alcuni possibili casi d’uso:

* Autenticazione con un IdP per ottenere l’accesso al contenuto
* Personalization eseguendo il rendering del contenuto dinamico in base alla geolocalizzazione, al tipo di dispositivo, agli attributi utente e così via.
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
