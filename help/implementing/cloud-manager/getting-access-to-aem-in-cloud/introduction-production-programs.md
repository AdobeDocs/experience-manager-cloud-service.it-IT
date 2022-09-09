---
title: Introduzione ai programmi di produzione
description: Scopri quali sono i programmi di produzione e suggerimenti su come impostare i tuoi.
exl-id: bb8d4a5a-b26a-4718-9327-149fedb87e6a
source-git-commit: a6152a1529b5c70bcf056857204e7ff97fc614e4
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 2%

---


# Introduzione ai programmi di produzione {#production-programs}

Un programma di produzione è destinato a un team pronto per iniziare a scrivere, creare e testare il codice allo scopo di distribuirlo per ospitare il traffico live.

Dopo [creare il programma di produzione,](creating-production-programs.md) a [creazione guidata programma](using-the-wizard.md) guida l’utente attraverso le selezioni a seconda dell’obiettivo dell’utente nella creazione del programma.

## Opzioni di creazione del programma {#program-creation-options}

Il contratto stipulato con l’Adobe definisce il numero e i tipi di soluzioni disponibili per la tua organizzazione specifica durante la creazione di programmi di produzione. Puoi controllare come mappare le soluzioni disponibili ai programmi Cloud Manager.

Nella tabella seguente sono descritti gli scenari comuni delle soluzioni disponibili e i programmi di produzione tipici creati in base ad esse.

| Soluzioni disponibili | Opzioni del programma | Contenuto | Quando utilizzare | Esempi |
|--- |--- |--- |--- |---|
| 1 soluzione Sites | Crea 1 programma solo siti | 1 Produzione + 1 fase, 1 sviluppo | N/D | N/D |
| 1 soluzione Assets | Crea 1 programma solo risorse | 1 Produzione + 1 fase, 1 sviluppo | N/D | N/D |
| 1 Sites +1 Assets | Crea un programma: <br>1 Programma Sites &amp; Assets | 1 Produzione + 1 fase, 2 sviluppo | Quando la maggior parte delle risorse digitali viene utilizzata per supportare l’implementazione dei siti.<br>In questi casi, la maggior parte delle risorse digitali è in uno stato finito, pronto per essere utilizzato per le esperienze cross-channel tramite Sites.<br>In genere, un singolo team è responsabile della gestione dei contenuti sia per Sites che per Assets. | Immagini utilizzate principalmente per un sito web.<br>PDF che verranno distribuiti tramite un portale interno integrato in AEM Sites. |
| 1 Sites +1 Assets | Creare programmi separati:<br>1 solo programma di Sites e 1 solo programma di Assets | 1 Produzione + 1 fase, 1 sviluppo<br> 1 Produzione + 1 fase, 1 sviluppo | Quando molte risorse digitali non supportano direttamente l’implementazione dei siti.<br> In questi casi, le risorse sono in vari stati, compresi i tipi di file non elaborati e i lavori in corso.<br>Un team creativo dedicato gestisce le risorse digitali attraverso il proprio ciclo di vita e dispone di flussi di lavoro e cicli di rilascio separati rispetto al team di gestione dei contenuti di Sites. | Le immagini non elaborate da un servizio fotografico sono memorizzate nel programma Assets e solo alcune verranno utilizzate nell’implementazione di Sites.<br>Un gran numero di tipi di file di Creative Cloud, come Photoshop e Illustrator, vengono gestiti in AEM Assets e passano attraverso il proprio flusso di lavoro di approvazione prima che venga generata una risorsa finita.<br>Considera l&#39;utilizzo di [Risorse collegate](/help/assets/use-assets-across-connected-assets-instances.md#overview-of-connected-assets) in tali casi. |
| 1 siti + 1 siti | Creare programmi separati:<br>1 Programma solo siti e 1 programma solo siti | 1 Produzione + 1 fase, 1 sviluppo<br>1 Produzione + 1 fase, 1 sviluppo | Per le implementazioni di siti multi-tenant.<br>In questi casi, è necessario gestire più siti con la propria pianificazione delle versioni e team dedicati di sviluppo e contenuti. | Due marchi retail con siti web dedicati e team di sviluppo separati |

>[!NOTE]
>
>Programmi di produzione [possono essere modificati e non eliminati.](editing-programs.md)
