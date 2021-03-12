---
title: 'Introduzione ai programmi di produzione '
description: 'Introduzione ai programmi di produzione '
translation-type: tm+mt
source-git-commit: a8101b4f25053454fbd0adc7785f40bfc3a6cb31
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---


# Introduzione ai programmi di produzione {#production-programs}

Un programma *Produzione* è destinato a un utente che ha dimestichezza con AEM e Cloud Manager ed è pronto per iniziare a scrivere, creare e testare il codice allo scopo di distribuirlo in Produzione.

>[!NOTE]
>Non potrai eliminare un programma Produzione.

Una procedura guidata di creazione del programma guiderà l’utente a effettuare le selezioni, a seconda dell’obiettivo dell’utente nella creazione del programma. In base alle adesioni non utilizzate della soluzione disponibili per il cliente o l’organizzazione specifici, l’utente ha il controllo su come mappare le adesioni disponibili (non utilizzate) ai programmi Cloud Manager.

## Considerazioni sulla creazione di programmi {#program-creation-considerations}

La tabella seguente descrive gli scenari comuni da prendere in considerazione durante la creazione di programmi in Cloud Manager:

| Autorizzazioni per soluzioni non utilizzate disponibili nell&#39;organizzazione | Opzioni del programma | Contenuto | Quando utilizzare e altre considerazioni |
|--- |--- |--- |--- |
| 1 soluzione Sites | Crea un programma solo per 1 sito | 1 Produzione + 1 fase, 1 sviluppo | ND |
| 1 soluzione Assets | Crea 1 solo programma Assets | 1 Produzione + 1 fase, 1 sviluppo | ND |
| 1 Sites +1 Assets | Crea un programma: 1 Programma Sites &amp; Assets | 1 Produzione + 1 fase, 2 sviluppo | La maggior parte delle risorse digitali viene utilizzata per supportare l’implementazione di Sites. La maggior parte delle risorse digitali è in uno stato finito, pronta per essere utilizzata per le esperienze cross-channel tramite Sites. In genere, un singolo team è responsabile della gestione dei contenuti sia per Sites che per Assets. **Esempi** comuni: Immagini utilizzate principalmente per un sito web. PDF che verranno distribuiti tramite un portale interno integrato in AEM Sites. |
| 1 Sites +1 Assets | Creare programmi separati: 1 solo programma di Sites e 1 solo programma di Assets | 1 Produzione + 1 fase, 1 sviluppo 1 produzione + 1 fase, 1 sviluppo | Molte risorse digitali non supportano direttamente l’implementazione dei siti. Le risorse gestite sono in vari stati, inclusi i tipi di file non elaborati e sono in corso di elaborazione. Un team creativo dedicato gestisce le risorse digitali attraverso il proprio ciclo di vita e dispone di flussi di lavoro e cicli di rilascio separati rispetto al team di gestione dei contenuti di Sites. *Esempi* comuni: Le immagini non elaborate provenienti da un servizio fotografico sono memorizzate nel programma Assets e solo alcune di esse saranno utilizzate nell’implementazione di Sites. Un gran numero di tipi di file di Creative Cloud, come Photoshop e Illustrator, vengono gestiti in AEM Assets e passano attraverso il proprio flusso di lavoro di approvazione prima che venga generata una risorsa finita. Funzionalità da sfruttare: [Risorse collegate](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html?lang=en#overview-of-connected-assets) |
| 1 siti + 1 siti | Creare programmi separati: 1 Programma solo siti e 1 programma solo siti | 1 Produzione + 1 fase, 1 sviluppo<br>1 produzione + 1 fase, 1 sviluppo | Implementazioni di siti multi-tenant. Più siti con la propria pianificazione delle versioni e team dedicati di sviluppo e contenuti. *Esempi* comuni: Due marchi retail con siti web dedicati e team di sviluppo separati |


