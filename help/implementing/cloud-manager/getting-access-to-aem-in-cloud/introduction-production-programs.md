---
title: Introduzione ai programmi di produzione
description: Scopri che cosa sono i programmi di produzione e suggerimenti su come configurarli.
exl-id: bb8d4a5a-b26a-4718-9327-149fedb87e6a
source-git-commit: a6152a1529b5c70bcf056857204e7ff97fc614e4
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 100%

---


# Introduzione ai programmi di produzione {#production-programs}

Un programma di produzione è destinato ai team pronti per iniziare a scrivere, generare e testare il codice allo scopo di distribuirlo per ospitare il traffico in tempo reale.

Dopo [aver creato un programma di produzione,](creating-production-programs.md) la [procedura guidata per la creazione di un programma](using-the-wizard.md) guida l’utente attraverso diverse opzioni selezionabili in base all’obiettivo prefissato per la creazione del programma.

## Opzioni per la creazione di un programma {#program-creation-options}

Il contratto stipulato con Adobe definisce il numero e i tipi di soluzioni disponibili per l’organizzazione specifica durante la creazione dei programmi di produzione. È l’utente a definire come associare le soluzioni disponibili ai programmi di Cloud Manager.

Nella tabella seguente sono descritti gli scenari comuni delle soluzioni disponibili e i programmi di produzione generalmente creati in base alle stesse.

| Soluzioni disponibili | Opzioni del programma | Contenuto | Applicazione consigliata | Esempi |
|--- |--- |--- |--- |---|
| 1 soluzione Sites | Creazione di 1 programma solo Sites | 1 ambiente produzione + 1 ambiente di staging, 1 ambiente di sviluppo | N/D | N/D |
| 1 soluzione Assets | Creazione di 1 programma solo Assets | 1 ambiente produzione + 1 ambiente di staging, 1 ambiente di sviluppo | N/D | N/D |
| 1 Sites + 1 Assets | Creazione di un solo programma: <br>1 programma Sites &amp; Assets | 1 ambiente produzione + 1 ambiente di staging, 2 ambienti di sviluppo | Quando la maggior parte delle risorse digitali viene utilizzata per supportare l’implementazione di Sites.<br>In questi casi, la maggior parte delle risorse digitali è in uno stato completato, pronta per essere utilizzata nelle esperienze cross-channel tramite Sites.<br>In genere la responsabilità della gestione dei contenuti per Sites e per Assets è affidata a un unico team. | Immagini utilizzate principalmente per un sito web.<br>PDF che verranno distribuiti tramite un portale interno integrato in AEM Sites. |
| 1 Sites + 1 Assets | Creazione di programmi separati:<br>1 programma solo Sites e 1 programma solo Assets | 1 ambiente di produzione + 1 ambiente di staging, 1 ambiente di sviluppo<br> 1 ambiente di produzione + 1 ambiente di staging, 1 ambiente di sviluppo | Quando molte risorse digitali non supportano direttamente l’implementazione di Sites.<br> In questi casi le risorse presentano diversi stati, compresi i tipi di file RAW e i processi in corso.<br>Un team creativo dedicato gestisce le risorse digitali durante il loro ciclo di vita e prevede flussi di lavoro e cicli di rilascio separati rispetto al team di gestione dei contenuti di Sites. | Le immagini RAW di un servizio fotografico vengono archiviate nel programma Assets e solo poche selezionate verranno utilizzate nell’implementazione di Sites.<br>Molti tipi di file di Creative Cloud, come i file di Photoshop e Illustrator, vengono gestiti in AEM Assets e seguono un proprio flusso di lavoro di approvazione prima della generazione di una risorsa completata.<br>In questi casi, considera l’utilizzo delle [risorse collegate](/help/assets/use-assets-across-connected-assets-instances.md#overview-of-connected-assets). |
| 1 Sites + 1 Sites | Creazione di programmi separati:<br>1 programma solo Sites e 1 programma solo Sites | 1 ambiente di produzione + 1 ambiente di staging, 1 ambiente di sviluppo<br>1 ambiente di produzione + 1 ambiente di staging, 1 ambiente di sviluppo | Per le implementazioni di Sites multi-tenant.<br>In questi casi, è necessario gestire più soluzioni Sites con una propria pianificazione delle versioni e team dedicati di sviluppo e contenuti. | Due marchi di vendita al dettaglio con siti web dedicati e team di sviluppo separati |

>[!NOTE]
>
>I programmi di produzione [possono essere modificati, ma non eliminati.](editing-programs.md)
