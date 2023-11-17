---
title: AEM Repo Tool
description: AEM Repo Tool è una soluzione semplice per trasferire contenuti JCR tra il file system locale e il server AEM tramite la riga di comando, simile all’FTP.
exl-id: fb887ba3-e40b-4ab1-b142-0748c6d9f18e
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 2%

---

# AEM Repo Tool {#aem-repo-tool}

AEM Repo Tool è una soluzione semplice per trasferire contenuti JCR tra il file system locale e il server AEM tramite la riga di comando, simile all’FTP. Lo strumento AEM Repo è simile al [Plug-in Jackrabbit FileVault Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin), ma è più veloce, ha dipendenze minime ed è un semplice script di base.

Questo strumento semplifica il trasferimento dei file per lo sviluppatore e può anche essere integrato in Eclipse e IntelliJ per rendere lo sviluppo ancora più efficiente.

## Panoramica {#overview}

Per un determinato percorso all’interno di un `jcr_root` Struttura FileVault sul file system, lo strumento AEM Repo crea un pacchetto con un singolo filtro per l&#39;intera sottostruttura e lo invia al server (simile all&#39;FTP) `put`), lo recupera dal server ( `get`) o confronta le differenze ( `status` e `diff`).

Lo strumento non supporta più percorsi di filtro o i `filter.xml`.

>[!CAUTION]
>
>Lo strumento AEM Repo Tool sovrascrive sempre l’intero file o la directory specificata.

## Download e documentazione {#download-and-documentation}

Il [Lo strumento AEM Repo è disponibile su GitHub tramite questo collegamento](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) insieme a istruzioni dettagliate per l&#39;installazione e l&#39;utilizzo.

Se desideri scaricare l’origine dello strumento AEM Repo Tool, consulta il progetto GitHub collegato di seguito.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto strumenti su GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
