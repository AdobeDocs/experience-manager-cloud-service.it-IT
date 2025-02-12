---
title: Note sulla versione 2024.9.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2024.9.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 75ecd154-112a-4468-9962-de50bb1f4cd0
source-git-commit: b0208964fc193e0e839bccaaf8245c86f280767d
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 91%

---

# Note sulla versione 2024.9.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione funzionale 2024.9.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2022 o 2023.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Per ricevere una notifica e-mail mensile sugli aggiornamenti delle note sulla versione di Experience Cloud, abbonati ad [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).

## Data di pubblicazione {#release-date}

La data di rilascio della versione corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2024.9.0) è il 26 settembre 2024. La prossima versione funzionale (2024.10.0) è pianificata per il 31 ottobre 2024.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica della versione di settembre 2024 per un riepilogo delle funzioni aggiunte alla versione 2024.9.0:

>[!VIDEO](https://video.tv.adobe.com/v/3434847?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuova funzione in Experience Manager Sites {#new-feature-sites}

#### Gestione della traduzione {#translation-management}

I flussi di lavoro di traduzione AEM e le azioni API ora attivano gli eventi per fornire informazioni approfondite sulle modifiche dello stato del processo di traduzione. Gli utenti possono iscriversi a questi eventi tramite Adobe Developer Console. Per ulteriori informazioni sull’API di gestione della traduzione AEM, consulta [qui](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/translation/).

### Programma per i primi utilizzatori {#sites-early-adopter}

**Generare varianti**

Sfruttare l’intelligenza artificiale generativa tramite la nuova funzione di AEM, [genera varianti](/help/generative-ai/generate-variations.md), ora accessibile in Cloud Service. Genera varianti consente di generare e ridimensionare la creazione di contenuti tramite l’utilizzo dell’intelligenza artificiale generativa. Rivolgiti al tuo team Adobe Account per prendere in considerazione il programma.


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Funzione per l’accesso anticipato in Dynamic Media {#dm-early-access}

**Didascalie video generate dall’intelligenza artificiale**

Le didascalie video generate dall’intelligenza artificiale in Adobe Dynamic Media utilizzano l’intelligenza artificiale per generare automaticamente le didascalie per i contenuti video. Questa funzione è stata progettata per migliorare l’accessibilità e l’esperienza utente fornendo didascalie accurate e in tempo reale. L’intelligenza artificiale analizza la traccia audio del video per trascrivere il discorso e creare didascalie, che possono essere modificate per maggiore precisione o personalizzazione. Queste didascalie soddisfano i requisiti di accessibilità e migliorano il coinvolgimento video per tipi di pubblico che si affidano al supporto video basato su testo o che preferiscono farlo.

Per ottenere l’accesso anticipato al supporto delle didascalie generate dall’intelligenza artificiale sul tuo account Dynamic Media, [crea e invia un caso all’Assistenza clienti Adobe](/help/assets/dynamic-media/video.md##enable-dash).

### Nuove funzioni in Selettore risorse {#asset-selector-new-features}

Il Selettore risorse ora supporta la navigazione nelle raccolte per trovare la risorsa desiderata.
![Raccolte del selettore risorse](/help/assets/assets/collections-rail-modal-view.png)

### Nuove funzioni nell’hub di contenuti {#content-hub-new-features}

Gli amministratori ora possono verificare se rendere visibili le risorse scadute nell’hub di contenuti. Inoltre, se le risorse scadute vengono rese visibili, possono definire se gli utenti potranno scaricarle.

![Risorse scadute nell’hub di contenuti](/help/assets/assets/view-download-expired-assets.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni pre-release in AEM Forms {#forms-new-prerelease-features}

#### Salvataggio automatico di una bozza per moduli adattivi basati su Componenti core

Gli utenti possono ora beneficiare di una funzione di salvataggio automatico che consente di salvare automaticamente come bozza un modulo parzialmente completato. L’utente potrà quindi completare in un secondo momento la compilazione del modulo, anche da un altro dispositivo. Questa funzione migliora i tassi di conversione per le organizzazioni riducendo l’abbandono dei moduli, in quanto gli utenti non devono ricominciare a compilarli dall’inizio.


### Funzionalità per Accesso anticipato ad AEM Forms {#forms-new-early-access-features}

Il programma per l’accesso anticipato ad AEM Forms offre un’opportunità unica per ottenere l’accesso esclusivo a innovazioni all’avanguardia e contribuire a modellarne lo sviluppo.

In queste note sulla versione sono elencate le innovazioni incluse nella versione corrente. Per l’elenco completo delle innovazioni disponibili nell’ambito del programma per l’accesso anticipato, consulta la [documentazione del programma per l’accesso anticipato ad AEM Forms](/help/forms/early-access-ea-features.md).

#### Assistente IA di AEM Forms

L’intelligenza artificiale generativa per moduli adattivi offre un livello completamente nuovo di potenza e semplicità ai processi di sviluppo dei moduli. Ti consente di creare moduli migliori più rapidamente che mai.

![Assistente IA generativa, moduli adattivi](/help/forms/assets/generative-ai-assistant.png)

Le funzionalità di intelligenza artificiale generativa offerte sono:

* **Assistente IA per le query sui prodotti**: ottieni risposte immediate alle domande relative al modulo AEM. L’Assistente IA funge da knowledge base personale, fornendo indicazioni approfondite e consigli direttamente all’interno della piattaforma.

* **Generazione di moduli adattivi**: creazione semplificata di moduli completi con prompt di IA generativa. L’intelligenza artificiale generativa di Adobe genera automaticamente moduli intuitivi che riducono i casi di abbandono e personalizzano l’esperienza.

* **Generazione del pannello per moduli**: genera sezioni del modulo personalizzate in base a esigenze specifiche di raccolta dati. Ad esempio, genera sezioni per la raccolta di informazioni di pagamento, preferenze cliente o dettagli di viaggio.

* **Modifica dei layout del modulo**: prova con layout e progettazioni diversi utilizzando i prompt di IA generativa. Prova diversi layout, ad esempio la procedura guidata o le visualizzazioni a schede, per trovare il layout ideale per il modulo. Utilizza i prompt di intelligenza artificiale generativa per ottimizzare i moduli per la reattività mobile e creare moduli visivamente coinvolgenti che gli utenti apprezzano.

* **Configura azione di invio**: utilizza i prompt di IA generativa per configurare facilmente un’azione di invio per il modulo. Scegli da una libreria di azioni di invio predefinite o personalizzate, create e implementate dal tuo team di sviluppo.

>[!IMPORTANT]
>
> Ti interessa partecipare al programma di accesso anticipato per qualsiasi innovazione sui moduli? Invia un’e-mail dal tuo indirizzo ufficiale a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) con l’elenco delle funzionalità che ti interessano.

## Componente aggiuntivo CIF {#cloud-services-cif}

### Miglioramenti {#improvements-fixes-cif}

* Rendi il limite delle categorie personalizzabile.

### Correzioni di bug {#bug-fixes-cif}

* I campi di Commerce non sono correttamente integrati nell’editor schema metadati di Assets.
* Problema con più campi dei prodotti carosello per il trascinamento.
* Problema con più campi della categoria carosello per il trascinamento.
* Il clic del mouse non funziona per i menu nelle informazioni della pagina nella pagina dell’editor di categorie e prodotti.
* Il numero ordine non è visibile nella pagina di conferma dell&#39;ordine.

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Edge Side Includes (ESI) per il caricamento di contenuti dinamici {#esi}

Adobe Managed CDN ora supporta [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md), un linguaggio di markup per l’assemblaggio di contenuti web dinamici a livello Edge. Includendo snippet ESI, è possibile memorizzare nella cache la pagina HTML generale sulla rete CDN con valori TTL più elevati e recuperare con maggiore frequenza dall’origine le sezioni più piccole che richiedono aggiornamenti più frequenti (TTL più bassi). Questa funzionalità verrà implementata in modo graduale.

### Autenticazione di base alla rete CDN {#basicauth-cdn}

Proteggi alcune risorse di contenuto visualizzando una finestra di dialogo di autenticazione di base che richiede un nome utente e una password. Questa funzione è destinata principalmente a casi d’uso di autenticazione leggera, come la revisione dei contenuti da parte delle parti aziendali interessate, anziché fungere da soluzione completa per i diritti di accesso degli utenti finali. L’elenco di nome utente e password viene gestito in Git tramite un file di configurazione distribuito tramite Pipeline di configurazione, con riferimento a variabili di ambiente Cloud Manager di tipo segreto. [Ulteriori informazioni](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth).

### Reindirizzamenti lato client {#client-side-redirects}

Dichiara [i reindirizzamenti del browser](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors) in un file di configurazione Git distribuiti e valutati nella rete CDN. Questa funzione può essere utile in scenari quali l’eliminazione di pagine, la modifica della struttura del sito e l’ottimizzazione SEO (Search Engine Optimization).

### Nuovo Developer Console di AEM (Beta pubblica) {#aem-developer-console-beta}

Prova una [Developer Console di AEM](/help/implementing/developing/introduction/aem-developer-console.md) rinnovata, che offre un’esperienza più interattiva per il debug del codice in ambienti cloud.

Chiunque può accedere alla versione Beta pubblica facendo clic sul pulsante *Nuova console disponibile* nella Developer Console di AEM corrente. Adobe accoglie con favore qualsiasi feedback che è possibile inviare via e-mail all’indirizzo **<aemcs-new-devconsole-ui-beta@adobe.com>**.

![Schermata dei bundle OSGi nella Developer Console di AEM](/help/implementing/developing/introduction/assets/osgi-bundles.png)

### Gli utenti aziendali possono dichiarare i reindirizzamenti al di fuori di Git (programma per i primi utilizzatori) {#apache-rewritemaps-early-adopter}

In modo simile ad AEM 6.5, Apache/dispatcher acquisisce le mappe di riscrittura che si trovano in una posizione specifica nell’archivio di pubblicazione e le carica, senza richiedere l’esecuzione di una pipeline a livello web. Questo approccio consente agli utenti aziendali di specificare reindirizzamenti utilizzando un foglio di calcolo o un’interfaccia utente, come ACS Commons Redirect Map Manager o un’applicazione personalizzata. Partecipa al programma per i primi utilizzatori inviando un’e-mail a **<aemcs-cdn-config-adopter@adobe.com>**.

### Pipeline di configurazione per gli RDE (Programma per i primi utilizzatori) {#config-pipeline-rdes-early-adopter}

La [pipeline di configurazione](/help/operations/config-pipeline.md) viene utilizzata per distribuire le configurazioni dei file yaml, incluse le opzioni CDN (regole del filtro del traffico, trasformazioni di richiesta/risposta e così via). Partecipa al programma per i primi utilizzatori inviando un’e-mail a **<aemcs-cdn-config-adopter@adobe.com>** per distribuire queste configurazioni anche negli RDE (Rapid Development Environments) che utilizzano una CLI.

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
