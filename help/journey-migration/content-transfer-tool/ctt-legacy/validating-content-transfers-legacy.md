---
title: Convalida dei trasferimenti di contenuto (legacy)
description: Utilizzare lo strumento Content Transfer (Trasferimento contenuti) per convalidare i trasferimenti di contenuti
hide: true
hidefromtoc: true
exl-id: 304b7aee-1d84-4d90-a89b-0c532d5d9c92
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 2%

---

# Convalida dei trasferimenti di contenuto (legacy) {#validating-content-transfers}

## Guida introduttiva {#getting-started}

Gli utenti possono determinare in modo affidabile se tutti i contenuti estratti dallo strumento Content Transfer sono stati correttamente acquisiti nell’istanza di destinazione. Questa funzione di convalida funziona confrontando un digest dei nodi coinvolti durante l’estrazione con un digest dei nodi coinvolti durante l’acquisizione. Se nel digest di estrazione sono presenti percorsi di nodo mancanti nel digest di acquisizione, la convalida viene considerata non riuscita e potrebbe essere necessaria un’ulteriore convalida manuale.

>[!INFO]
>
>Questa funzione sarà disponibile a partire dalla versione 1.8.x dello strumento Content Transfer (CTT). L’ambiente di destinazione AEM Cloud Service deve eseguire almeno la versione 6158 o successiva. Richiede anche che l’ambiente di origine sia configurato per essere eseguito [pre-copia](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#setting-up-pre-copy-step). La funzionalità di convalida cerca il file azcopy.config nell&#39;origine. Se il file non viene trovato, la convalida non verrà eseguita. Per ulteriori informazioni su come configurare un file azcopy.config, vedere [questa pagina](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#configure-azcopy-config-file).

La convalida di un trasferimento di contenuto è una funzione facoltativa. L’abilitazione di questa funzione aumenta sia il tempo necessario per eseguire un’estrazione che l’acquisizione. Per utilizzare la funzione, abilitala nella console di sistema dell’ambiente AEM sorgente seguendo questi passaggi:

1. Passa alla console web di Adobe Experience Manager nell’istanza sorgente, da **Strumenti - Operazioni - Console web** o direttamente all’URL in *https://serveraddress:serverport/system/console/configMgr*
1. Cerca **Configurazione del servizio di estrazione dello strumento Content Transfer**
1. Utilizza il pulsante di icona della matita per modificarne i valori di configurazione
1. Abilita **Abilita convalida migrazione durante l’estrazione** , quindi premere **Salva**:

   ![immagine](/help/journey-migration/content-transfer-tool/assets/CTTvalidation1.png)

Se questa impostazione è abilitata e l’ambiente AEM Cloud Service di destinazione esegue una versione compatibile, la convalida della migrazione verrà eseguita durante tutte le estrazioni e acquisizioni successive.

Per ulteriori informazioni su come installare lo strumento Content Transfer (Trasferimento contenuti), consulta [Guida introduttiva allo strumento Content Transfer (Trasferimento contenuti)](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md).

## Convalidare un trasferimento di contenuti {#how-to-validate-a-content-transfer}

Con la convalida della migrazione abilitata nell’ambiente AEM di origine, inizia un’estrazione.

Se **Sovrascrivi contenitore staging durante l’estrazione** è abilitato, tutti i nodi coinvolti nell’estrazione verranno registrati nel riepilogo del percorso di estrazione. Quando si utilizza questa impostazione, è importante abilitare **Cancella i contenuti esistenti nell’istanza Cloud prima dell’acquisizione** durante l’acquisizione, altrimenti potrebbero mancare dei nodi dal digest di acquisizione. Si tratta dei nodi già presenti sul target dalle acquisizioni precedenti.

Per un’illustrazione grafica, consulta gli esempi seguenti:

### Esempio 1 {#example-1}

* **Estrazione (sovrascrittura)**

   ![immagine](/help/journey-migration/content-transfer-tool/assets/CTTextractionoverwrite.png)

* **Acquisizione (Wipe)**

   ![immagine](/help/journey-migration/content-transfer-tool/assets/CTTingestionwipe.png)

* **Note**

   Questa combinazione di &quot;Sovrascrivi&quot; e &quot;Cancella&quot; darà risultati di convalida coerenti, anche per acquisizioni ripetute.

### Esempio 2 {#example-2}

* **Estrazione**

   ![immagine](/help/journey-migration/content-transfer-tool/assets/CTTextraction.png)

* **Acquisizione**

   ![immagine](/help/journey-migration/content-transfer-tool/assets/CTTingestion.png)

* **Note**

   Questa combinazione di &quot;Sovrascrivi&quot; e &quot;Cancella&quot; genera risultati di convalida coerenti per l’acquisizione iniziale.

   Se l’acquisizione viene ripetuta, il riepilogo dell’acquisizione sarà vuoto e la convalida non riuscirà. Il digest di acquisizione sarà vuoto perché tutti i nodi di questa estrazione saranno già presenti nella destinazione.

Una volta completata l’estrazione, inizia l’acquisizione.

La parte superiore del registro di acquisizione conterrà una voce simile a `aem-ethos/tools:1.2.438`. Verifica che il numero di versione sia **1,2,438** o superiore, altrimenti la convalida non è supportata dal rilascio di AEM as a Cloud Service che si sta utilizzando.

Una volta completata l’acquisizione e avviata la convalida, nel registro di acquisizione verrà annotata la seguente voce di registro:

```
Gathering artifacts for migration validation...  
```

I dettagli della convalida seguiranno questa voce. Di seguito è riportato un esempio tratto da una migrazione di grandi dimensioni:

```
Beginning publish migration validation. Migration job id=[3aba1f96-84b6-4bd0-8642-c61c0d528387]
Extraction path digest is being processed...
Extraction path digest processing took 982 seconds
Ingestion path digest is being processed...
Ingestion path digest processing took 999 seconds
Comparing the Extraction and Ingestion path digests...
----------------------------------------------------------
EXTRACTION: Number of nodes extracted: 51674784
INGESTION: Number of nodes ingested: 51674784
----------------------------------------------------------
Validation succeeded! No entries were detected to be missing from the ingestion digest.
----------------------------------------------------------
Comparing the path digests took 29 seconds
Migration validation took 33 minutes
```

Questo è un esempio di convalida riuscita, poiché nel digest di estrazione non erano presenti voci mancanti nel digest di acquisizione.

Per confrontare, ecco come apparirebbe un rapporto di convalida se la convalida non fosse riuscita:

```
Beginning publish migration validation. Migration job id=[ac217e5a-a08d-4e81-cbd6-f39f88b174ce]
Extraction path digest is being processed...
Extraction path digest processing took 0 seconds
Ingestion path digest is being processed...
Ingestion path digest processing took 0 seconds
Comparing the Extraction and Ingestion path digests...
----------------------------------------------------------
EXTRACTION: Number of nodes extracted: 4635
INGESTION: Number of nodes ingested: 0
----------------------------------------------------------
Validation failed. However, the following nodes may already be present in the target environment.
Please refer to our Migration Validation FAQ (https://www.adobe.com/go/aem_cloud_ctt_validation_en) or open a ticket with Customer Care.
There are 4635 entries present in the extraction digest that are missing from the ingestion digest.
/content/dam/bruce
/content/dam/bruce-assets
... more paths listed (up to 10k) ...
----------------------------------------------------------
Comparing the path digests took 0 seconds
Migration validation took 0 minutes
```

L’esempio di errore precedente è stato ottenuto eseguendo un’acquisizione e quindi eseguendo nuovamente la stessa acquisizione con Wipe disabilitato, in modo che non vi fossero nodi coinvolti durante l’acquisizione — tutto era già presente nel target.

Oltre a essere incluso nel registro di acquisizione, il rapporto di convalida è accessibile dall’interfaccia utente dello strumento Content Transfer (Trasferimento contenuti). A questo scopo, seleziona un set di migrazione e fai clic sul pulsante **Convalida** dalla barra delle azioni:


![immagine](/help/journey-migration/content-transfer-tool/assets/CTTvalidatebutton.png)

Viene visualizzata la finestra di dialogo Registri di convalida:

![immagine](/help/journey-migration/content-transfer-tool/assets/CTTvalidationlogs.png)

Utilizza il **Rapporto di convalida pubblicazione/authoring** per visualizzare il rapporto di convalida per l’acquisizione più recente nel livello specificato dell’ambiente di destinazione. Di seguito trovi un esempio da una piccola acquisizione di pubblicazione:

![immagine](/help/journey-migration/content-transfer-tool/assets/CTTvalidationreport.png)

>[!NOTE]
>
>Il **Rapporto di convalida pubblicazione/authoring** al termine dell’acquisizione verrà visualizzato il collegamento. Inoltre, i rapporti di convalida vengono mantenuti e non scadono al termine dell’acquisizione, come accade invece per i registri di acquisizione.

## Risoluzione dei problemi {#troubleshooting}

### Convalida non riuscita. E adesso? {#validation-fail}

Il primo passaggio consiste nel determinare se l’acquisizione non ha avuto esito positivo o se il contenuto estratto è già presente nell’ambiente di destinazione. Ciò può verificarsi se un’acquisizione viene ripetuta con **Cancella i contenuti esistenti nell’istanza Cloud prima dell’acquisizione** opzione disabilitata.

Per verificare il funzionamento, scegliere un percorso dal rapporto di convalida e verificare se è presente nell&#39;ambiente di destinazione. Se si tratta di un ambiente di pubblicazione, potresti essere limitato al controllo diretto di pagine e risorse. Apri un ticket presso l’Assistenza clienti se hai bisogno di assistenza per questo passaggio.

### Il conteggio dei nodi è inferiore al previsto. Perché? {#node-count-lower-than-expected}

Alcuni percorsi dai digest di estrazione e acquisizione sono esclusi appositamente per mantenere gestibili le dimensioni di questi file, con l’obiettivo di poter calcolare il risultato della convalida della migrazione entro due ore dal completamento dell’acquisizione.

I percorsi che attualmente escludiamo dai digest includono: `cqdam.text.txt` rappresentazioni, nodi in `/home`, e nodi in `/jcr:system`.
