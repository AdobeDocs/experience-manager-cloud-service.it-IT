---
title: Note sulla versione 2024.7.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2024.7.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 6194df9d-8c3c-4c7f-be59-099b970a565a
source-git-commit: 47b6d7871201cd7dbc1db77620879e69bce4ad3a
workflow-type: tm+mt
source-wordcount: '1626'
ht-degree: 82%

---

# Note sulla versione 2024.7.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione funzionale 2024.7.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2022 o 2023.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Per ricevere una notifica e-mail mensile sugli aggiornamenti delle note sulla versione di Experience Cloud, abbonati ad [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).

## Data di pubblicazione {#release-date}

La data di rilascio della versione funzionale corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2024.7.0) è il 25 luglio 2024. La successiva versione funzionale (2024.8.0) è pianificata per il 29 agosto 2024.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica sulla versione di luglio 2024 per un riepilogo delle funzioni aggiunte alla versione 2024.7.0:

>[!VIDEO](https://video.tv.adobe.com/v/3431707?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuova funzione in Experience Manager Sites {#new-feature-sites}

### Programma per i primi utilizzatori {#sites-early-adopter}

**Generare varianti**

Sfruttare l’intelligenza artificiale generativa tramite la nuova funzione di AEM, [genera varianti](/help/generative-ai/generate-variations.md), ora accessibile in Cloud Service. Genera varianti consente di generare e ridimensionare la creazione di contenuti tramite l’utilizzo dell’intelligenza artificiale generativa. Rivolgiti al tuo team Adobe Account per prendere in considerazione il programma.

**Esplorazione delle risorse nella console Frammenti di contenuto**

Gli autori dei contenuti ora possono esplorare, visualizzare e intervenire sulle immagini e su altre risorse senza dover uscire dalla console Frammenti di contenuto.

![Esplorazione delle risorse](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

Ti interessa provare questa funzione e condividere con noi un tuo feedback? Per ulteriori informazioni sul programma per i primi utilizzatori, invia un’e-mail all’indirizzo aemcs-headless-adopter@adobe.com dal tuo ID e-mail ufficiale.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Caricare risorse tramite il Selettore risorse**

Asset Selector now offers the ability for content authors to upload final assets directly from the selector, by either dragging or by browsing from the local file system. This functionality allows final assets to be uploaded to the DAM from the application of your choice.

### Funzione per l’accesso anticipato in Dynamic Media {#dm-early-access}

**Didascalie video generate dall’intelligenza artificiale**

Le didascalie video generate dall’intelligenza artificiale in Adobe Dynamic Media utilizzano l’intelligenza artificiale per generare automaticamente le didascalie per i contenuti video. Questa funzione è stata progettata per migliorare l’accessibilità e l’esperienza utente fornendo didascalie accurate e in tempo reale. L’intelligenza artificiale analizza la traccia audio del video per trascrivere il discorso e creare didascalie, che possono essere modificate per maggiore precisione o personalizzazione. Queste didascalie soddisfano i requisiti di accessibilità e migliorano il coinvolgimento video per tipi di pubblico che si affidano al supporto video basato su testo o che preferiscono farlo.

Per ottenere l’accesso anticipato al supporto delle didascalie generate dall’intelligenza artificiale sul tuo account Dynamic Media, [crea e invia un caso all’Assistenza clienti Adobe](/help/assets/dynamic-media/video.md##enable-dash).

### Nuove funzioni nella vista Risorse {#assets-view-new-features}

**Integrazione di dati Content Credentials**

Experience Manager Assets ora supporta i dati Content Credentials per i formati di immagine supportati. This ability provides information on the lineage of the asset and how it was created, including if it was modified using GenAI.

![Content Credentials](/help/assets/assets/content-credentials.png)

**Anteprime visive del contenuto delle cartelle**

Experience Manager Assets now displays visual previews of folder contents on the folder thumbnail when browsing or searching for content, which improves the discoverability of assets available within the AEM Assets repository.

<!--


**Content Credentials**

Content Credentials feature in Assets view now provides detailed asset provenance data adhered to an asset. This helps to trace the enroute edits along the asset's lifecycle to prevent users from deception through deliberately tempered assets. This ensures content authenticity among users and fosters trust through transparency.

When looking at the asset details, any image with content credentials added, such as those created with GenAI, displays the manifest details in a dedicated panel. If the asset is downloaded, published, or shared, the credentials remain intact with the asset.

![check publish status1](/help/release-notes/assets/content-credentials.png)

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni in AEM Forms {#forms-new-prerelease-features}

#### Editor di regole visivo ottimizzato per moduli adattivi basati su componenti core

Adaptive form authors can use repeatable form fields and out-of-the-box visual rule editor functions to create complex business logic in forms without needing customization or support from the development team.

### Funzionalità per Accesso anticipato ad AEM Forms {#forms-new-early-access-features}

Il programma di accesso anticipato per AEM Forms offre un’opportunità unica per ottenere l’accesso esclusivo a innovazioni all’avanguardia prima di chiunque altro e contribuire a definirne lo sviluppo. Il programma offre l’accesso a molteplici innovazioni.

In queste note sulla versione sono elencate le innovazioni incluse nella versione corrente. Per l’elenco completo delle innovazioni disponibili nell’ambito del programma per l’accesso anticipato, consulta la [documentazione del programma per l’accesso anticipato ad AEM Forms](/help/forms/early-access-ea-features.md).

#### Creare moduli adattivi utilizzando l’editor universale

Con l’[editor universale](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction) di Adobe Experience Manager puoi creare moduli adattivi in modalità WYSIWYG e mediante il semplice trascinamento degli elementi, per l’authoring di esperienze di registrazione headless e headful, distribuite tramite Edge Delivery Services. Adaptive form authors can easily create and launch experiments for variations of the forms in the web pages. This ability lets them determine the best performing experiences for end users.

>[!IMPORTANT]
>
> Se ti interessa partecipare al programma di accesso anticipato di Adobe per qualsiasi innovazione, invia un’e-mail dal tuo indirizzo ufficiale a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com). Puoi richiedere l’accesso a tutte le innovazioni o solo a qualcuna.

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Eliminare i contenuti dalla rete CDN con una chiave API self-service {#purge-cdn}

Impostando il valore TTL (Time to Live) mediante l’intestazione HTTP cache-control è possibile bilanciare in modo efficace le prestazioni di distribuzione dei contenuti e lo stato di aggiornamento degli stessi. However, in scenarios where it is critical to serve updated content immediately, it may be beneficial to purge the CDN cache directly.

[Learn how](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token) to self-serve the configuration of a purge API token using the Cloud Manager configuration pipeline, so you can [invoke the purge APIs](/help/implementing/dispatcher/cdn-cache-purge.md), with any of these variations:

* URL singolo
* Più URL con un tag
* Eliminazione completa della cache CDN

### Configurazione self-service di X-AEM-Edge-Key per CDN gestita dal cliente {#customermanaged-keys}

In precedenza, era necessario un ticket di supporto per generare la chiave X-AEM-Edge-Key necessaria per la configurazione di una rete CDN gestita dalla clientela. This workflow is now self-service by declaring the key value in a configuration file that is deployed using the Configuration Pipeline, removing any delay in onboarding a new environment. [Ulteriori informazioni](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value).

### Avvisi delle regole di filtro del traffico {#traffic-filter-rules-alerts}

Traffic filter rules, which include the optionally licensable Web Application Firewall (WAF) rules, lets you configure what traffic should be blocked.

Now, you can [subscribe to alerts](/help/security/traffic-filter-rules-including-waf.md#traffic-filter-rules-alerts) whenever your traffic filter rules are triggered. Le notifiche e-mail del Centro azioni ti informeranno quando si verificano determinate condizioni di traffico, in modo che tu possa adottare le misure appropriate.

### Programmi per i primi utilizzatori relativi alla distribuzione dei contenuti {#foundation-early-adopter}

Invia un’e-mail all’indirizzo **<aemcs-cdn-config-adopter@adobe.com>**, indicando quali dei programmi per i primi utilizzatori seguenti ti interessa.

#### Autenticazione di base alla rete CDN (Programma per i primi utilizzatori) {#basicauth-cdn}

Proteggi alcune risorse di contenuto visualizzando una finestra di dialogo di autenticazione di base che richiede un nome utente e una password. Questa funzione è destinata principalmente a casi d’uso di autenticazione leggera, come la revisione dei contenuti da parte delle parti aziendali interessate, anziché fungere da soluzione completa per i diritti di accesso degli utenti finali. L’elenco di nome utente e password in gestito tramite un file di configurazione in Git distribuito tramite la pipeline di configurazione, con riferimento alle variabili di ambiente Cloud Manager di tipo segreto. [Ulteriori informazioni](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth).

#### Server-Side Redirects (Early Adopter Program) {#server-side-redirects-early-adopter}

Configure 301/302 server-side redirects in source control, and deploy to the CDN. [Ulteriori informazioni](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors).<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> Attenzione: sono già disponibili diverse altre funzioni correlate a [Configurazione CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md), comprese le trasformazioni di richiesta e risposta e il routing del traffico verso siti esterni ad AEM.

#### Gli utenti aziendali possono dichiarare i reindirizzamenti al di fuori di Git (programma per i primi utilizzatori) {#apache-rewritemaps-early-adopter}

In modo simile ad AEM 6.5, Apache/dispatcher acquisisce le mappe di riscrittura che si trovano in una posizione specifica nell’archivio di pubblicazione e le carica, senza richiedere l’esecuzione di una pipeline a livello web. Questo approccio consente agli utenti aziendali di dichiarare i reindirizzamenti utilizzando un foglio di calcolo o un’interfaccia utente, come ACS Commons Redirect Map Manager o un’applicazione personalizzata. <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### Edge Side Includes (ESI) per il caricamento di contenuti dinamici (programma per i primi utilizzatori) {#esi-early-adopter}

Adobe Managed CDN ora supporta [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md), un linguaggio di markup per l’assemblaggio di contenuti web dinamici a livello di edge. Includendo snippet ESI, è possibile memorizzare nella cache la pagina HTML generale sulla rete CDN con valori TTL più elevati e recuperare con maggiore frequenza dall’origine le sezioni più piccole che richiedono aggiornamenti più frequenti (TTL più bassi). <!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

### Programma per i primi utilizzatori per le notifiche del centro per le azioni relative all’integrità dei contenuti {#actions-center-notifications}

Il [Centro azioni](/help/operations/actions-center.md) invia notifiche e-mail quando si verificano problemi importanti, o se viene notato qualcosa in merito al codice o alla configurazione in cui dovresti intervenire in modo proattivo. Adobe ha ora introdotto diversi nuovi tipi di notifiche associate all’integrità dei contenuti. Questa funzione è disponibile tramite un programma per i primi utilizzatori. Per partecipare, contatta l’Assistenza clienti Adobe.

#### Le pagine contengono un numero elevato di nodi {#page-nodes}

Un numero elevato di nodi può ridurre le prestazioni di rendering e i tempi di caricamento delle pagine. Ricevi una notifica proattiva tramite il Centro azioni quando viene rilevato un numero elevato di nodi in una pagina, consentendo di adottare le misure necessarie per ridurre il numero totale di nodi all’interno di una pagina.

#### Numero elevato di istanze di flusso di lavoro in esecuzione {#running-workflows}

Le prestazioni del motore del flusso di lavoro sono interessate quando nell’ambiente di authoring è presente un numero elevato di flussi di lavoro in esecuzione. Ricevi una notifica proattiva tramite il Centro azioni quando viene rilevato un numero elevato di istanze di flusso di lavoro in esecuzione. Questo processo consente di configurare un processo di eliminazione per interrompere flussi di lavoro in esecuzione non necessari.

#### Utenti aggiunti direttamente ai gruppi personalizzati {#users-customgroups}

Ricevi una notifica proattiva tramite il Centro azioni quando gli utenti vengono aggiunti direttamente ai gruppi personalizzati. Questo processo consente di seguire le best practice IMS aggiungendo utenti ai gruppi IMS rilevanti e includendo quindi tali gruppi IMS come membri dei gruppi AEM.

#### Contenuto JCR mancante {#jcr-content}

Il Centro azioni invia una notifica proattiva quando viene rilevato un contenuto JCR mancante. Questo approccio consente di aggiungere i contenuti mancanti e di evitare l’errore di alcune funzioni di AEM Assets.

#### Flussi di lavoro completati non eliminati {#workflows}

Il Centro azioni notifica in modo proattivo quando i flussi di lavoro completati oltre i 90 giorni non sono stati eliminati. Questo approccio consente di migliorare le prestazioni del motore del flusso di lavoro riducendo il numero di istanze del flusso di lavoro.

#### Risorsa Sling mancante {#sling-resource}

Il Centro azioni invia una notifica proattiva quando viene rilevata una risorsa Sling mancante. Questo approccio consente di aggiungere la risorsa mancante e di evitare l’errore di alcune funzioni di AEM Assets.

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
