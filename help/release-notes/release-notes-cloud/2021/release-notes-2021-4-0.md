---
title: Note sulla versione 2021.4.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione 2021.4.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 775332b5-24ce-430e-97a2-6eeb80877c64
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1533'
ht-degree: 25%

---

# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per la versione corrente (più recente) di [!DNL Adobe Experience Manager] as a Cloud Service.

>[!NOTE]
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio quelle del 2020, 2021 e così via.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2021.4.0 è il 6 maggio 2021.
La seguente versione (2021.5.0) sarà del 27 maggio 2021.

## Fondazione AEM as a Cloud Service{#aem-as-a-cloud-service-foundation}

### Novità {#what-is-new-foundation}

* [Flusso di lavoro per la pubblicazione della struttura dei contenuti](/help/operations/replication.md#publish-content-tree-workflow) - Un nuovo modello e passaggio di flusso di lavoro offre prestazioni migliori quando si pubblicano gerarchie profonde di contenuti.

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novità in [!DNL Sites] {#what-is-new-sites}

* Endpoint GraphQL: ora è possibile abilitare l’API GraphQL dell’AEM per le singole configurazioni di AEM Sites e per queste configurazioni è possibile creare endpoint GraphQL personalizzati utilizzando una nuova interfaccia utente della console GraphQL. L’interfaccia utente consente inoltre di gestire gli endpoint di GraphQL.

* Modelli di contenuto, tipo di dati Data e ora migliorato - ora puoi configurare il tipo di dati Data e ora per consentire l’authoring di informazioni relative solo alla data, solo all’ora o a data e ora.

* Modelli di contenuto, tipo di dati Tag migliorato: ora puoi configurare il tipo di dati Tag per consentire l’authoring di uno o più tag.

* Modelli di contenuto, nuovo tipo di dati Segnaposto scheda . Il nuovo tipo di dati Segnaposto scheda consente di raggruppare i tipi di dati in sezioni visualizzate all’interno di schede nell’editor dei frammenti di contenuto.

### Correzioni di bug in [!DNL Sites] {#bug-fixes-sites}

* Frammenti di contenuto - Con lo spostamento di frammenti di contenuto o cartelle, ora vengono aggiornati i riferimenti nidificati all’interno del frammento (CQ-4320815)

* GraphQL: le query persistenti ora supportano endpoint definiti dall&#39;utente specifici per le configurazioni di AEM Sites (CQ-4315928)

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novità in [!DNL Assets] {#what-is-new-assets}

* [!DNL Experience Manager] non archivia i download di singole risorse nel punto in cui viene scaricato il file originale. Questo miglioramento consente download più veloci.

* Quando scarichi una risorsa tramite l’opzione di condivisione collegamenti, ora puoi scegliere di scaricare o meno le rappresentazioni. In precedenza, venivano scaricati tutti i rendering delle risorse.

* Gli amministratori possono configurare [!DNL Experience Manager] per eliminare l’origine delle risorse dopo l’inserimento di una risorsa in blocco. Consulta [inserimento in blocco delle risorse](/help/assets/add-assets.md#asset-bulk-ingestor).

* Quando si esegue una verifica stato per importare risorse in blocco, Experience Manager fornisce ora ulteriori informazioni sui motivi degli errori. Consulta [inserimento in blocco delle risorse](/help/assets/add-assets.md#asset-bulk-ingestor).

* Quando importano risorse utilizzando lo strumento di importazione in blocco, gli amministratori ora hanno la possibilità di eliminare i file di origine una volta completata l’importazione. Consulta [inserimento in blocco delle risorse](/help/assets/add-assets.md#asset-bulk-ingestor).

* Quando si modifica uno schema di metadati, un nuovo campo di selezione del percorso principale consente agli amministratori di effettuare la selezione in modo rapido e semplice, riducendo in tal modo il tempo di configurazione.

* Quando si modifica uno schema di metadati, viene aggiunto un tipo di dati che fornisce un’area di testo in formato libero nell’editor di metadati. Gli utenti possono utilizzare questa area di testo per immettere testo in formato libero come metadati di una risorsa. Consulta [editor schema metadati](/help/assets/metadata-schemas.md).

* I metadati di molte risorse possono essere importati in blocco utilizzando un file CSV ed esportati in un file CSV. Il formato di data predefinito è ora `yyyy-MM-dd'T'HH:mm:ss.SSSXXX`. Gli utenti possono utilizzare un formato diverso aggiornando l’intestazione della colonna. Ad esempio, aggiungi `Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX` come intestazione di colonna nel file CSV al posto della parola `Date`.

* Quando esplori le risorse nella vista a colonne, un indicatore visivo mostra lo stato approvato o rifiutato di ciascuna risorsa.

* Quando esplori le risorse nella vista a colonne, un indicatore visivo segnala le risorse scadute.

### Correzioni di bug in [!DNL Assets] {#bug-fixes-assets}

* Quando si tenta di spostare più risorse o cartelle, nella console viene registrato un errore e l’operazione di spostamento non viene completata. Se non è possibile aggiornare il titolo, l&#39;operazione di spostamento non riesce. (CQ-4322080)

* Un campo di metadati può essere nascosto in base a una regola tale che quando viene soddisfatta una condizione predefinita i metadati non sono obbligatori. Tuttavia, tali campi di metadati nascosti vengono visualizzati come campi obbligatori. (CQ-4321285)

* L’importazione di metadati in blocco non riesce a causa di un formato di data errato. (CQ-4319014)

* Quando si effettua una selezione nella pagina Proprietà per aggiornare i metadati, la risposta dell’interfaccia risulta lenta se lo schema fornisce molte opzioni. (CQ-4318538)

* Durante l’aggiornamento e il salvataggio del valore dei metadati in un campo di testo a riga singola, i valori nel menu a discesa vengono eliminati, anche se le modifiche sono disabilitate nel menu a discesa. (CQ-4317077)

* Puoi utilizzare i puntini di sospensione come annotazione per rivedere le risorse. Quando si utilizza un&#39;ellisse piccola, l&#39;ellisse si sovrappone al numero dell&#39;annotazione nella versione di stampa. (CQ-4316792)

* L’opzione Pubblicazione rapida non viene visualizzata quando una risorsa viene selezionata dai risultati della ricerca. (CQ-4317748)

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#what-is-new-forms}

* **Utilizzare il metodo di autenticazione tramite documento ufficiale in Adaptive Forms abilitato per Adobe Sign**

  Basato su algoritmi avanzati di apprendimento automatico, il processo tramite documento ufficiale di Adobe Sign consente alle aziende di tutto il mondo di garantire un’autenticazione di alta qualità dell’identità del destinatario. Ora puoi utilizzare il metodo di autenticazione tramite documento ufficiale in Adaptive Forms abilitato per Adobe Sign.

  Il Government ID è un metodo di autenticazione dell’identità avanzato che indica al destinatario di [caricare l&#39;immagine di un documento di identità ufficiale (patente di guida, carta d&#39;identità, passaporto)](https://helpx.adobe.com/in/sign/using/adobesign-authentication-government-id.html)e quindi valuta il documento per assicurarne l&#39;autenticità.

* **Supporto all’utilizzo dell’esperienza di firma interna ai moduli per l’invio asincrono dei moduli adattivi**

  È ora possibile utilizzare l’esperienza di firma interna ai moduli per l’invio asincrono di moduli adattivi. È inoltre possibile incorporare un modulo adattivo in un [!DNL Experience Manager Sites] e utilizza l’esperienza di firma interna ai moduli per inviare moduli adattivi.

* **Supporto per l’utilizzo di una variabile per specificare un allegato durante la precompilazione di un Modulo adattivo per una fase Assegna attività**

  Durante la precompilazione di un modulo adattivo per una fase Assegna attività, è ora possibile utilizzare una variabile relativa al tipo di documento per selezionare un allegato di input per il modulo adattivo.

* **Supporto per l’utilizzo dell’opzione letterale per impostare il valore per una variabile di tipo JSON**

  È possibile utilizzare l’opzione letterale per impostare il valore di una variabile di tipo JSON nel passaggio Imposta variabile di un flusso di lavoro AEM. L’opzione letterale ti consente di specificare un JSON sotto forma di stringa.

* **Utilizzare l’ambiente di sviluppo locale per creare un documento di record (DoR)**

  Puoi utilizzare un XDP come modello per un documento di record nelle istanze di Cloud Service e nell’SDK as a Cloud Service di AEM Forms (ambiente di sviluppo locale). In precedenza, il supporto era limitato solo alle istanze di Cloud Service.

### Correzioni di bug in [!DNL Forms] {#bug-fixes-forms}

* Quando un modulo adattivo configurato per non generare il documento di record viene inviato a un flusso di lavoro AEM configurato per generare il documento di record, non viene visualizzato alcun messaggio di errore e l’operazione non viene inviata.

### Altri aggiornamenti {#misc-2021-04-0-forms}

* Per facilitare il riconoscimento del contenuto, il servizio ora genera una miniatura live per i file XDP, Dynamic PDF e Schema.
* Aggiungi la possibilità di spostare un file PDF in una cartella inserita nell’interfaccia utente di AEM Forms.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Supporto per la categoria UID: questo consente di sbloccare le integrazioni con e-commerce di terze parti per i sistemi che utilizzano Stringhe per gli ID categoria

* Estensione AEM per il PWA Studi, incl. integrazione di esempio

* Nuovo componente core di navigazione CIF che estende il componente core di navigazione WCM

* Indicatore visivo per i dati di catalogo nella vetrina dell’AEM

* L’endpoint Commerce è ora configurabile tramite l’interfaccia utente di Cloud Manager

### Correzioni di bug {#bug-fixes-commerce}

* Il campo della categoria principale non veniva visualizzato nella scheda Commerce nelle proprietà della pagina delle pagine delle categorie

## Cloud Manager {#cloud-manager}

Questa sezione illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.4.0.

### Data di pubblicazione {#release-date-cm-april}

La data di pubblicazione di Cloud Manager in AEM as a Cloud Service 2021.4.0 è il 8 aprile 2021.
La prossima versione è pianificata per il 6 maggio 2021.

### Novità {#what-is-new-april}

* L’interfaccia utente dei flussi di lavoro Aggiungi e Modifica programma è stata aggiornata per renderli più intuitivi.

* Ora gli utenti con le autorizzazioni necessarie possono inviare l’endpoint di Commerce tramite l’interfaccia utente.

* Ora le variabili di ambiente possono avere l’ambito di un servizio specifico tra Author o Publish. Richiede AEM versione `2021.03.5104.20210328T185548Z` o superiore.

* Il pulsante **Gestisci Git** viene visualizzato nella scheda Pipeline anche quando non è stata configurata alcuna pipeline.

* L’archetipo del progetto AEM utilizzato da Cloud Manager è stato aggiornato alla versione 27.

* Ora non è più possibile modificare o eliminare accidentalmente i progetti nella Console per sviluppatori di Adobe I/O creata da Cloud Manager.

* Quando un utente aggiunge un nuovo ambiente viene informato che, dopo la creazione, l’ambiente non può essere spostato in un’area diversa.

* Ora le variabili di ambiente possono avere l’ambito di un servizio specifico tra Author o Publish. Richiede AEM versione 2021.03.5104.20210328T185548Z o superiore.

* Il messaggio di errore durante l’avvio di una pipeline quando un ambiente veniva eliminato è stato corretto per maggiore chiarezza.

* Ora i bundle OSGi forniti dai progetti Eclipse sono esclusi dalla regola `CQBP-84--dependencies`.

### Correzioni di bug {#bug-fixes-cm-april}

* Ora quando si modifica la pagina Audit dell’esperienza di una pipeline inserendo un percorso di input che inizia con una barra `( / )`, il passaggio non si blocca più nello stato In sospeso.

* Quando si creava una nuova pipeline di produzione, se l’utente non aggiungeva alcuna sostituzione dei contenuti dall’audit, la pagina Home predefinita non veniva sottoposta a audit.

* Alcuni problemi relativi a `CloudServiceIncompatibleWorkflowProcess` riportavano la gravità errata nel file CSV scaricabile relativo ai problemi.

* Il controllo `Runmode` generava falsi positivi per i nodi non inclusi nella cartella.

## Analisi delle best practice {#best-practices-analyzer}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.12 è il 12 aprile 2021.

### Correzioni di bug {#bug-fixes-bpa-april}

* Sono state viste righe duplicate nel BPA segnalato. Questo problema è stato risolto.
* Nell’interfaccia utente BPA della versione 6.4.2 dell’AEM veniva generato un errore JS che causava la disabilitazione del pulsante Genera rapporto. Questo problema è stato risolto.
