---
title: Strumento di risoluzione dei problemi relativi al trasferimento dei contenuti (legacy)
description: Risoluzione dei problemi dello strumento Content Transfer (Trasferimento contenuti)
hide: true
hidefromtoc: true
exl-id: b99f8f2b-b1b7-4ec1-b1d2-0efe83e17e91
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 94%

---

# Strumento di risoluzione dei problemi relativi al trasferimento dei contenuti (legacy) {#troubleshoot-content-transfer-tool}


## ID BLOB mancanti {#missing-blobs}

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


## Comportamento dell’interfaccia {#ui-behavior}

Come utente, nell’interfaccia dello strumento Content Transfer (Trasferimento contenuti) potresti osservare le seguenti modifiche comportamentali:

* Le icone nell’interfaccia dello strumento Content Transfer (Trasferimento contenuti) possono apparire diverse dalle schermate mostrate in questa guida o possono non apparire affatto, a seconda della versione dell’istanza AEM sorgente.
