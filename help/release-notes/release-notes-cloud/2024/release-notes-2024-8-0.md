---
title: Note sulla versione 2024.8.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2024.8.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
feature: Release Information
role: Admin
exl-id: dd1d4b8f-8331-4e97-a754-37e720974db6
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 98%

---

# Note sulla versione 2024.8.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione funzionale 2024.8.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2022 o 2023.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Per ricevere una notifica e-mail mensile sugli aggiornamenti delle note sulla versione di Experience Cloud, abbonati ad [Adobe Priority Product Update](https://www.adobe.com/subscription/priority-product-update.html).

## Data di pubblicazione {#release-date}

La data di rilascio della versione corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2024.8.0) è il 29 agosto 2024. La prossima versione funzionale (2024.9.0) è pianificata per il 26 settembre 2024.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica sulla versione di agosto 2024 per un riepilogo delle funzioni aggiunte alla versione 2024.8.0:

>[!VIDEO](https://video.tv.adobe.com/v/3433381?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuova funzione in Experience Manager Sites {#new-feature-sites}

**Authoring di AEM per Edge Delivery Services**

Ora è supportata, la funzionalità [ereditarietà](/help/sites-cloud/authoring/universal-editor/inheritance.md) dei siti esistenti, tra cui:

* [Lanci AEM](/help/sites-cloud/authoring/launches/overview.md)
* [MSM](/help/sites-cloud/administering/msm/overview.md) a livello di pagina

Inoltre, sono ora supportate le seguenti funzioni di gestione delle pagine:

* [I tag AEM](/help/sites-cloud/authoring/sites-console/tags.md) possono essere esportati come [tassonomia](https://www.aem.live/docs/authoring-taxonomy) in Edge Delivery Services.
* [I modelli](/help/sites-cloud/authoring/universal-editor/templates.md) per Edge Delivery Services saranno presto disponibili.

### Programma per i primi utilizzatori {#sites-early-adopter}

**Generare varianti**

Sfruttare l’intelligenza artificiale generativa tramite la nuova funzione di AEM, [genera varianti](/help/generative-ai/generate-variations.md), ora accessibile in Cloud Service. Genera varianti consente di generare e ridimensionare la creazione di contenuti tramite l’utilizzo dell’intelligenza artificiale generativa. Rivolgiti al tuo team Adobe Account per prendere in considerazione il programma.


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni nella vista Risorse {#assets-view-new-features}

**Generazione immagine Adobe Firefly aggiornata**

Assets as a Cloud Service ora utilizza il widget più recente di Firefly che consente di generare immagini in stili diversi utilizzando Adobe Firefly. Definendone stile, composizione, dimensioni e altro ancora mediante l’editor di Firefly integrato, puoi creare e salvare rapidamente le risorse necessarie all’interno dell’archivio AEM Assets per un utilizzo immediato.

![Generazione immagine Adobe Firefly](/help/assets/assets/bugatti-type-57.png)

**Supporto file PSB**

Assets as a Cloud Service ora supporta i documenti di grandi dimensioni di Photoshop (file PSB) oltre al supporto del file PSD esistente.

### Nuovi miglioramenti nell’’hub di contenuti {#content-hub-new-enhancements}

* Migliore gestione dei nomi di file lunghi, facile espansione del nome completo tramite descrizione comando.
* Miniature migliorate per adattarsi meglio alle proporzioni dei contenuti e coprire aree di contenuto più ampie.
* Esperienza di miniature personalizzata da AEM supportata con l’hub di contenuti.
* Miglioramenti nella ricerca dei colori.
* I miglioramenti nell’esperienza di salvataggio delle configurazioni.
* È stata migliorata la pagina delle informazioni delle raccolte per riflettere il nome dell’autore.


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

* **Assistente IA per le query sui prodotti**: ottieni risposte immediate alle domande relative al modulo AEM. L’Assistente IA funge da knowledge base personale, fornendo indicazioni approfondite e consigli direttamente all’interno della piattaforma.

* **Generazione di moduli adattivi**: creazione semplificata di moduli completi con prompt di IA generativa. L’intelligenza artificiale generativa di Adobe genera automaticamente moduli intuitivi che riducono i casi di abbandono e personalizzano l’esperienza.

* **Generazione del pannello per moduli**: genera sezioni del modulo personalizzate in base a esigenze specifiche di raccolta dati. Ad esempio, genera sezioni per la raccolta di informazioni di pagamento, preferenze cliente o dettagli di viaggio.

* **Modifica dei layout del modulo**: prova con layout e progettazioni diversi utilizzando i prompt di IA generativa. Prova diversi layout, ad esempio la procedura guidata o le visualizzazioni a schede, per trovare il layout ideale per il modulo. Utilizza i prompt di intelligenza artificiale generativa per ottimizzare i moduli per la reattività mobile e creare moduli visivamente coinvolgenti che gli utenti apprezzano.

* **Configura azione di invio**: utilizza i prompt di IA generativa per configurare facilmente un’azione di invio per il modulo. Scegli da una libreria di azioni di invio predefinite o da un elenco di azioni di invio personalizzate, create e implementate dal tuo team di sviluppo.

>[!IMPORTANT]
>
> Se ti interessa partecipare al programma di accesso anticipato per qualsiasi innovazione, è sufficiente inviare un’e-mail dal tuo indirizzo ufficiale a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) con l’elenco delle funzionalità che ti interessano.


## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Programmi per i primi utilizzatori relativi alla distribuzione dei contenuti {#foundation-early-adopter}

Invia un’e-mail all’indirizzo **<aemcs-cdn-config-adopter@adobe.com>**, indicando quali dei programmi per i primi utilizzatori seguenti ti interessa.

#### Autenticazione di base alla rete CDN (Programma per i primi utilizzatori) {#basicauth-cdn}

Proteggi alcune risorse di contenuto visualizzando una finestra di dialogo di autenticazione di base che richiede un nome utente e una password. Questa funzione è destinata principalmente a casi d’uso di autenticazione leggera, come la revisione dei contenuti da parte delle parti aziendali interessate, anziché fungere da soluzione completa per i diritti di accesso degli utenti finali. L’elenco di nome utente e password in gestito tramite un file di configurazione in Git distribuito tramite la pipeline di configurazione, con riferimento alle variabili di ambiente Cloud Manager di tipo segreto. [Ulteriori informazioni](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth).

#### Reindirizzamenti Lato Server (Programma Early Adopter) {#server-side-redirects-early-adopter}

Configura i reindirizzamenti lato server 301/302 nel controllo del codice sorgente e distribuiscili alla rete CDN. [Ulteriori informazioni](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors).<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> Attenzione: sono già disponibili diverse altre funzioni correlate a [Configurazione CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md), comprese le trasformazioni di richiesta e risposta e il routing del traffico verso siti esterni ad AEM.

#### Gli utenti aziendali possono dichiarare i reindirizzamenti al di fuori di Git (programma per i primi utilizzatori) {#apache-rewritemaps-early-adopter}

In modo simile ad AEM 6.5, Apache/dispatcher acquisisce le mappe di riscrittura che si trovano in una posizione specifica nell’archivio di pubblicazione e le carica, senza richiedere l’esecuzione di una pipeline a livello web. Questo approccio consente agli utenti aziendali di dichiarare i reindirizzamenti utilizzando un foglio di calcolo o un’interfaccia utente, come ACS Commons Redirect Map Manager o un’applicazione personalizzata. <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### Edge Side Includes (ESI) per il caricamento di contenuti dinamici (programma per i primi utilizzatori) {#esi-early-adopter}

Adobe Managed CDN ora supporta [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md), un linguaggio di markup per l’assemblaggio di contenuti web dinamici a livello di edge. Includendo snippet ESI, è possibile memorizzare nella cache la pagina HTML generale sulla rete CDN con valori TTL più elevati e recuperare con maggiore frequenza dall’origine le sezioni più piccole che richiedono aggiornamenti più frequenti (TTL più bassi). <!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

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
