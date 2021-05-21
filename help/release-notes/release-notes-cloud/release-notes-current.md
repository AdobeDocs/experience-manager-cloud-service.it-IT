---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager] come Cloud Service.
description: Note sulla versione corrente per  [!DNL Adobe Experience Manager] come Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 6c1320d43b551247e63962dd52ada58d463fb92e
workflow-type: tm+mt
source-wordcount: '1996'
ht-degree: 2%

---


# Note sulla versione corrente per [!DNL Adobe Experience Manager] come Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per la versione corrente (più recente) di [!DNL Experience Manager] come Cloud Service.

>[!NOTE]
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, per quelli del 2020, 2021 e così via.

>[!NOTE]
>
>Per informazioni sugli aggiornamenti della documentazione non direttamente correlati a una versione, consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) .

## Data di rilascio {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2021.4.0 è il 6 maggio 2021.
La versione seguente (2021.5.0) sarà il 27 maggio 2021.

## AEM come Cloud Service Foundation{#aem-as-a-cloud-service-foundation}

### Novità {#what-is-new-foundation}

* [Flusso di lavoro Pubblica albero contenuto](/help/operations/replication.md#publish-content-tree-workflow) : un nuovo modello di flusso di lavoro e un nuovo passaggio consentono di migliorare le prestazioni durante la pubblicazione di gerarchie profonde di contenuto.

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novità in [!DNL Sites] {#what-is-new-sites}

* Endpoint GraphQL: è ora possibile abilitare l’API GraphQL AEM per le singole configurazioni AEM Sites e creare endpoint GraphQL personalizzati per tali configurazioni utilizzando una nuova interfaccia utente della console GraphQL. L’interfaccia utente consente inoltre di gestire gli endpoint GraphQL.

* Modelli di contenuto, tipo di dati Data e ora avanzato: è ora possibile configurare il tipo di data e ora per consentire l’authoring di solo informazioni su data, ora o data e ora.

* Modelli di contenuto, tipo di dati di tag avanzati: è ora possibile configurare il tipo di dati Tag per consentire la creazione di uno o più tag.

* Modelli di contenuto, nuovo tipo di dati segnaposto tabulazione : il nuovo tipo di dati segnaposto per tabulazione consente di raggruppare i tipi di dati in sezioni che verranno sottoposte a rendering in schede nell’editor frammento di contenuto.

### Correzioni di bug in [!DNL Sites] {#bug-fixes-sites}

* Frammenti di contenuto : lo spostamento di frammenti di contenuto o cartelle aggiorna ora i riferimenti nidificati all’interno del frammento (CQ-4320815)

* GraphQL: le query persistenti ora supportano endpoint definiti dall&#39;utente specifici per le configurazioni di AEM Sites (CQ-4315928)

## [!DNL Adobe Experience Manager Assets] come  [!DNL Cloud Service] {#assets}

### Novità in [!DNL Assets] {#what-is-new-assets}

* [!DNL Experience Manager] non archivia i download di singole risorse in cui viene scaricato il file originale. Questo miglioramento consente download più veloci. Consulta [scaricare risorse](/help/assets/download-assets-from-aem.md).

* Quando scarichi una risorsa tramite un’opzione di condivisione dei collegamenti, ora puoi scegliere di scaricare o meno i rendering. In precedenza, venivano scaricate tutte le rappresentazioni delle risorse. Consulta [opzioni di download](/help/assets/download-assets-from-aem.md).

* Durante l’esecuzione di un controllo di integrità per importare le risorse in blocco, Experience Manager fornisce ora ulteriori informazioni sui motivi degli errori. Consulta [inserimento di risorse in blocco](/help/assets/add-assets.md#asset-bulk-ingestor).

* Quando si importano le risorse utilizzando lo strumento di importazione in blocco, gli amministratori ora possono eliminare i file di origine dopo il successo dell’importazione. Consulta [inserimento di risorse in blocco](/help/assets/add-assets.md#asset-bulk-ingestor).

* Durante la modifica di uno schema di metadati, un nuovo campo di selezione del percorso principale consente agli amministratori di effettuare la selezione in modo rapido e semplice. Questo miglioramento consente di ridurre i tempi di configurazione dei metadati.

* I metadati di molte risorse possono essere importati in blocco utilizzando un file CSV e possono essere esportati in un file CSV. Il formato di data predefinito è ora `yyyy-MM-dd'T'HH:mm:ss.SSSXXX`. Gli utenti possono utilizzare un formato diverso aggiornando l’intestazione della colonna. Ad esempio, aggiungi `Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX` come intestazione di colonna nel file CSV anziché la parola `Date`. Consulta [importare metadati](/help/assets/metadata-import-export.md).

* Nella vista a colonne, un indicatore visivo mostra lo stato di approvazione o rifiuto di ciascuna risorsa.

* Nella vista a colonne, viene visualizzato un indicatore visivo per le risorse scadute.

* Nell’editor di metadati [!DNL Assets] è disponibile un tipo di dati dell’area di testo. È possibile utilizzare questa opzione per consentire agli utenti di immettere i metadati in un campo di testo a forma libera.

### Correzioni di bug in [!DNL Assets] {#bug-fixes-assets}

* Quando tenti di spostare più risorse o cartelle, viene registrato un errore nella console e l’operazione di spostamento non è completata. L’operazione di spostamento non riesce se il titolo non può essere aggiornato. (CQ-4322080)

* Un campo di metadati può essere nascosto in base a una regola in modo che, quando viene soddisfatta una condizione predefinita, i metadati non siano obbligatori. Tuttavia, tali campi di metadati nascosti vengono visualizzati come campi obbligatori. (CQ-4321285)

* Importazione in blocco dei metadati non riuscita a causa di un formato di data non corretto. (CQ-4319014)

* Quando si effettua una selezione nella pagina Proprietà per aggiornare i metadati, l&#39;interfaccia è lenta a rispondere quando ci sono molte opzioni fornite dallo schema. (CQ-4318538)

* Durante l’aggiornamento e il salvataggio del valore dei metadati in un campo di testo a riga singola, i valori nel menu a discesa vengono eliminati, anche se le modifiche sono disabilitate nel menu a discesa. (CQ-4317077)

* Puoi usare i puntini di sospensione come annotazione per esaminare le risorse. Quando si utilizza una piccola ellisse, l&#39;ellisse si sovrappone al numero dell&#39;annotazione nella versione di stampa. (CQ-4316792)

## [!DNL Adobe Experience Manager Forms] come  [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#what-is-new-forms}

È possibile utilizzare [AEM Forms come Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/home.html) per creare moduli digitali, collegare moduli a origini dati esistenti, integrare moduli con Adobe Sign per aggiungere firme elettroniche ai moduli, generare documenti di record (DoR) per archiviare i moduli inviati come file PDF. Il servizio può anche convertire i PDF forms esistenti in moduli digitali. Oltre alle funzioni standard di AEM Forms, il servizio offre diverse funzionalità native per il cloud, come il ridimensionamento automatico, tempi di inattività zero per gli aggiornamenti e ambiente di sviluppo nativo per il cloud. Leggi [questo post di blog](https://blog.adobe.com/en/publish/2021/03/11/experience-manager-forms-as-a-cloud-service.html) per scoprire le funzionalità e le funzionalità di AEM Forms as a Cloud Service.

* **Utilizzare il metodo di autenticazione dell&#39;identità ID governativo in Forms adattivo abilitato per Adobe Sign**

   Basato su algoritmi avanzati di apprendimento automatico, il processo ID governativo di Adobe Sign consente alle aziende di tutto il mondo di garantire un’autenticazione di alta qualità dell’identità del destinatario. Ora puoi utilizzare il metodo di autenticazione dell&#39;identità governativa in Forms adattivo abilitato per Adobe Sign.

   ID governativo è un metodo di autenticazione dell&#39;identità premium che indica al destinatario di [caricare l&#39;immagine di un documento di identità rilasciato dal governo (patente di guida, ID nazionale, passaporto)](https://helpx.adobe.com/in/sign/using/adobesign-authentication-government-id.html) e quindi valuta tale documento per assicurarne l&#39;autenticità.

* **Supporto per l’utilizzo dell’esperienza di firma nei moduli per l’invio asincrono di moduli adattivi**

   È ora possibile utilizzare l’esperienza di firma all’interno del modulo per gli invii asincroni di moduli adattivi. È inoltre possibile incorporare un modulo adattivo in una pagina [!DNL Experience Manager Sites] e utilizzare l’esperienza di firma all’interno del modulo per l’invio di moduli adattivi.

* **Supporto per l&#39;utilizzo di una variabile per specificare un allegato durante la precompilazione di un modulo adattivo per un passaggio Assegna attività**

   Durante la precompilazione di un modulo adattivo per un passaggio Assegna attività, è ora possibile utilizzare una variabile del tipo di documento per selezionare un allegato di input per il modulo adattivo.

* **Supporto per l’utilizzo dell’opzione letterale per impostare il valore per una variabile di tipo JSON**

   Puoi utilizzare l’opzione letterale per impostare il valore per una variabile di tipo JSON nel passaggio della variabile set di un flusso di lavoro AEM. L’opzione letterale ti consente di specificare un JSON sotto forma di stringa.

* **Utilizzare l&#39;ambiente di sviluppo locale per creare un documento di record (DoR)**

   Puoi utilizzare un XDP come modello Documento di record nelle istanze di Cloud Service e AEM Forms as a Cloud Service SDK (ambiente di sviluppo locale). In precedenza, il supporto era limitato solo alle istanze di Cloud Service.

### Correzioni di bug in [!DNL Forms] {#bug-fixes-forms}

* Quando un modulo adattivo configurato per non generare un documento di record viene inviato a un flusso di lavoro AEM configurato per generare un documento di record, non viene visualizzato alcun messaggio di errore e l’attività non viene inviata.

### Altri aggiornamenti {#misc-2021-04-0-forms}

* Per facilitare il riconoscimento del contenuto, il servizio ora genera miniature live per i file XDP, PDF dinamici e schema.
* Aggiunta la possibilità di spostare un file PDF in una cartella inserita nell’interfaccia utente di AEM Forms.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Supporto per UID categoria : consente di sbloccare le integrazioni di e-commerce di terze parti per i sistemi che utilizzano stringhe per ID categoria

* Estensione AEM per PWA Studi incl. integrazione di esempio

* Nuovo componente core di navigazione CIF che estende il componente core di navigazione WCM

* Indicatore visivo per i dati di catalogo in fase di AEM vetrina

* L’endpoint Commerce è ora configurato tramite l’interfaccia utente di Cloud Manager

### Correzioni di bug {#bug-fixes-commerce}

* Il campo della categoria principale non veniva visualizzato nella scheda commercio nelle proprietà della pagina delle pagine delle categorie


## Cloud Manager {#cloud-manager}

Questa sezione illustra le note sulla versione per Cloud Manager in AEM as a Cloud Service 2021.5.0 e 2021.4.0.

### Data di rilascio {#release-date-cm-may}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.5.0 è il 6 maggio 2021.
La prossima versione è prevista per il 3 giugno 2021.

### Novità {#what-is-new-may}

* La regola di qualità PackageOverlaps ora rileva i casi in cui lo stesso pacchetto è stato distribuito più volte, ovvero in più posizioni incorporate, nello stesso set di pacchetti distribuito.

* L’endpoint dell’archivio nell’API pubblica ora include l’URL Git.

* Il registro di distribuzione scaricato da un utente di Cloud Manager sarà più dettagliato e ora includerà dettagli sugli errori e sugli scenari di successo.

* Sono stati risolti gli errori intermittenti durante il push del codice all’Git di Adobe.

* È ora possibile applicare il componente aggiuntivo Commerce ai programmi Sandbox durante il flusso di lavoro Modifica programma .

* L&#39;esperienza del programma Edit è stata aggiornata.

* La tabella Nomi di dominio nella pagina Dettagli ambiente visualizza fino a 250 nomi di dominio tramite impaginazione.

* La scheda Soluzioni nei flussi di lavoro Aggiungi programma e Modifica programma visualizzerà la soluzione, anche se per il programma è disponibile una sola soluzione.

* Il messaggio di errore nel registro dei passaggi della build quando la build non produceva pacchetti di contenuto distribuiti non era chiaro.

### Correzioni di bug {#bug-fixes-cm-may}

* In alcuni casi, l’utente potrebbe visualizzare uno stato verde &quot;attivo&quot; accanto a un Elenco consentiti IP anche quando tale configurazione non è stata distribuita.

* Invece di rimuovere le variabili &quot;eliminate&quot;, le variabili delle pipeline API le contrassegnavano solo con lo stato **ELIMINATO**.

* Alcuni problemi di qualità del tipo di odore del codice hanno avuto un impatto errato sul rating di affidabilità.

* Poiché i domini con caratteri jolly non sono supportati, l’interfaccia utente non consente all’utente di inviare un dominio con caratteri jolly.

* Quando è stata avviata l’esecuzione di una pipeline tra la mezzanotte e l’1:00 UTC, la versione dell’artefatto generata da Cloud Manager non era garantita come maggiore di una versione creata il giorno precedente.

* Durante la configurazione del programma Sandbox, una volta che il progetto con codice di esempio è stato creato correttamente, Manage Git (Gestisci Git) apparirà come collegamento dalla scheda eroe nella pagina Overview (Panoramica).

### Data di rilascio {#release-date-cm-april}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.4.0 è l’8 aprile 2021.

### Novità {#what-is-new-april}

* L’interfaccia utente è aggiornata ai flussi di lavoro Aggiungi e Modifica programma per renderlo più intuitivo.

* Un utente con le autorizzazioni necessarie può ora inviare l’endpoint di e-commerce tramite l’interfaccia utente di .

* Le variabili di ambiente possono ora essere indirizzate a un servizio specifico, sia per l’authoring che per la pubblicazione. Richiede AEM versione `2021.03.5104.20210328T185548Z` o successiva.

* Il pulsante **Manage Git** viene visualizzato sulla scheda Pipelines anche quando non è stata configurata alcuna pipeline.

* La versione dell’archetipo di progetto AEM utilizzato da Cloud Manager è stata aggiornata alla versione 27.

* I progetti nella Console per sviluppatori di Adobe I/O creata da Cloud Manager non possono più essere modificati o eliminati accidentalmente.

* Quando un utente aggiunge un nuovo ambiente, viene informato che una volta creato l’ambiente non può essere spostato in un’area diversa.

* Le variabili di ambiente possono ora essere indirizzate a un servizio specifico, sia per l’authoring che per la pubblicazione. Richiede AEM versione 2021.03.5104.20210328T185548Z o superiore.

* È stato chiarito il messaggio di errore durante l’avvio di una pipeline quando un ambiente è stato eliminato.

* I bundle OSGi forniti dai progetti Eclipse ora sono esclusi dalla regola `CQBP-84--dependencies`.

### Correzioni di bug {#bug-fixes-cm-april}

* Quando modifichi la pagina di audit esperienza di una pipeline, un percorso di input che inizia con una barra `( / )` non bloccherà più il passaggio nello stato in sospeso.

* Quando viene creata una nuova pipeline di produzione, se l’utente non aggiunge alcuna sostituzione di controllo del contenuto, la pagina home predefinita non è stata sottoposta a controllo.

* I problemi relativi alla `CloudServiceIncompatibleWorkflowProcess` presentavano una gravità errata nel file CSV del problema scaricabile.

* Il controllo `Runmode` produceva falsi positivi sui nodi non presenti nelle cartelle.

## Strumento Content Transfer (Trasferimento contenuti) {#content-transfer-tool}

### Data di rilascio {#release-date-ctt}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.4.0 è l’11 maggio 2021.

### Novità {#what-is-new-ctt-may}

* Questa versione dello strumento Content Transfer (Trasferimento contenuti) crea rappresentazioni di testo per le risorse da migrare al Cloud Service. Le rappresentazioni di testo sono necessarie per supportare la ricerca full-text sulle risorse acquisite.
* Il numero massimo di set di migrazione dello strumento Content Transfer (Trasferimento contenuti) che un utente può creare è stato aumentato da 4 a 10.

### Correzioni di bug {#bug-fixes-ctt-may}

* Correzioni di bug multipli relative alla funzione di aggiornamento automatico nell’interfaccia utente dello strumento Content Transfer (Trasferimento contenuti).
* Lo strumento Content Transfer (Trasferimento contenuti) con `wipe=true` causava un indice di contatore errato nel target. Questo problema è stato risolto.

## Analisi delle best practice {#best-practices-analyzer}

### Data di rilascio {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.12 è il 12 aprile 2021.

### Correzioni di bug {#bug-fixes-bpa-april}

* Sono state visualizzate righe duplicate nel BPA segnalato. Questo problema è stato risolto.
* L’interfaccia utente BPA sulla versione 6.4.2 AEM generava un errore JS che disattivava il pulsante Genera report . È stato corretto

