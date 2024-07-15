---
title: AEM Repo Tool
description: AEM Repo Tool è una soluzione semplice per trasferire contenuti JCR tra il file system locale e il server AEM tramite la riga di comando, simile all’FTP.
exl-id: fb887ba3-e40b-4ab1-b142-0748c6d9f18e
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 2%

---

# AEM Repo Tool {#aem-repo-tool}

AEM Repo Tool è una soluzione semplice per trasferire contenuti JCR tra il file system locale e il server AEM tramite la riga di comando, simile all’FTP. Lo strumento AEM Repo è simile al plug-in Maven [Jackrabbit FileVault](https://jackrabbit.apache.org/filevault-package-maven-plugin), ma è più veloce, ha dipendenze minime ed è un semplice script di base.

Questo strumento semplifica il trasferimento dei file per lo sviluppatore e può anche essere integrato in Eclipse e IntelliJ per rendere lo sviluppo ancora più efficiente.

## Panoramica {#overview}

Per un determinato percorso all&#39;interno di una struttura FileVault `jcr_root` nel file system, lo strumento AEM Repo crea un pacchetto con un singolo filtro per l&#39;intera sottostruttura e lo invia al server (in modo simile all&#39;FTP `put`), lo recupera dal server ( `get`) o confronta le differenze ( `status` e `diff`).

Lo strumento non supporta più percorsi di filtro o `filter.xml` di FileVault.

>[!CAUTION]
>
>Lo strumento AEM Repo Tool sovrascrive sempre l’intero file o la directory specificata.

## Download e documentazione {#download-and-documentation}

Lo strumento [AEM Repo Tool è disponibile su GitHub tramite questo collegamento](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) insieme a istruzioni dettagliate di installazione e utilizzo.

Se desideri scaricare l’origine dello strumento AEM Repo Tool, consulta il progetto GitHub collegato di seguito.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto strumenti in GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Scarica il progetto come [file ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
