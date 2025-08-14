---
title: Note sulla versione 2024.11.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2024.11.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 3fd6482e-66f0-48ee-983c-4cb6b7742dcd
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: tm+mt
source-wordcount: '1810'
ht-degree: 98%

---

# Note sulla versione 2024.11.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione funzionale 2024.11.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2022 o 2023.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Per ricevere una notifica e-mail mensile sugli aggiornamenti delle note sulla versione di Experience Cloud, abbonati ad [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).

## Data di pubblicazione {#release-date}

La data di rilascio della versione funzionale corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2024.11.0) è il 21 novembre 2024. La prossima versione funzionale (2025.1.0) è pianificata per il venerdì 30 gennaio 2025.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica sulla versione di giugno 2024 per un riepilogo delle funzioni aggiunte alla versione 2024.11.0:

>[!VIDEO](https://video.tv.adobe.com/v/3440920?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

**[!DNL Edge Delivery Services]Modelli di pagina con authoring tramite editor universale**

Trasforma rapidamente qualsiasi pagina di Edge Delivery in un modello di pagina. Questo consente di iniziare una nuova pagina con una struttura e un contenuto predefiniti, anziché una pagina vuota. [Ulteriori informazioni](/help/sites-cloud/authoring/universal-editor/templates.md).

**[!DNL Edge Delivery Services]Importazione CSV per la pubblicazione tramite un’istanza AEM**

Gestisci in modo efficiente i dati del foglio di calcolo di Edge Delivery (ad es. reindirizzamenti) nello strumento preferito e caricalo su AEM tramite la nuova funzione di importazione CSV. [Ulteriori informazioni](https://www.aem.live/docs/authoring-tabular-data).

### Funzionalità pre-release in AEM Sites

È stato migliorato il [frammento di contenuto con riferimento a riferimenti univoci basati su ID](/help/headless/graphql-api/uuid-reference-upgrade.md), garantendo collegamenti stabili che rimangono validi anche quando le risorse o i frammenti vengono spostati, eliminando la necessità di aggiornamenti o ripubblicazione. Limitazione corrente: i riferimenti a pagine non sono ancora supportati con ID univoci. Se nei frammenti di contenuto si fa riferimento alle pagine, questa funzionalità non deve essere utilizzata.

### Programma per i primi utilizzatori {#sites-early-adopter}

**OpenAPI REST di AEM per la distribuzione dei frammenti di contenuto**

OpenAPI REST di [AEM per la distribuzione dei frammenti di contenuto](/help/headless/aem-content-fragment-delivery-with-openapi.md) è ora disponibile per AEM as a Cloud Service.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Funzionalità per Accesso anticipato a Dynamic Media {#dm-early-access}

**Didascalie video generate dall’intelligenza artificiale**

Le didascalie video generate dall’intelligenza artificiale in Adobe Dynamic Media utilizzano l’intelligenza artificiale per generare automaticamente le didascalie per i contenuti video. Questa funzione è stata progettata per migliorare l’accessibilità e l’esperienza utente fornendo didascalie accurate e in tempo reale. L’intelligenza artificiale analizza la traccia audio del video per trascrivere il discorso e creare didascalie, che possono essere modificate per maggiore precisione o personalizzazione. Queste didascalie soddisfano i requisiti di accessibilità e migliorano il coinvolgimento video per tipi di pubblico che si affidano al supporto video basato su testo o che preferiscono farlo.

Per ottenere l’accesso anticipato al supporto delle didascalie generate dall’intelligenza artificiale sul tuo account Dynamic Media, [crea e invia un caso all’Assistenza clienti Adobe](/help/assets/dynamic-media/video.md##enable-dash).

**Rapporto di consegna Dynamic Media**

Ottieni informazioni dettagliate sulla consegna delle risorse effettuata con Dynamic Media, con numero di consegna a livello di risorsa, informazioni sul referrer, percorso della risorsa in AEM Assets e ID univoco della risorsa. È possibile generare rapporti per tutte le risorse consegnate tramite Dynamic Media all’archivio AEM Assets o a una specifica gerarchia di cartelle in AEM Assets. Le informazioni approfondite consentono di misurare il ROI delle risorse consegnate, le prestazioni dei canali e di intraprendere attività di gestione delle risorse informate.

Per ottenere l’accesso anticipato al rapporto di consegna Dynamic Media sull’account Dynamic Media, [crea e invia un caso all’Assistenza clienti Adobe](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html).

### Nuove funzioni nella vista Risorse {#assets-view-new-features}

**Pannello Dynamic Media**

La vista Risorse ora consente di accedere alle rappresentazioni Dynamic Media e Dynamic Media con OpenAPI da un pannello separato reso disponibile. Puoi scegliere di copiare l’URL di consegna o scaricare le rappresentazioni in base alla risorsa e al tipo di rappresentazione. Per ulteriori informazioni, consulta [Rappresentazioni Dynamic Media](/help/assets/renditions.md#dynamic-media-renditions) e [Rappresentazioni Dynamic Media con funzionalità OpenAPI](/help/assets/renditions.md#dm-with-openapi-renditions).

![rappresentazioni dinamiche](/help/assets/assets/dm-scene7-renditions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni in AEM Forms {#forms-new-features}

* **[Aggiornamento facile degli ambiti di Adobe Sign](/help/forms/adobe-sign-integration-adaptive-forms.md)**: è possibile modificare gli ambiti di una configurazione Adobe Sign direttamente dalla pagina Configurazioni AEM Cloud, per aggiornare le configurazioni esistenti in modo più rapido e semplice.

* **[Supporto di funzioni asincrone per moduli adattivi](/help/forms/using-async-funct-in-rule-editor.md)**: quando un modulo adattivo richiede operazioni asincrone, ad esempio l’attesa per processi esterni o il recupero di dati, è possibile implementare queste operazioni con funzioni personalizzate e configurarle nell’editor di regole.

### Nuove funzioni pre-release in AEM Forms {#forms-new-prerelease-features}

* **Gestisci pubblicazione**: puoi utilizzare il flusso di lavoro Gestisci pubblicazione per pubblicare o annullare la pubblicazione di moduli in ambienti diversi, in genere dall’istanza di authoring a quelle di pubblicazione e anteprima. Consente agli utenti di pubblicare, annullare o pianificare la pubblicazione dei contenuti in modo semplice.

* **[Salvataggio automatico di una bozza per componenti core basati su moduli adattivi](/help/forms/save-core-component-based-form-as-draft.md)**: una funzione di salvataggio automatico consente di salvare automaticamente come bozza un modulo parzialmente completato. L’utente potrà quindi completare in un secondo momento la compilazione del modulo, anche da un altro dispositivo. Questa funzione migliora i tassi di conversione per le organizzazioni riducendo l’abbandono dei moduli, in quanto gli utenti non devono ricominciare a compilarli dall’inizio.

* **[Miglioramenti dell’editor di regole](/help/forms/invoke-service-enhancements-rule-editor.md)**: per o Moduli adattivi basati su componenti core, ora puoi popolare le opzioni a discesa, impostare pannelli ripetibili e singoli pannelli utilizzando l’output di Avvia servizio e utilizzare il parametro di output del Servizio di richiamata per convalidare altri campi.

* **[Esperienza utente ottimizzata con pulsanti di navigazione nei layout dei pannelli](/help/forms/rule-editor-core-components-usecases.md#navigating-among-panels-using-button)**: è ora possibile aggiungere pulsanti di navigazione ai layout dei pannelli, ad esempio Schede orizzontali, Schede verticali, Pannelli a soffietto o Procedura guidata. Questi pulsanti migliorano l’esperienza utente semplificando il passaggio da un pannello a un altro e concentrandosi sul pannello selezionato.


### Funzionalità per Accesso anticipato ad AEM Forms {#forms-new-early-access-features}

Il programma per l’accesso anticipato ad AEM Forms offre un’opportunità unica per ottenere l’accesso esclusivo a innovazioni all’avanguardia e contribuire a modellarne lo sviluppo.

In queste note sulla versione sono elencate le innovazioni incluse nella versione corrente. Per l’elenco completo delle innovazioni disponibili nell’ambito del programma per l’accesso anticipato, consulta la [documentazione del programma per l’accesso anticipato ad AEM Forms](/help/forms/early-access-ea-features.md).

#### Integrazioni

* **[Integrare moduli adattivi con Adobe Marketo Engage](/help/forms/integrate-form-to-marketo-engage.md)**: AEM Forms as a Cloud Service ora include un’opzione di facile utilizzo per collegare i moduli adattivi con Adobe Marketo Engage. Questa integrazione consente di creare moduli adattivi direttamente con l’acquisizione di lead di Marketo Engage e i relativi oggetti personalizzati. Ora puoi precompilare i campi del modulo con i dati di Marketo Engage e inviare nuovamente i dati per automatizzare i flussi di lavoro come campagne intelligenti e automazione delle e-mail. È inoltre possibile collegare un modulo adattivo alla libreria Munchkin per tenere traccia del numero di visite, clic e invii di moduli.

#### Moduli adattivi e moduli HTML5

* **[Creare moduli adattivi basati su un modello XFA esistente](/help/forms/create-adaptive-form-using-xfa-templates.md)**: è ora possibile creare un modulo adattivo basato su Componenti core utilizzando modelli di modulo XFA (file *.XDP). Questa funzionalità consente ai clienti AEM Forms On-Premise che già investono nella tecnologia XFA di adottare AEM Forms as a Cloud Service.

* **Moduli HTML5 (moduli web basati su XFA)**: ora la clientela di AEM Forms On-Premise che utilizza la tecnologia XFA può passare facilmente ad AEM Forms as a Cloud Service mantenendo la propria esperienza utente esistente con i moduli HTML5 (moduli web basati su XFA). Questa funzionalità consente di eseguire il rendering dei modelli di modulo XFA in formato HTML5, rendendo i moduli accessibili su dispositivi che non supportano moduli PDF basati su XFA.

  ![HTML Forms (moduli web basati su XFA)](/help/forms/assets/html-forms-xfa-based-web-forms.png)


* **[Supporto di stringhe codificate Base64 per file allegati](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment#basic-tab)**: il componente File allegati nei moduli adattivi basati su componenti core ora include un’opzione per inviare i file allegati come stringhe codificate Base64.

#### API di comunicazione e comunicazione interattiva

* **Editor di comunicazioni interattive**: l’editor di comunicazioni interattive è uno strumento grafico di progettazione delle comunicazioni, semplice da usare e che facilita la creazione di corrispondenze personalizzate e basate su dati; funziona in qualsiasi browser moderno. Supporta l’integrazione diretta dei dati, la definizione di logiche complesse e l’integrazione di rich media, garantendo la creazione di documenti, comunicazioni e modelli professionali e conformi alle diverse esigenze aziendali.

  ![Editor di comunicazione interattiva](/help/forms/assets/ic-editor.png)


* **[Miglioramenti della conformità PDF/A](/help/forms/aem-forms-cloud-service-communications-introduction.md#convert-to-and-validate-pdfa-compliant-documents)**: ora puoi utilizzare le API di comunicazione per convertire i documenti PDF in formati PDF/A (1a, 2a, 3a) a scopo di archiviazione, garantendo al contempo l’accessibilità e verificando la conformità agli standard.


* **[API di firma (Document Assurance)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance)**: una nuova API RESTful nelle API di comunicazione consente una facile gestione delle firme PDF. Supporta operazioni quali:
   * Cancella firma: rimuove una firma da un campo specificato.
   * Rimuovi campo firma: elimina un campo firma specificato.

<!-- 
* **Hamburger Menu Layout in Adaptive Forms**: Adaptive Forms now offers a responsive hamburger menu layout for mobile devices. This collapsible menu organizes form sections, making navigation more 
intuitive and improving the mobile form-filling experience.

* **Masked Field with Eye Icon (Password Box Component)**: The Password Box is a text input field that masks the characters typed into it by displaying placeholder symbols. It allows users to securely input sensitive information, such as passwords and enables them to toggle visibility on demand using the eye icon.

-->

## Servizio di conversione automatica dei moduli

* **[Converti moduli PDF in moduli adattivi basati su componenti core](https://experienceleague.adobe.com/it/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms)**: ora puoi utilizzare il servizio di conversione moduli automatica per trasformare moduli PDF, AcroForms o moduli basati su XFA in moduli adattivi basati su componenti core.

>[!IMPORTANT]
>
> Ti interessa partecipare al programma di accesso anticipato per qualsiasi innovazione sui moduli? Invia un’e-mail dal tuo indirizzo ufficiale a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) con l’elenco delle funzionalità che ti interessano.## Componente aggiuntivo CIF {#cloud-services-cif}

## Componente aggiuntivo CIF {#cif}

### Correzioni di bug {#bug-fixes-cif}

* Sono stati corretti i test dell’interfaccia utente per il corretto funzionamento con i componenti core CIF.
* È stato risolto un problema a causa del quale il formato dell’URL delle categorie non funzionava come previsto nell’istanza cloud.

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Migliori prestazioni di replica della struttura (e obsolescenza del flusso di lavoro pubblicazioni di contenuti della struttura) {#tree-replication-performance}

[Passaggio del flusso di lavoro di attivazione della struttura](/help/operations/replication.md#tree-activation) è un nuovo passaggio del modello di flusso di lavoro consigliato per la replica di gerarchie di contenuti profondi. È importante notare che consente alle repliche indipendenti (ad esempio, tramite Pubblicazione rapida o Gestisci pubblicazione) di procedere in parallelo con il flusso di lavoro di replica della struttura in corso. Questa funzione è particolarmente utile se devi pubblicare alcuni contenuti sensibili al fattore tempo mentre è ancora in corso una replica in blocco. Il passaggio della replica della struttura sostituisce il flusso di lavoro Pubblica contenuti struttura e il relativo passaggio del flusso di lavoro, che ora sono obsoleti.

### API basate su OpenAPI - Programma per i primi utilizzatori {#open-apis-earlyadopter}

Gli sviluppatori possono integrare in modo approfondito le funzionalità di AEM as a Cloud Service nelle proprie applicazioni e strumenti. Le nuove API di AEM as a Cloud Service seguiranno le specifiche OpenAPI, con l’obiettivo di essere coerenti, ben documentate e di facile utilizzo. Le credenziali per gli endpoint che richiedono l’autenticazione verranno generate creando progetti Adobe Developer Console.

Scopri di più sulle [API AEM basate su OpenAPI](/help/implementing/developing/open-api-based-apis.md) e prova un [tutorial end-to-end](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) che ne illustra la configurazione e l’utilizzo.

In concreto, gli endpoint API elencati di seguito sono disponibili come parte di un programma per i primi utilizzatori. Per partecipare, inviare un’e-mail all’indirizzo [aem-apis@adobe.com](mailto:aem-apis@adobe.com) con la descrizione di come si intende utilizzarli.
* [API per frammenti di contenuto di Sites](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)
* [API di Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/assets/author/)
* API per Sites e cartelle di Assets
* [API di comunicazione di Forms](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)

### Edge Computing - Richiesta di feedback! {#edge-computing-feedback}

L’Edge computing avvicina l’elaborazione dei dati al browser, il che offre vantaggi quali una latenza ridotta. Come contributo alla roadmap, ci piacerebbe sapere se trovi questa tecnologia utile per i progetti Pubblica consegna AEM e Edge Delivery Services e per cosa pensi di usarla. Invia un’e-mail a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con domande e commenti.

### Nuovo Developer Console di AEM (Beta pubblica) {#aem-developer-console-beta}

Prova una [Developer Console di AEM](/help/implementing/developing/introduction/aem-developer-console.md) rinnovata, che offre un’esperienza più interattiva per il debug del codice in ambienti cloud.

Chiunque può accedere alla versione Beta pubblica facendo clic sul pulsante *Nuova console disponibile* nella Developer Console di AEM corrente. Adobe accoglie con favore i feedback. Si possono inviare via e-mail all’indirizzo [aemcs-new-devconsole-ui-beta@adobe.com](mailto:aemcs-new-devconsole-ui-beta@adobe.com).

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
