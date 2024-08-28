---
title: Convalida dei trasferimenti di contenuto
description: Utilizzare lo strumento Content Transfer (Trasferimento contenuti) per convalidare i trasferimenti di contenuti
exl-id: a12059c3-c15a-4b6d-b2f4-df128ed0eea5
feature: Migration
role: Admin
source-git-commit: b7e485e3b7ce6f2d2fa7fe9b2953d2296186871d
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 1%

---


# Convalida dei trasferimenti di contenuto {#validating-content-transfers}

## Guida introduttiva {#getting-started}

Gli utenti possono determinare in modo affidabile se tutti i contenuti estratti dallo strumento Content Transfer (Trasferimento contenuti) sono stati correttamente acquisiti nell’istanza di destinazione. Questa funzione di convalida funziona confrontando un riepilogo dei percorsi di tutti i nodi coinvolti durante l’estrazione con un riepilogo dei percorsi di tutti i nodi coinvolti durante l’acquisizione. Se nel digest di estrazione sono presenti percorsi di nodo mancanti nel digest di acquisizione, la convalida viene considerata non riuscita e potrebbe essere necessaria un’ulteriore convalida manuale.

>[!INFO]
>
>Questa funzione sarà disponibile a partire dalla versione 1.8.x dello strumento Content Transfer (CTT). L’ambiente di destinazione AEM Cloud Service deve eseguire almeno la versione 6158 o successiva. È inoltre necessario configurare l&#39;ambiente di origine per eseguire [pre-copia](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#setting-up-pre-copy-step). La funzionalità di convalida cerca il file azcopy.config nell&#39;origine. Se il file non viene trovato, la convalida non verrà eseguita. Per ulteriori informazioni su come configurare un file azcopy.config, vedere [Gestione di archivi di contenuti di grandi dimensioni - Configurazione di un file azcopy.config](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#configure-azcopy-config-file).

La convalida di un trasferimento di contenuto è una funzione facoltativa. L’attivazione di questa funzione aumenta sia il tempo necessario per eseguire un’estrazione che quello necessario per l’acquisizione. Per utilizzare la funzione, abilitala nella Console di sistema dell’ambiente AEM sorgente seguendo questi passaggi:

1. Passa alla console Web Adobe Experience Manager nell&#39;istanza di origine, da **Strumenti - Operazioni - Console Web** o direttamente all&#39;URL in *https://serveraddress:serverport/system/console/configMgr*
1. Cerca la **configurazione del servizio di estrazione dello strumento Content Transfer**
1. Utilizza il pulsante di icona della matita per modificarne i valori di configurazione
1. Abilita l&#39;impostazione **Abilita convalida migrazione durante l&#39;estrazione**, quindi premi **Salva**:

   ![immagine](/help/journey-migration/content-transfer-tool/assets/CTTvalidation1.png)

Se questa impostazione è abilitata e l’ambiente AEM Cloud Service di destinazione esegue una versione compatibile, la convalida della migrazione verrà eseguita durante tutte le estrazioni e acquisizioni successive.

Per ulteriori informazioni sull&#39;installazione dello strumento Content Transfer, vedere [Guida introduttiva allo strumento Content Transfer](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md).

## Convalidare un trasferimento di contenuti {#how-to-validate-a-content-transfer}

Con la convalida della migrazione abilitata nell’ambiente AEM di origine, inizia un’estrazione.

Se **Overwrite staging container during extraction** è abilitato, tutti i nodi coinvolti nell&#39;estrazione vengono registrati nel digest del percorso di estrazione. Quando si utilizza questa impostazione, è importante abilitare l&#39;impostazione **Cancella contenuto esistente nell&#39;istanza Cloud prima dell&#39;acquisizione** durante l&#39;acquisizione, altrimenti potrebbero mancare dei nodi nel digest di acquisizione. Si tratta dei nodi già presenti sul target dalle acquisizioni precedenti.

Per un’illustrazione grafica di questo, vedi gli esempi seguenti:

### Esempio 1 {#example-1}

* **Estrazione (sovrascrittura)**

  ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/validation-01.png)

* **Acquisizione (Cancellazione)**

  ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/validation-02.png)

* **Note**

  Questa combinazione di &quot;Sovrascrivi&quot; e &quot;Cancella&quot; darà risultati di convalida coerenti, anche per acquisizioni ripetute.

### Esempio 2 {#example-2}

* **Estrazione**

  ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/validation-03.png)

* **Acquisizione**

  ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/validation-04.png)

* **Note**

  Questa combinazione di &quot;Sovrascrivi&quot; e &quot;Cancella&quot; genera risultati di convalida coerenti per l’acquisizione iniziale.

  Se l’acquisizione viene ripetuta, il digest di acquisizione è vuoto e la convalida non è riuscita. Il digest di acquisizione è vuoto perché tutti i nodi di questa estrazione saranno già presenti nella destinazione.

Una volta completata l’estrazione, inizia l’acquisizione.

La parte superiore del registro di acquisizione conterrà una voce simile a `aem-ethos/tools:1.2.438`. Verificare che il numero di versione sia **1.2.438** o superiore, altrimenti la convalida non è supportata dalla versione di AEM as a Cloud Service in uso.

