---
title: Gestione delle versioni dei progetti Maven
description: Per le distribuzioni di staging e produzione di AEM as a Cloud Service, Cloud Manager genera una versione univoca e incrementale.
exl-id: 658bcbed-0733-45da-a3e3-9a5f817099c5
source-git-commit: 21607fadf33dac038c7f794b933b92f60b8e20a9
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 3%

---


# Gestione delle versioni dei progetti Maven {#maven-project-version-handling}

Per le distribuzioni di staging e produzione di AEM as a Cloud Service, Cloud Manager genera una versione univoca e incrementale

Questa versione viene visualizzata nella pagina [pagina dei dettagli di esecuzione della pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) e la pagina dell’attività. Quando viene eseguita una build, il progetto Maven viene aggiornato per utilizzare questa versione e viene creato un tag nell’archivio Git con tale versione come nome.

Se la versione del progetto originale soddisfa determinati criteri, la versione del progetto Maven aggiornata unirà sia la versione del progetto originale che la versione generata da Cloud Manager. Tuttavia, il tag utilizza sempre la versione generata. Affinché l’unione si verifichi, la versione originale del progetto deve essere formata con esattamente tre segmenti di versione, ad esempio: `1.0.0` o `1.2.3`, ma non `1.0` o `1`e la versione originale non deve terminare in `-SNAPSHOT`.

>[!IMPORTANT]
>
>Il valore della versione del progetto originale deve essere impostato in modo statico nel `<version>` elemento del livello superiore `pom.xml` nel ramo dell’archivio git.

Se la versione originale soddisfa questi criteri, la versione generata verrà aggiunta alla versione originale come segmento di nuova versione. Anche la versione generata verrà leggermente modificata per includere l’ordinamento e la gestione delle versioni corrette. Ad esempio, supponendo una versione generata di `2019.926.121356.0000020490` avrebbe i seguenti risultati.

| Versione | Versione in `pom.xml` | Commenti |
|---|---|---|
| `1.0.0` | `1.0.0.2019_0926_121356_0000020490` | Versione originale formata correttamente |
| `1.0.0-SNAPSHOT` | `2019.926.121356.0000020490` | Versione istantanea, sovrascritta |
| `1` | `2019.926.121356.0000020490` | Versione incompleta, sovrascritta |

>[!NOTE]
>
>Indipendentemente dal fatto che la versione originale sia stata incorporata o meno nella versione inizializzata da Cloud Manager, la versione originale è disponibile come proprietà Maven con il nome `cloudManagerOriginalVersion`.
