---
title: AEM Repo Tool
description: AEM Repo Tool è una soluzione semplice per trasferire il contenuto JCR tra il filesystem locale e il server AEM tramite la riga di comando paragonabile a FTP.
exl-id: fb887ba3-e40b-4ab1-b142-0748c6d9f18e
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 2%

---

# Strumento AEM repository {#aem-repo-tool}

AEM Repo Tool è una soluzione semplice per trasferire il contenuto JCR tra il filesystem locale e il server AEM tramite la riga di comando paragonabile a FTP. Lo strumento Repo AEM è simile al [Plug-in Jackrabbit FileVault Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin), ma è più veloce, ha dipendenze minime ed è un semplice script bash.

Questo strumento semplifica il trasferimento di file per lo sviluppatore e può anche essere integrato in Eclipse e IntelliJ per rendere lo sviluppo ancora più efficiente.

## Panoramica {#overview}

Per un determinato percorso all&#39;interno di un `jcr_root` Struttura FileVault sul filesystem, AEM Repo Tool crea un pacchetto con un singolo filtro per l&#39;intero sottoalbero e lo invia al server (simile a FTP `put`), lo recupera dal server ( `get`) o confronta le differenze ( `status` e `diff`).

Lo strumento non supporta più percorsi di filtro o FileVault `filter.xml`.

>[!CAUTION]
>
>Tieni presente che lo AEM Repo Tool sovrascrive sempre l’intero file o directory specificato.

## Download e documentazione {#download-and-documentation}

La [AEM Repo Tool è disponibile su GitHub tramite questo collegamento](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) oltre a istruzioni dettagliate sull&#39;installazione e sull&#39;utilizzo.

Per scaricare l’origine dello strumento Repo AEM, fai riferimento al progetto GitHub collegato di seguito.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Progetto Open tools su GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
