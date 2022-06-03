---
title: Convalida dei trasferimenti di contenuto (legacy)
description: Utilizza lo strumento Content Transfer (Trasferimento contenuti) per convalidare i trasferimenti di contenuto
hide: true
hidefromtoc: true
source-git-commit: 1fb4d0f2a3b3f9a27f5ab1228ec2d419149e0764
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 1%

---

# Convalida dei trasferimenti di contenuto (legacy) {#validating-content-transfers}

## Guida introduttiva {#getting-started}

Gli utenti possono determinare in modo affidabile se tutti i contenuti estratti dallo strumento Content Transfer (Trasferimento contenuti) sono stati correttamente acquisiti nell’istanza di destinazione. Questa funzione di convalida funziona confrontando un riassunto dei nodi coinvolti durante l’estrazione con un riassunto dei nodi coinvolti durante l’acquisizione. Se nel digest di estrazione mancano percorsi di nodo nel digest di acquisizione, la convalida si considera non riuscita e potrebbe essere necessaria una convalida manuale aggiuntiva.

>[!INFO]
>
>Questa funzione sarà disponibile a partire dalla versione 1.8.x dello strumento Content Transfer (CTT) . L’ambiente di destinazione di AEM Cloud Service deve essere in esecuzione almeno nella versione 6158 o successiva. Richiede inoltre la configurazione dell&#39;ambiente sorgente per l&#39;esecuzione [pre-copia](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#setting-up-pre-copy-step). La funzione di convalida cerca il file azcopy.config nell&#39;origine. Se il file non viene trovato, la convalida non viene eseguita. Per ulteriori informazioni su come configurare un file azcopy.config, vedi [questa pagina](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#configure-azcopy-config-file).

La convalida di un trasferimento di contenuto è facoltativa. L’abilitazione di questa funzione aumenta sia il tempo necessario per eseguire un’estrazione che un’acquisizione. Per utilizzare la funzione, abilitala nella console di sistema dell’ambiente AEM sorgente seguendo questi passaggi:

1. Passa alla console Web di Adobe Experience Manager nell’istanza sorgente, scegliendo **Strumenti - Operazioni - Console web** o direttamente all’URL in *https://serveraddress:serverport/system/console/configMgr*
1. Cerca **Configurazione del servizio di estrazione dello strumento Content Transfer (Trasferimento contenuti)**
1. Utilizza il pulsante icona a forma di matita per modificarne i valori di configurazione
1. Abilita la **Abilita convalida di migrazione durante l’estrazione** premere **Salva**:

   ![immagine](/help/journey-migration/content-transfer-tool/assets/CTTvalidation1.png)

Con questa impostazione abilitata e con l’ambiente AEM Cloud Service di destinazione che esegue una versione compatibile, la convalida della migrazione verrà eseguita durante tutte le operazioni di estrazione e acquisizione successive.

Per ulteriori informazioni su come installare lo strumento Content Transfer (Trasferimento contenuti), consulta [Guida introduttiva allo strumento Content Transfer (Trasferimento contenuti)](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md).

## Convalidare un trasferimento di contenuti {#how-to-validate-a-content-transfer}

Con la convalida della migrazione abilitata nell’ambiente AEM di origine, inizia un’estrazione.

Se **Sovrascrivi contenitore di staging durante l’estrazione** è attivato, tutti i nodi coinvolti nell’estrazione verranno registrati nel digest del percorso di estrazione. Quando si utilizza questa impostazione, è importante abilitare **Cancella il contenuto esistente sull’istanza Cloud prima dell’acquisizione** durante l’acquisizione, in caso contrario potrebbero mancare nodi nel digest di acquisizione. Si tratta dei nodi già presenti nel target da acquisizioni precedenti.

Per un&#39;illustrazione grafica, si prega di fare riferimento agli esempi seguenti:

### Esempio 1 {#example-1}

* **Estrazione (sovrascrittura)**

   ![immagine](/help/journey-migration/content-transfer-tool/assets/CTTextractionoverwrite.png)

* **Acquisizione (Wipe)**

   ![immagine](/help/journey-migration/content-transfer-tool/assets/CTTingestionwipe.png)

* **Note**

   Questa combinazione di &quot;Sovrascrivi&quot; e &quot;Cancella&quot; darà luogo a risultati di convalida coerenti, anche per acquisizioni ripetute.

