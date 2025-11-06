---
title: Note sulla versione 2024.10.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2024.10.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 7a63f04f-10f0-4879-bd06-4182bb288a9b
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1663'
ht-degree: 99%

---

# Note sulla versione 2024.10.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione funzionale 2024.10.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2022 o 2023.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Per ricevere una notifica e-mail mensile sugli aggiornamenti delle note sulla versione di Experience Cloud, abbonati ad [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).

## Data di pubblicazione {#release-date}

La data di rilascio della versione funzionale corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2024.10.0) è il 31 ottobre 2024. La prossima versione funzionale (2024.11.0) è pianificata per il 21 novembre 2024.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Video sulla versione {#release-video}

Dai un’occhiata al video di panoramica sulla versione di ottobre 2024 per un riepilogo delle funzioni aggiunte alla versione 2024.10.0:

>[!VIDEO](https://video.tv.adobe.com/v/3440501?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**Eventi pagina modernizzati**

I seguenti eventi pagina di AEM Sites sono ora disponibili come eventi fruibili esternamente basati sulla piattaforma di eventi di AEM as a Cloud Service. Gli eventi possono essere elaborati tramite Adobe I/O per interagire con i processi esterni.

* Pagina pubblicata
* Pagina di cui è stata annullata la pubblicazione
* Pagina eliminata

### Programma per i primi utilizzatori {#sites-early-adopter}

**Generare varianti**

Sfruttare l’intelligenza artificiale generativa tramite la nuova funzione di AEM, [genera varianti](/help/generative-ai/generate-variations.md), ora accessibile in Cloud Service. Genera varianti consente di generare e ridimensionare la creazione di contenuti tramite l’utilizzo dell’intelligenza artificiale generativa. Rivolgiti al tuo team Adobe Account per prendere in considerazione il programma.

**OpenAPI REST di AEM per la distribuzione dei frammenti di contenuto**

OpenAPI REST di [AEM per la distribuzione dei frammenti di contenuto](/help/headless/aem-content-fragment-delivery-with-openapi.md) è ora disponibile per AEM as a Cloud Service.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Funzione per l’accesso anticipato in Dynamic Media {#dm-early-access}

**Didascalie video generate dall’intelligenza artificiale**

Le didascalie video generate dall’intelligenza artificiale in Adobe Dynamic Media utilizzano l’intelligenza artificiale per generare automaticamente le didascalie per i contenuti video. Questa funzione è stata progettata per migliorare l’accessibilità e l’esperienza utente fornendo didascalie accurate e in tempo reale. L’intelligenza artificiale analizza la traccia audio del video per trascrivere il discorso e creare didascalie, che possono essere modificate per maggiore precisione o personalizzazione. Queste didascalie soddisfano i requisiti di accessibilità e migliorano il coinvolgimento video per tipi di pubblico che si affidano al supporto video basato su testo o che preferiscono farlo.

Per ottenere l’accesso anticipato al supporto delle didascalie generate dall’intelligenza artificiale sul tuo account Dynamic Media, [crea e invia un caso all’Assistenza clienti Adobe](/help/assets/dynamic-media/video.md##enable-dash).

### Nuove funzioni nella vista Risorse {#assets-view-new-features}

**Rapporti pianificati**

Ora è possibile generare automaticamente i rapporti nella vista Risorse in base a una pianificazione ricorrente o in una data futura, riducendo gli sforzi per individuare informazioni basate sui dati.

![Rapporti pianificati](/help/assets/assets/scheduled-reports-tab.png)

### Nuove funzioni nell’hub di contenuti {#content-hub-new-features}

**Digital Rights Management per le risorse con licenza**

Le organizzazioni possono ora aumentare la conformità alle licenze e ridurre al minimo il rischio di condividere le risorse con le condizioni di licenza sfruttando DRM per le risorse concesse in licenza agli utenti dell’hub di contenuti, che dovranno rivedere e accettare le condizioni di licenza prima di iniziare a scaricare le risorse concesse in licenza. Per ulteriori informazioni, consulta [Gestire le risorse con licenza nell’hub di contenuti](/help/assets/manage-licensed-assets-on-content-hub.md).

![download-multiple-license](/help/assets/assets/download-multiple-license.png)

**Configurazione metadati scheda risorse**

L’hub di contenuti ora consente di configurare fino a un massimo di 6 campi di metadati chiave da visualizzare nella scheda delle risorse. Per ulteriori informazioni, consulta la sezione Scheda risorse in [Configurare l’hub di contenuti](/help/assets/configure-content-hub-ui-options.md#asset-card).

![metadati chiave nella scheda risorse](/help/assets/assets/asset-card-key-metadata.png)

**Configurare la visibilità e il download delle risorse scadute**

Gli amministratori ora possono verificare se rendere visibili le risorse scadute nell’hub di contenuti. Inoltre, se le risorse scadute vengono rese visibili, possono definire se gli utenti potranno scaricarle. Per ulteriori informazioni, consulta la sezione Risorse scadute in [Configurare l’hub di contenuti](/help/assets/configure-content-hub-ui-options.md#expired-assets-content-hub).

![Risorse scadute nell’hub di contenuti](/help/assets/assets/expired-assets-content-hub.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni in AEM Forms {#forms-new-features}

* [Esperienza utente ottimizzata con pulsanti di navigazione nei layout dei pannelli](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button): è ora possibile aggiungere pulsanti di navigazione ai layout dei pannelli, ad esempio Schede orizzontali, Schede verticali, Pannelli a soffietto o Procedura guidata. Questi pulsanti migliorano l’esperienza utente semplificando il passaggio da un pannello a un altro e concentrandosi sul pannello selezionato.

<!--* **Specify Display Styles for Document of Record (DoR) Components**: In an XFA file, you can now specify the display styles for Document of Record components. These styles can later be applied to the corresponding components in Adaptive Forms Editor.-->

### Nuove funzioni pre-release in AEM Forms {#forms-new-prerelease-features}

* [Salvataggio automatico di una bozza per componenti core basati su moduli adattivi](/help/forms/save-core-component-based-form-as-draft.md): una funzione di salvataggio automatico consente di salvare automaticamente come bozza un modulo parzialmente completato. L’utente potrà quindi completare in un secondo momento la compilazione del modulo, anche da un altro dispositivo. Questa funzione migliora i tassi di conversione per le organizzazioni riducendo l’abbandono dei moduli, in quanto gli utenti non devono ricominciare a compilarli dall’inizio.

* [Aggiornamento facile degli ambiti di Adobe Sign](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/integrate/services/adobe-sign-integration-adaptive-forms): è possibile modificare gli ambiti di una configurazione Adobe Sign direttamente dalla pagina Configurazioni AEM Cloud, per aggiornare le configurazioni esistenti in modo più rapido e semplice.

* [Supporto di funzioni asincrone per moduli adattivi](/help/forms/using-async-funct-in-rule-editor.md): quando un modulo adattivo richiede operazioni asincrone, ad esempio l’attesa per processi esterni o il recupero di dati, è possibile implementare queste operazioni con funzioni personalizzate e configurarle nell’editor di regole.

### Funzionalità per Accesso anticipato ad AEM Forms {#forms-new-early-access-features}

Il programma per l’accesso anticipato ad AEM Forms offre un’opportunità unica per ottenere l’accesso esclusivo a innovazioni all’avanguardia e contribuire a modellarne lo sviluppo.

In queste note sulla versione sono elencate le innovazioni incluse nella versione corrente. Per l’elenco completo delle innovazioni disponibili nell’ambito del programma per l’accesso anticipato, consulta la [documentazione del programma per l’accesso anticipato ad AEM Forms](/help/forms/early-access-ea-features.md).

#### Assistente IA di AEM Forms

[L’intelligenza artificiale generativa per moduli adattivi](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/forms-overview/early-access-ea-features#aem-forms-ai-assistant-gen-ai) offre un livello completamente nuovo di potenza e semplicità ai processi di sviluppo dei moduli. Ti consente di creare moduli migliori più rapidamente che mai.

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

### Correzioni di bug {#bug-fixes-cif}

* Sono stati corretti i test dell’interfaccia utente per il corretto funzionamento con i componenti core CIF.
* È stato risolto un problema a causa del quale il formato dell’URL delle categorie non funzionava come previsto nell’istanza cloud.

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Configurazione per controllare l’invio dei moduli {#configuration-submissions}

Per controllare gli invii dei moduli Coral o Foundation in posizioni specifiche, AEM ha introdotto una nuova configurazione: `com.adobe.granite.ui.components.FormRestrict`. Questa configurazione è costituita da due campi:

1. **Aggiungi percorsi consentiti**: specifica i percorsi in cui sono consentite le azioni del modulo.
1. **Limita comportamento**: determina il comportamento per i percorsi con restrizioni (percorsi non inclusi nell’elenco Consentiti). Puoi scegliere tra due opzioni:
   * **Popup** (impostazione predefinita): mostra una notifica popup.
   * **Impedisci**:Blocks l&#39;invio del modulo.

>[!NOTE]
>
>Questa configurazione non è supportata per tutti i moduli Coral o Foundation che si trovano in `/apps`, `/libs`, `/mnt/overlay` e `/mnt/override`.

### Inoltro self-service dei registri con opzione di rete avanzata {#log-forwarding}

Anche se i registri di AEM (inclusi Apache/Dispatcher) e della CDN possono essere scaricati da Cloud Manager, molte organizzazioni trovano utile inviare in streaming tali registri a una destinazione di registrazione preferita. AEM ora supporta l’[inoltro dei registri](/help/implementing/developing/introduction/log-forwarding.md) ad Azure Blob Storage, Datadog, HTTPS, Elasticsearch (e OpenSearch) e Splunk. I registri di AEM possono essere facoltativamente inoltrati tramite configurazioni di rete avanzate, ad esempio utilizzando un indirizzo IP dedicato.

Questa funzione può essere configurata dagli utenti in modo autonomo e distribuita mediante la [pipeline di configurazione](/help/operations/config-pipeline.md).

### Reindirizzamenti URL senza pipeline per utenti aziendali {#pipeline-free-redirects}

I reindirizzamenti lato browser sono utili quando una pagina web viene rimossa o spostata, o in altri scenari. Con [Reindirizzamenti URL senza pipeline](/help/implementing/dispatcher/pipeline-free-url-redirects.md), è possibile inserire un file di mappa di riscrittura Apache in un percorso di pubblicazione AEM, dove viene caricato automaticamente, senza dover eseguire il commit del file nel controllo del codice sorgente o avviare una pipeline Cloud Manager.

Le opzioni per la pubblicazione del file di riscrittura includono il caricamento come risorsa, l’utilizzo di ACS Commons Rewrite Map Manager o l’interazione con un’interfaccia utente personalizzata.

### Pipeline di configurazione per RDE {#config-pipeline-rdes}

Gli ambienti di sviluppo rapido sono uno strumento potente per implementare e testare rapidamente il codice e la configurazione in un ambiente Cloud. Gli RDE ora supportano la [sincronizzazione dei file YAML di configurazione](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline), incluse le impostazioni CDN quali le regole del filtro del traffico e le trasformazioni di richieste o risposte, nonché l’inoltro dei registri e altre opzioni di configurazione. Per ulteriori dettagli, [consulta l’elenco completo](/help/operations/config-pipeline.md) delle opzioni di configurazione supportate.

### Nuovi profili di prodotto {#new-product-profiles}

Quando viene creato un nuovo ambiente AEM, i profili di prodotto vengono visualizzati automaticamente in Adobe Admin Console, consentendo agli amministratori di assegnare l’accesso alle soluzioni e alle funzioni concesse in licenza.

I nuovi ambienti includono ora un set aggiornato di profili di prodotto, rendendoli compatibili con le funzioni future, inclusa la generazione di credenziali API in Adobe Developer Console. Gli ambienti esistenti saranno in grado di aggiornare i relativi profili di prodotto in una versione futura. [Ulteriori informazioni](/help/onboarding/aem-cs-team-product-profiles.md).

### Nuovo Developer Console di AEM (Beta pubblica) {#aem-developer-console-beta}

Prova una [Developer Console di AEM](/help/implementing/developing/introduction/aem-developer-console.md) rinnovata, che offre un’esperienza più interattiva per il debug del codice in ambienti cloud.

Chiunque può accedere alla versione Beta pubblica facendo clic sul pulsante *Nuova console disponibile* nella Developer Console di AEM corrente. Adobe accoglie con favore qualsiasi feedback che è possibile inviare via e-mail all’indirizzo **<aemcs-new-devconsole-ui-beta@adobe.com>**.

![Schermata dei bundle OSGi nella Developer Console di AEM](/help/implementing/developing/introduction/assets/osgi-bundles.png)

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