Una volta completata l’acquisizione e avviata la convalida, nel registro di acquisizione viene annotata la seguente voce di registro:

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

Per confrontare, ecco come apparirebbe un rapporto di convalida se la convalida non fosse riuscita (o se fosse stata eseguita una migrazione di integrazione):

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
See our Migration Validation FAQ (https://www.adobe.com/go/aem_cloud_ctt_validation_en) or open a ticket with Customer Care.
There are 4635 entries present in the extraction digest that are missing from the ingestion digest.
/content/dam/bruce
/content/dam/bruce-assets
... more paths listed (up to 10k) ...
----------------------------------------------------------
Comparing the path digests took 0 seconds
Migration validation took 0 minutes
```

L’esempio di errore precedente è stato ottenuto eseguendo un’acquisizione e quindi eseguendo nuovamente la stessa acquisizione con Wipe disabilitato, in modo che non vi fossero nodi coinvolti durante l’acquisizione — tutto era già presente nel target.

Oltre a essere incluso nel registro di acquisizione, è possibile accedere al rapporto di convalida anche dall&#39;interfaccia utente **Processi di acquisizione** in Cloud Acceleration Manager. A tale scopo, fare clic sui tre punti (**...**), quindi fare clic su **Report di convalida** nel menu a discesa per visualizzare il report di convalida.


![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/CTTvalidationreportnew.png)

## Convalidare la migrazione dell’entità {#how-to-validate-group-migration}

Consulta [Migrazione gruppo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md) per leggere i dettagli della migrazione principale e i motivi per cui è necessaria.

Una volta completata correttamente l’estrazione e l’acquisizione, sono disponibili un riepilogo e un rapporto della migrazione principale. Queste informazioni possono essere utilizzate per verificare quali gruppi sono stati migrati correttamente e, forse, per determinare perché alcuni non lo sono stati.

Per visualizzare queste informazioni, passa a Cloud Acceleration Manager. Fai clic sulla scheda del progetto e poi sulla scheda Content Transfer (Trasferimento contenuti). Passa a **Processi di acquisizione** e individua l&#39;acquisizione da verificare. Fai clic sui tre punti (**...**) per l&#39;acquisizione, quindi fai clic su **Visualizza riepilogo entità** nel menu a discesa.

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-principal-action.png)

Viene visualizzata una finestra di dialogo con le informazioni di riepilogo. Utilizzare le icone della guida per una descrizione più completa. Fai clic sul pulsante **Scarica rapporto** per scaricare il rapporto CSV completo.  Inoltre, alla fine di questo rapporto c’è il Rapporto utenti, che può essere utilizzato per la gestione degli utenti dopo la migrazione.

![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-principal-dialog.png)

Il rapporto principale sulla migrazione conterrà:

* È stata eseguita la migrazione di ogni gruppo e del primo percorso di contenuto che ha attivato la migrazione del gruppo. Il gruppo potrebbe trovarsi anche in altri percorsi, ma viene segnalato solo il primo trovato per un determinato gruppo. Indica anche se è stato trovato in un ACL o in un criterio CUG.
* Ogni gruppo non è stato migrato e il motivo per cui non è stato migrato.  In genere si tratta di uno dei seguenti motivi:
   * È un gruppo incorporato
   * È già presente nel sistema di destinazione
   * Non è incluso in un criterio ACL o CUG per il contenuto di cui si esegue la migrazione
   * Ha un campo univoco duplicato (uno tra rep:principalName, rep:authorizableId, jcr:uuid o rep:externalId è già presente nella destinazione, ma tutti devono essere univoci)

## Risoluzione dei problemi {#troubleshooting}

### Convalida non riuscita. E adesso? {#validation-fail}

Il primo passaggio consiste nel determinare se l’acquisizione non ha avuto esito positivo o se il contenuto estratto è già presente nell’ambiente di destinazione. Ciò può verificarsi se un&#39;acquisizione viene ripetuta con l&#39;opzione **Cancella contenuto esistente nell&#39;istanza cloud prima dell&#39;acquisizione** disabilitata.

Per verificare il funzionamento, scegliere un percorso dal rapporto di convalida e verificare se è presente nell&#39;ambiente di destinazione. Se si tratta di un ambiente di pubblicazione, potresti essere limitato al controllo diretto di pagine e risorse. Apri un ticket presso l’Assistenza clienti se hai bisogno di assistenza per questo passaggio.

### Il conteggio dei nodi è inferiore al previsto. Perché? {#node-count-lower-than-expected}

Alcuni percorsi dai digest di estrazione e acquisizione sono esclusi appositamente per mantenere gestibili le dimensioni di questi file, con l’obiettivo di poter calcolare il risultato della convalida della migrazione entro due ore dal completamento dell’acquisizione.

I percorsi attualmente esclusi dai digest includono: `cqdam.text.txt` rappresentazioni, nodi all&#39;interno di `/home` e nodi all&#39;interno di `/jcr:system`.

### Gruppi utenti chiusi {#validating-cugs}

Vedere [Migrazione di gruppi utenti chiusi](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) per ulteriori considerazioni sull&#39;utilizzo di un criterio Gruppo utenti chiuso.
