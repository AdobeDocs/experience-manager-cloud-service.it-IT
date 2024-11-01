---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione corrente per  [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: d98aa9d206486022d465ca19c8888088562d56c3
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 63%

---

# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note specifiche sulla versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2022 o 2023.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Per ricevere una notifica e-mail mensile sugli aggiornamenti delle note sulla versione di Experience Cloud, abbonati ad [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).

## Data di pubblicazione {#release-date}

La data di rilascio della versione funzionale corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2024.10.0) è il venerdì 31 ottobre 2024. La prossima versione funzionale (2024.11.0) è pianificata per il venerdì 21 novembre 2024.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

<!-- ## Release Video {#release-video}

Have a look at the October 2024 Release Overview video for a summary of the features added in the 2024.10.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3434847?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**Eventi pagina modernizzati**

I seguenti eventi pagina di AEM Sites sono ora disponibili come eventi fruibili esternamente basati su AEM as a Cloud Service Eventing Platform. Gli eventi possono essere elaborati tramite Adobe I/O per interagire con i processi esterni.
* Pagina pubblicata
* Pagina di cui è stata annullata la pubblicazione
* Pagina eliminata

### Programma per i primi utilizzatori {#sites-early-adopter}

**Generare varianti**

Sfruttare l’intelligenza artificiale generativa tramite la nuova funzione di AEM, [genera varianti](/help/generative-ai/generate-variations.md), ora accessibile in Cloud Service. Genera varianti consente di generare e ridimensionare la creazione di contenuti tramite l’utilizzo dell’intelligenza artificiale generativa. Rivolgiti al tuo team Adobe Account per prendere in considerazione il programma.

**REST OpenAPI per AEM per la distribuzione dei frammenti di contenuto**

L&#39;API REST [AEM per la distribuzione dei frammenti di contenuto](/help/headless/aem-rest-openapi-content-fragment-delivery.md) è ora disponibile per AEM as a Cloud Service.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Funzione per l’accesso anticipato in Dynamic Media {#dm-early-access}

**Didascalie video generate dall’intelligenza artificiale**

Le didascalie video generate dall’intelligenza artificiale in Adobe Dynamic Media utilizzano l’intelligenza artificiale per generare automaticamente le didascalie per i contenuti video. Questa funzione è stata progettata per migliorare l’accessibilità e l’esperienza utente fornendo didascalie accurate e in tempo reale. L’intelligenza artificiale analizza la traccia audio del video per trascrivere il discorso e creare didascalie, che possono essere modificate per maggiore precisione o personalizzazione. Queste didascalie soddisfano i requisiti di accessibilità e migliorano il coinvolgimento video per tipi di pubblico che si affidano al supporto video basato su testo o che preferiscono farlo.

