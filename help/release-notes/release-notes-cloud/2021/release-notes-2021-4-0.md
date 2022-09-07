---
title: Note sulla versione 2021.4.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione 2021.4.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 775332b5-24ce-430e-97a2-6eeb80877c64
source-git-commit: 8f4b504898b1332c21f3cb82ab9bbf663c9dc312
workflow-type: tm+mt
source-wordcount: '1535'
ht-degree: 9%

---

# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per la versione corrente (più recente) di [!DNL Adobe Experience Manager] as a Cloud Service.

>[!NOTE]
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, per quelli del 2020, 2021 e così via.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

Data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2021.4.0 è il 6 maggio 2021.
La versione seguente (2021.5.0) sarà il 27 maggio 2021.

## AEM as a Cloud Service Foundation{#aem-as-a-cloud-service-foundation}

### Novità {#what-is-new-foundation}

* [Flusso di lavoro Pubblica albero del contenuto](/help/operations/replication.md#publish-content-tree-workflow) - Un nuovo modello e un nuovo passaggio del flusso di lavoro fornisce prestazioni migliori durante la pubblicazione di gerarchie profonde di contenuti.

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novità in [!DNL Sites] {#what-is-new-sites}

* Endpoint GraphQL: è ora possibile abilitare l’API GraphQL AEM per le singole configurazioni AEM Sites e creare endpoint GraphQL personalizzati per tali configurazioni utilizzando una nuova interfaccia utente della console GraphQL. L’interfaccia utente consente inoltre di gestire gli endpoint GraphQL.

* Modelli di contenuto, tipo di dati Data e ora avanzato: è ora possibile configurare il tipo di data e ora per consentire l’authoring di solo informazioni su data, ora o data e ora.

* Modelli di contenuto, tipo di dati di tag avanzati: è ora possibile configurare il tipo di dati Tag per consentire la creazione di uno o più tag.

* Modelli di contenuto, nuovo tipo di dati segnaposto tabulazione : il nuovo tipo di dati segnaposto per tabulazione consente di raggruppare i tipi di dati in sezioni che verranno sottoposte a rendering in schede nell’editor frammento di contenuto.

### Correzioni di bug in [!DNL Sites] {#bug-fixes-sites}

* Frammenti di contenuto : lo spostamento di frammenti di contenuto o cartelle aggiorna ora i riferimenti nidificati all’interno del frammento (CQ-4320815)

* GraphQL: le query persistenti ora supportano endpoint definiti dall&#39;utente specifici per le configurazioni di AEM Sites (CQ-4315928)

## [!DNL Adobe Experience Manager Assets] come [!DNL Cloud Service] {#assets}

### Novità in [!DNL Assets] {#what-is-new-assets}

* [!DNL Experience Manager] non archivia i download di singole risorse in cui viene scaricato il file originale. Questo miglioramento consente download più veloci.

* Quando una risorsa viene scaricata tramite l’opzione di condivisione dei collegamenti, ora puoi scegliere di scaricare o meno i rendering. In precedenza, venivano scaricate tutte le rappresentazioni delle risorse.

* Gli amministratori possono configurare [!DNL Experience Manager] per eliminare l’origine delle risorse dopo l’assimilazione di risorse in massa. Vedi [inserimento di risorse in massa](/help/assets/add-assets.md#asset-bulk-ingestor).

* Durante l’esecuzione di un controllo di integrità per importare le risorse in blocco, Experience Manager fornisce ora ulteriori informazioni sui motivi degli errori. Vedi [inserimento di risorse in massa](/help/assets/add-assets.md#asset-bulk-ingestor).

* Quando si importano le risorse utilizzando lo strumento di importazione in blocco, gli amministratori ora possono eliminare i file di origine dopo il successo dell’importazione. Vedi [inserimento di risorse in massa](/help/assets/add-assets.md#asset-bulk-ingestor).

* Durante la modifica di uno schema di metadati, un nuovo campo di selezione del percorso principale consente agli amministratori di effettuare la selezione in modo rapido e semplice, riducendo in tal modo il tempo di configurazione.

* Durante la modifica di uno schema di metadati, viene aggiunto un tipo di dati che fornisce un’area di testo in formato libero nell’editor di metadati. Gli utenti possono utilizzare questa area di testo per immettere testo in formato libero come metadati di una risorsa. Vedi [editor di schemi di metadati](/help/assets/metadata-schemas.md).

* I metadati di molte risorse possono essere importati in blocco utilizzando un file CSV e possono essere esportati in un file CSV. Il formato della data predefinito è ora `yyyy-MM-dd'T'HH:mm:ss.SSSXXX`. Gli utenti possono utilizzare un formato diverso aggiornando l’intestazione della colonna. Ad esempio, aggiungi `Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX` come intestazione di colonna nel file CSV anziché come parola `Date`.

* Nella vista a colonne, un indicatore visivo mostra lo stato di approvazione o rifiuto di ciascuna risorsa.

* Nella vista a colonne, viene visualizzato un indicatore visivo per le risorse scadute.

### Correzioni di bug in [!DNL Assets] {#bug-fixes-assets}

* Quando tenti di spostare più risorse o cartelle, viene registrato un errore nella console e l’operazione di spostamento non è completata. L’operazione di spostamento non riesce se il titolo non può essere aggiornato. (CQ-4322080)

* Un campo di metadati può essere nascosto in base a una regola in modo che, quando viene soddisfatta una condizione predefinita, i metadati non siano obbligatori. Tuttavia, tali campi di metadati nascosti vengono visualizzati come campi obbligatori. (CQ-4321285)

* Importazione in blocco dei metadati non riuscita a causa di un formato di data non corretto. (CQ-4319014)

* Quando si effettua una selezione nella pagina Proprietà per aggiornare i metadati, l&#39;interfaccia è lenta a rispondere quando ci sono molte opzioni fornite dallo schema. (CQ-4318538)

* Durante l’aggiornamento e il salvataggio del valore dei metadati in un campo di testo a riga singola, i valori nel menu a discesa vengono eliminati, anche se le modifiche sono disabilitate nel menu a discesa. (CQ-4317077)

* Puoi usare i puntini di sospensione come annotazione per esaminare le risorse. Quando si utilizza una piccola ellisse, l&#39;ellisse si sovrappone al numero dell&#39;annotazione nella versione di stampa. (CQ-4316792)

* L’opzione di pubblicazione rapida non viene visualizzata quando una risorsa viene selezionata dai risultati della ricerca dopo la ricerca. (CQ-4317748)

## [!DNL Adobe Experience Manager Forms] come [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#what-is-new-forms}

* **Utilizzare il metodo di autenticazione dell&#39;identità ID governativo in Forms adattivo abilitato per Adobe Sign**

   Basato su algoritmi avanzati di apprendimento automatico, il processo ID governativo di Adobe Sign consente alle aziende di tutto il mondo di garantire un’autenticazione di alta qualità dell’identità del destinatario. Ora puoi utilizzare il metodo di autenticazione dell&#39;identità governativa in Forms adattivo abilitato per Adobe Sign.

   ID governativo è un metodo di autenticazione dell&#39;identità premium che istruisce il destinatario a [caricare l’immagine di un documento d’identità rilasciato dal governo (patente di guida, ID nazionale, passaporto)](https://helpx.adobe.com/in/sign/using/adobesign-authentication-government-id.html), quindi valuta il documento per assicurarne l&#39;autenticità.

* **Supporto per l’utilizzo dell’esperienza di firma nei moduli per l’invio asincrono di moduli adattivi**

   È ora possibile utilizzare l’esperienza di firma all’interno del modulo per gli invii asincroni di moduli adattivi. È inoltre possibile incorporare un modulo adattivo in un [!DNL Experience Manager Sites] e utilizzare l’esperienza di firma in-form per l’invio di moduli adattivi.

* **Supporto per l&#39;utilizzo di una variabile per specificare un allegato durante la precompilazione di un modulo adattivo per un passaggio Assegna attività**

   Durante la precompilazione di un modulo adattivo per un passaggio Assegna attività, è ora possibile utilizzare una variabile del tipo di documento per selezionare un allegato di input per il modulo adattivo.

* **Supporto per l’utilizzo dell’opzione letterale per impostare il valore per una variabile di tipo JSON**

   Puoi utilizzare l’opzione letterale per impostare il valore per una variabile di tipo JSON nel passaggio della variabile set di un flusso di lavoro AEM. L’opzione letterale ti consente di specificare un JSON sotto forma di stringa.

* **Utilizzare l&#39;ambiente di sviluppo locale per creare un documento di record (DoR)**

   Puoi utilizzare un XDP come modello Documento di record nelle istanze di Cloud Service e AEM Forms as a Cloud Service SDK (ambiente di sviluppo locale). In precedenza, il supporto era limitato solo alle istanze di Cloud Service.

### Correzioni di bug in [!DNL Forms] {#bug-fixes-forms}

* Quando un modulo adattivo configurato per non generare un documento di record viene inviato a un flusso di lavoro AEM configurato per generare un documento di record, non viene visualizzato alcun messaggio di errore e l’attività non viene inviata.

### Altri aggiornamenti {#misc-2021-04-0-forms}

* Per facilitare il riconoscimento del contenuto, il servizio ora genera miniature live per i file XDP, Dynamic PDF e Schema.
* Possibilità di spostare un file PDF in una cartella memorizzata nell’interfaccia utente di AEM Forms.

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

Questa sezione illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.4.0.

### Data di pubblicazione {#release-date-cm-april}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.4.0 è l’8 aprile 2021.
La prossima versione è prevista per il 6 maggio 2021.

### Novità {#what-is-new-april}

* L’interfaccia utente è aggiornata ai flussi di lavoro Aggiungi e Modifica programma per renderlo più intuitivo.

* Un utente con le autorizzazioni necessarie può ora inviare l’endpoint di e-commerce tramite l’interfaccia utente di .

* Le variabili di ambiente possono ora essere indirizzate a un servizio specifico, sia per l’authoring che per la pubblicazione. Richiede AEM versione `2021.03.5104.20210328T185548Z` o superiore.

* La **Gestisci Git** sulla scheda Pipelines viene visualizzato il pulsante anche quando non è stata configurata alcuna pipeline.

* La versione dell’archetipo di progetto AEM utilizzato da Cloud Manager è stata aggiornata alla versione 27.

* I progetti nella Console per sviluppatori di Adobe I/O creata da Cloud Manager non possono più essere modificati o eliminati accidentalmente.

* Quando un utente aggiunge un nuovo ambiente, viene informato che una volta creato l’ambiente non può essere spostato in un’area diversa.

* Le variabili di ambiente possono ora essere indirizzate a un servizio specifico, sia per l’authoring che per la pubblicazione. Richiede AEM versione 2021.03.5104.20210328T185548Z o superiore.

* È stato chiarito il messaggio di errore durante l’avvio di una pipeline quando un ambiente è stato eliminato.

* I bundle OSGi forniti dai progetti Eclipse ora sono esclusi dalla regola `CQBP-84--dependencies`.

### Correzioni di bug {#bug-fixes-cm-april}

* Quando modifichi la pagina di audit esperienza di una pipeline, crea un percorso di input che inizia con una barra `( / )` non comporterà più il blocco del passaggio nello stato in sospeso.

* Quando viene creata una nuova pipeline di produzione, se l’utente non aggiunge alcuna sostituzione di controllo del contenuto, la pagina home predefinita non è stata sottoposta a controllo.

* Problemi relativi al `CloudServiceIncompatibleWorkflowProcess` aveva la gravità errata nel file CSV del problema scaricabile.

* La `Runmode` check stava producendo falsi positivi sui nodi non cartelle.

## Analisi delle best practice {#best-practices-analyzer}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.12 è il 12 aprile 2021.

### Correzioni di bug {#bug-fixes-bpa-april}

* Sono state visualizzate righe duplicate nel BPA segnalato. Questo problema è stato risolto.
* L’interfaccia utente BPA sulla versione 6.4.2 AEM generava un errore JS che disattivava il pulsante Genera report . Questo problema è stato risolto.