### Esempio 2 {#example-2}

* **Estrazione**

   ![immagine](/help/journey-migration/content-transfer-tool/assets/CTTextraction.png)

* **Acquisizione**

   ![immagine](/help/journey-migration/content-transfer-tool/assets/CTTingestion.png)

* **Note**

   Questa combinazione di &quot;Sovrascrivi&quot; e &quot;Cancella&quot; darà luogo a risultati di convalida coerenti per l’acquisizione iniziale.

   Se l’acquisizione viene ripetuta, il digest di acquisizione sarà vuoto e la convalida apparirà non riuscita. Il digest di acquisizione sarà vuoto perché tutti i nodi di questa estrazione saranno già presenti nel target.

Una volta completata l’estrazione, inizia l’acquisizione.

La parte superiore del registro di acquisizione conterrà una voce, simile a `aem-ethos/tools:1.2.438`. Verifica che il numero di versione sia **1.2.438** o superiore, in caso contrario la convalida non è supportata dal rilascio di AEM as a Cloud Service in uso.

Una volta completata l’acquisizione e avviata la convalida, la seguente voce di registro verrà annotata nel registro di acquisizione:

```
Gathering artifacts for migration validation...  
```

I dettagli della convalida seguiranno questa voce. Di seguito è riportato un esempio di migrazione di grandi dimensioni:

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

Questo è un esempio di convalida riuscita, in quanto non mancavano voci nel digest di acquisizione presenti nel digest di estrazione.

Per confrontare, in caso di errore di convalida, come si presenterà un rapporto di convalida:

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

L’esempio di errore di cui sopra è stato ottenuto eseguendo un’acquisizione, e quindi eseguendo nuovamente la stessa acquisizione con Wipe disabilitata, in modo tale che nessun nodo era coinvolto durante l’acquisizione, tutto era già presente sul target.

Oltre a essere incluso nel registro di acquisizione, il rapporto di convalida è accessibile anche dall’interfaccia utente dello strumento Content Transfer (Trasferimento contenuti). A tale scopo, seleziona un set di migrazione e fai clic sul pulsante **Convalida** dalla barra delle azioni:


![immagine](/help/journey-migration/content-transfer-tool/assets/CTTvalidatebutton.png)

Viene visualizzata la finestra di dialogo Registri di convalida:

![immagine](/help/journey-migration/content-transfer-tool/assets/CTTvalidationlogs.png)

Utilizza la **Rapporto Pubblicazione/Autore convalida** per visualizzare il rapporto di convalida per l’acquisizione più recente nel livello specificato dell’ambiente di destinazione. Di seguito è riportato un esempio tratto da una piccola acquisizione di pubblicazione:

![immagine](/help/journey-migration/content-transfer-tool/assets/CTTvalidationreport.png)

>[!NOTE]
>
>La **Rapporto Pubblicazione/Autore convalida** al termine dell’acquisizione verrà visualizzato il collegamento . Inoltre, i rapporti di convalida vengono mantenuti e non scadono al termine dell’acquisizione, come fanno i registri di acquisizione.

## Risoluzione dei problemi {#troubleshooting}

### Convalida non riuscita. E adesso? {#validation-fail}

Il primo passaggio consiste nel determinare se l’acquisizione ha avuto esito negativo o se il contenuto estratto è già presente nell’ambiente di destinazione. Ciò può verificarsi se un’acquisizione viene ripetuta con **Cancella il contenuto esistente sull’istanza Cloud prima dell’acquisizione** Opzione disabilitata.

Per verificare, scegli un percorso dal rapporto di convalida e verifica se è presente nell’ambiente di destinazione. Se si tratta di un ambiente di pubblicazione, puoi limitarti a controllare direttamente pagine e risorse. Apri un ticket con l’Assistenza clienti se hai bisogno di assistenza per questo passaggio.

### Il conteggio dei nodi è inferiore a quanto mi aspettavo. Perché? {#node-count-lower-than-expected}

Alcuni percorsi dei digesti di estrazione e acquisizione sono esclusi appositamente per mantenere le dimensioni di questi file gestibili, con l’obiettivo di poter calcolare il risultato della convalida della migrazione entro due ore dal completamento dell’acquisizione.

I percorsi che escludiamo attualmente dai digesti includono: `cqdam.text.txt` rappresentazioni, nodi `/home`e i nodi all&#39;interno di `/jcr:system`.
