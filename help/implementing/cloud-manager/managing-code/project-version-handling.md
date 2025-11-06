---
title: Gestione delle versioni dei progetti Maven
description: Per le distribuzioni negli ambienti di staging e produzione di AEM as a Cloud Service, Cloud Manager genera una versione univoca e incrementale.
exl-id: 658bcbed-0733-45da-a3e3-9a5f817099c5
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 100%

---


# Gestione delle versioni dei progetti Maven {#maven-project-version-handling}

Per le distribuzioni negli ambienti di staging e produzione di AEM as a Cloud Service, Cloud Manager genera una versione univoca e incrementale.

Questa versione viene visualizzata nella [pagina dei dettagli di esecuzione delle pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) e nella pagina dell’attività. Quando viene eseguita una build, il progetto Maven viene aggiornato per utilizzare questa versione e viene creato un tag nell’archivio Git con tale versione come nome.

Se la versione del progetto originale soddisfa determinati criteri, nella versione del progetto Maven aggiornata verranno unite sia la versione del progetto originale che la versione generata da Cloud Manager. Tuttavia, il tag utilizza sempre la versione generata. Affinché tale unione si verifichi, la versione originale del progetto deve essere formata da esattamente tre segmenti di versione, ad esempio `1.0.0` o `1.2.3`, ma non `1.0` o `1`, mentre la versione originale non deve terminare con `-SNAPSHOT`.

>[!IMPORTANT]
>
>Il valore della versione originale di questo progetto deve essere impostato in modo statico nell’elemento `<version>` del file `pom.xml` di livello superiore nel ramo dell’archivio Git.

Se la versione originale soddisfa questi criteri, la versione generata viene aggiunta alla versione originale come segmento di nuova versione. Anche la versione generata verrà leggermente modificata per includere l’ordinamento e la gestione delle versioni corrette. Ad esempio, presupponendo la versione generata `2019.926.121356.0000020490`, si otterrebbero i seguenti risultati.

| Versione | Versione in `pom.xml` | Commenti |
|---|---|---|
| `1.0.0` | `1.0.0.2019_0926_121356_0000020490` | Versione originale formata correttamente |
| `1.0.0-SNAPSHOT` | `2019.926.121356.0000020490` | Versione snapshot, sovrascritta |
| `1` | `2019.926.121356.0000020490` | Versione incompleta, sovrascritta |

>[!NOTE]
>
>Indipendentemente dal fatto che la versione originale fosse incorporata nella versione inizializzata da Cloud Manager, la versione originale è disponibile come proprietà Maven con il nome `cloudManagerOriginalVersion`.
