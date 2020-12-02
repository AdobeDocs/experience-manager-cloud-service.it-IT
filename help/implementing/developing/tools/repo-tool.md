---
title: AEM Repo Tool
description: AEM Repo Tool è una soluzione semplice per trasferire il contenuto JCR tra il file system locale e il server AEM tramite la riga di comando paragonabile all'FTP.
translation-type: tm+mt
source-git-commit: c40d668cb6dcf5c3e2d09504b547457306a99c85
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---


# AEM Repo Tool {#aem-repo-tool}

AEM Repo Tool è una soluzione semplice per trasferire il contenuto JCR tra il file system locale e il server AEM tramite la riga di comando paragonabile all&#39;FTP. AEM Repo Tool è simile al plug-in [Jackrabbit FileVault Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin), ma è più veloce, ha dipendenze minime ed è un semplice script di base.

Questo strumento semplifica il trasferimento di file per lo sviluppatore e può essere integrato in Eclipse e IntelliJ per rendere lo sviluppo ancora più efficiente.

## Panoramica {#overview}

Per un determinato percorso all&#39;interno di una struttura `jcr_root` FileVault del file system, lo strumento AEM Repo crea un pacchetto con un singolo filtro per l&#39;intera struttura secondaria e lo invia al server (simile all&#39;FTP `put`), lo recupera dal server ( `get`) o confronta le differenze ( `status` e `diff`).

Lo strumento non supporta più percorsi di filtro o percorsi di FileVault `filter.xml`.

>[!CAUTION]
>
>Si noti che AEM Repo Tool sovrascriverà sempre l&#39;intero file o directory specificato.

## Download e documentazione {#download-and-documentation}

Il [AEM Repo Tool è disponibile su GitHub tramite questo collegamento](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) con istruzioni dettagliate sull&#39;installazione e l&#39;utilizzo.

Se desiderate scaricare l&#39;origine del AEM Repo Tool, fate riferimento al progetto GitHub collegato di seguito.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Open tools project on GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