Per ottenere l’accesso anticipato al supporto delle didascalie generate dall’intelligenza artificiale sul tuo account Dynamic Media, [crea e invia un caso all’Assistenza clienti Adobe](/help/assets/dynamic-media/video.md##enable-dash).

### Nuove funzioni nella vista Risorse {#assets-view-new-features}

**Report pianificati**

Ora è possibile generare automaticamente i rapporti nella vista Assets in base a una pianificazione ricorrente o in una data futura, riducendo gli sforzi per individuare informazioni basate sui dati.

![Report pianificati-](/help/assets/assets/scheduled-reports-tab.png)

### Nuove funzioni nell’hub di contenuti {#content-hub-new-features}

**Digital Rights Management per risorse con licenza**

Le organizzazioni possono ora aumentare la conformità alle licenze e ridurre al minimo il rischio di condividere le risorse con le condizioni di licenza sfruttando DRM per le risorse concesse in licenza agli utenti di Content Hub, che devono rivedere e accettare le condizioni di licenza prima di iniziare a scaricare le risorse concesse in licenza.

![download-multiple-license](/help/assets/assets/download-multiple-license.png)

**Configurazione metadati scheda risorse**

Content Hub ora consente di configurare fino a un massimo di 6 campi di metadati chiave da visualizzare nella scheda delle risorse.

![metadati chiave nella scheda risorse](/help/assets/assets/asset-card-key-metadata.png)

**Configurare la visibilità e il download delle risorse scadute**

Gli amministratori ora possono verificare se rendere visibili le risorse scadute nell’hub di contenuti. Inoltre, se le risorse scadute vengono rese visibili, possono definire se gli utenti potranno scaricarle.

![Risorse scadute nell’hub di contenuti](/help/assets/assets/expired-assets-content-hub.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni pre-release in AEM Forms {#forms-new-prerelease-features}

#### Salvataggio automatico di una bozza per moduli adattivi basati su Componenti core

Gli utenti possono ora beneficiare di una funzione di salvataggio automatico che consente di salvare automaticamente come bozza un modulo parzialmente completato. Potranno tornare in un secondo momento per completarne la compilazione sullo stesso dispositivo o su un altro. Questa funzione migliora i tassi di conversione per le organizzazioni riducendo l’abbandono dei moduli, in quanto gli utenti non devono ricominciare a compilarli dall’inizio.

### Funzionalità per Accesso anticipato ad AEM Forms {#forms-new-early-access-features}

Il programma per l’accesso anticipato ad AEM Forms offre un’opportunità unica per ottenere l’accesso esclusivo a innovazioni all’avanguardia e contribuire a modellarne lo sviluppo.

In queste note sulla versione sono elencate le innovazioni incluse nella versione corrente. Per l’elenco completo delle innovazioni disponibili nell’ambito del programma per l’accesso anticipato, consulta la [documentazione del programma per l’accesso anticipato ad AEM Forms](/help/forms/early-access-ea-features.md).

#### Assistente IA di AEM Forms

L’intelligenza artificiale generativa per moduli adattivi offre un livello completamente nuovo di potenza e semplicità ai processi di sviluppo dei moduli. Ti consente di creare moduli migliori più rapidamente che mai.

![Assistente IA generativa, moduli adattivi](/help/forms/assets/generative-ai-assistant.png)

Le funzionalità di intelligenza artificiale generativa offerte sono:

* **Assistente IA per le query sui prodotti**: ottieni risposte immediate alle domande relative al modulo AEM. L’assistente di IA funge da knowledge base personale, fornendo indicazioni approfondite e consigli direttamente all’interno della piattaforma.

* **Generazione di moduli adattivi**: creazione semplificata di moduli completi con prompt di IA generativa. L’intelligenza artificiale generativa di Adobe genera automaticamente moduli intuitivi che riducono i casi di abbandono e personalizzano l’esperienza.

* **Generazione del pannello per moduli**: genera sezioni del modulo personalizzate in base a esigenze specifiche di raccolta dati. Ad esempio, genera sezioni per la raccolta di informazioni di pagamento, preferenze cliente o dettagli di viaggio.

* **Modifica dei layout del modulo**: prova con layout e progettazioni diversi utilizzando i prompt di IA generativa. Prova diversi layout, ad esempio la procedura guidata o le visualizzazioni a schede, per trovare il layout ideale per il modulo. Utilizza i prompt di intelligenza artificiale generativa per ottimizzare i moduli per la reattività mobile e creare moduli visivamente coinvolgenti che gli utenti apprezzano.

* **Configura azione di invio**: utilizza i prompt di IA generativa per configurare facilmente un’azione di invio per il modulo. Scegli da una libreria di azioni di invio predefinite o personalizzate, create e implementate dal tuo team di sviluppo.

>[!IMPORTANT]
>
> Ti interessa partecipare al programma di accesso anticipato per qualsiasi innovazione sui moduli? Invia un’e-mail dal tuo indirizzo ufficiale a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) con l’elenco delle funzionalità che ti interessano.

## Componente aggiuntivo CIF {#cloud-services-cif}

### Correzioni di bug {#bug-fixes-cif}

* Sono stati corretti i test dell’interfaccia utente per il corretto funzionamento con i componenti core CIF.
* È stato risolto un problema a causa del quale il formato dell’URL della categoria non funzionava come previsto nell’istanza cloud.

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Inoltro dei registri self-service con opzione di rete avanzata {#log-forwarding}

Mentre i registri AEM (incluso Apache/Dispatcher) e CDN possono essere scaricati da Cloud Manager, molte organizzazioni trovano utile inviare in streaming tali registri a una destinazione di registrazione preferita. AEM ora supporta [l&#39;inoltro del registro](/help/implementing/developing/introduction/log-forwarding.md) ad Azure Blob Storage, Datadog, HTTPS, Elasticsearch (e OpenSearch) e Splunk. I registri AEM possono essere facoltativamente inoltrati tramite configurazioni di rete avanzate, ad esempio utilizzando un indirizzo IP dedicato.

Questa funzionalità è configurata dagli utenti in modo autonomo e distribuita utilizzando la [pipeline di configurazione](/help/operations/config-pipeline.md).

### Reindirizzamenti URL senza pipeline per utenti aziendali {#pipeline-free-redirects}

I reindirizzamenti lato browser sono utili quando una pagina web viene rimossa o spostata o in altri scenari. Con [Reindirizzamenti URL senza pipeline](/help/implementing/dispatcher/pipeline-free-url-redirects.md), è possibile inserire un file di mappa di riscrittura Apache in un percorso di pubblicazione AEM, dove viene caricato automaticamente, senza dover eseguire il commit del file nel controllo del codice sorgente o avviare una pipeline Cloud Manager.

Le opzioni per la pubblicazione del file di riscrittura includono il caricamento come risorsa, l’utilizzo di ACS Commons Rewrite Map Manager o l’interazione con un’interfaccia utente personalizzata.

### Pipeline di configurazione per RDE {#config-pipeline-rdes}

Gli ambienti di sviluppo rapido sono uno strumento potente per distribuire e testare rapidamente il codice e la configurazione in un ambiente Cloud. Gli RDE ora supportano [la sincronizzazione dei file YAML di configurazione](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline), incluse le impostazioni CDN quali le regole del filtro del traffico e le trasformazioni di richieste/risposte, nonché l&#39;inoltro del registro e altre opzioni di configurazione. [Per ulteriori dettagli, vedere l&#39;elenco completo](/help/operations/config-pipeline.md) delle opzioni di configurazione supportate.

### Nuovi profili di prodotto {#new-product-profiles}

Quando viene creato un nuovo ambiente AEM, i profili di prodotto vengono visualizzati automaticamente in Adobe Admin Console, consentendo agli amministratori di assegnare l’accesso alle soluzioni e alle funzionalità concesse in licenza.

I nuovi ambienti includono ora un set aggiornato di profili di prodotto, che li rendono compatibili con le funzioni future, inclusa la generazione di credenziali API in Adobe Developer Console. Gli ambienti esistenti saranno in grado di aggiornare i loro profili di prodotto in una versione futura. [Ulteriori informazioni](/help/onboarding/aem-cs-team-product-profiles.md).

### Nuovo Developer Console di AEM (Beta pubblica) {#aem-developer-console-beta}

Prova una [Developer Console di AEM](/help/implementing/developing/introduction/aem-developer-console.md) rinnovata, che offre un’esperienza più interattiva per il debug del codice in ambienti cloud.

Chiunque può accedere alla versione Beta pubblica facendo clic sul pulsante *Nuova console disponibile* nella Developer Console di AEM corrente. Adobe accoglie con favore qualsiasi feedback che è possibile inviare via e-mail all’indirizzo **<aemcs-new-devconsole-ui-beta@adobe.com>**.

![Schermata dei bundle OSGi nella Developer Console di AEM](/help/implementing/developing/introduction/assets/osgi-bundles.png)

## Guide di [!DNL Experience Manager] {#guides}

L’elenco completo delle funzioni nuove e migliorate dell’ultima versione delle Guide di Adobe Experience Manager è disponibile [qui](https://experienceleague.adobe.com/it/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2406-release/whats-new-2024-06-0).

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
