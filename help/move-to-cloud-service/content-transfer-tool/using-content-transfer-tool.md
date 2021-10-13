---
title: Utilizzo dello strumento Content Transfer (Trasferimento contenuti)
description: Utilizzo dello strumento Content Transfer (Trasferimento contenuti)
exl-id: a19b8424-33ab-488a-91b3-47f0d3c8abf5
source-git-commit: 5b569ab1b1cca7e5ec46b872f8726fddfc8b8d14
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 57%

---

# Utilizzo dello strumento Content Transfer (Trasferimento contenuti) {#using-content-transfer-tool}

## Esecuzione dello strumento Content Transfer (Trasferimento contenuti) su un’istanza Publish {#running-ctt-on-publish}

Durante lo spostamento del contenuto in un’istanza Publish, è consigliabile installare CTT nell’istanza Publish di origine per spostare il contenuto nell’istanza Publish di destinazione. Segui l’approccio consigliato come descritto di seguito:

* Utilizza la stessa versione del CTT utilizzata nell’istanza di authoring.

* È necessario migrare un solo nodo di pubblicazione. Deve essere rimosso dal load balancer prima di iniziare l’estrazione.

* Quando crei il set di migrazione, utilizza l’URL dell’ambiente AEMaaCS di authoring.

* Durante l’acquisizione per la pubblicazione, il livello di pubblicazione NON viene ridimensionato (a differenza dell’autore). Per precauzione, evitare operazioni di scrittura avviate dall’utente quali:

   * Distribuzione dei contenuti da AEMaaCS Author a Publish in tale ambiente
   * Sincronizzazione utente tra istanze di pubblicazione


## Risoluzione dei problemi {#troubleshooting}

### ID BLOB mancanti {#missing-blobs}

Se vengono segnalati degli ID BLOB mancanti, come indicato di seguito, è necessario eseguire una verifica di coerenza nell’archivio esistente e ripristinarli.
`ERROR o.a.j.o.p.b.AbstractSharedCachingDataStore - Error retrieving record [ba45c53f8b687e7056c85dceebf8156a0e6abc7e]`

Viene eseguito il comando seguente

>[!NOTE]
>
>`--verbose` Questo flag è necessario per segnalare i percorsi dei nodi in cui si fa riferimento ai BLOB.

**Per archivi AEM 6.5 (Oak 1.8 e versioni precedenti)**

```shell
java -jar oak-run.jar datastorecheck --consistency --store [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds] <DATASTORE_CFG> --verbose <OUT_DIR> --dump
```

**Per archivi con Oak successivo alla versione 1.10**

```shell
java -jar oak-run.jar datastore --check-consistency [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds|azureds] <DATASTORE_CFG> --out-dir <OUT_DIR> --work-dir <TEMP_DIR> --verbose
```

Per ulteriori informazioni, consulta [Oak Runnable Jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run).

I file creati per coerenza nel percorso *OUT_DIR* indicato sopra possono quindi essere controllati per individuare percorsi con binary mancanti e possono essere intraprese azioni appropriate come il ripristino da un backup, l’eliminazione dei percorsi, la reindicizzazione e così via.


### Comportamento dell’interfaccia {#ui-behavior}

Come utente, nell’interfaccia dello strumento Content Transfer (Trasferimento contenuti) potresti osservare le seguenti modifiche comportamentali:

* Le icone nell’interfaccia dello strumento Content Transfer (Trasferimento contenuti) possono apparire diverse dalle schermate mostrate in questa guida o possono non apparire affatto, a seconda della versione dell’istanza AEM sorgente.
