---
title: Replica
description: Replica per la distribuzione e la risoluzione dei problemi.
translation-type: tm+mt
source-git-commit: 8fba31951276d7e0de1f3bd079e42e431edaff4e

---


# Replica {#replication}

Adobe Experience Manager come servizio cloud utilizza la funzionalità [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html) (Distribuzionedi contenuti Sling) per spostare il contenuto in modo che venga replicato in un servizio pipeline eseguito su Adobe I/O al di fuori del runtime AEM.

>[!NOTE]
>
> Per ulteriori informazioni, consulta [Distribuzione](/help/core-concepts/architecture.md#content-distribution) .

## Metodi di pubblicazione dei contenuti {#methods-of-publishing-content}

### Annullamento/Pubblicazione Rapida - Annullamento/Pubblicazione Pianificata {#publish-unpublish}

Queste funzionalità standard di AEM per gli autori non vengono modificate con il servizio AEM Cloud.

### Attivazione albero {#tree-activation}

Per eseguire l&#39;attivazione di una struttura ad albero:

1. Dal menu Start di AEM, andate a **Strumenti > Distribuzione > Distribuzione**
2. Selezionare la scheda **forwardPublisher**
3. Nell&#39;interfaccia della console Web di Publisher, **selezionare Distribuisci**
   ![](assets/distribute.png "Distribuisci")
4. Selezionate il percorso nel browser dei percorsi, scegliete di aggiungere un nodo, una struttura ad albero o l’eliminazione come necessario e selezionate **Invia**

## Risoluzione dei problemi {#troubleshooting}

Per risolvere i problemi di replica, andate alle code di replica nell&#39;interfaccia utente Web di AEM Author Service:

1. Dal menu Start di AEM, andate a **Strumenti > Distribuzione > Distribuzione**
2. Selezionare la scheda **forwardPublisher**
   ![](assets/status.png "StatusStatus")
3. Verificare lo stato della coda che deve essere verde
4. È possibile verificare la connessione al servizio di replica
5. Selezionate la scheda **Registri** che mostra la cronologia delle pubblicazioni di contenuto

![](assets/logs.png "LogsLogs")

Se non è stato possibile pubblicare il contenuto, l&#39;intera pubblicazione viene ripristinata da AEM Publish Service.
In tal caso, le code dovrebbero essere riviste per individuare quali elementi hanno causato l&#39;annullamento della pubblicazione. Facendo clic su una coda che mostra uno stato rosso, viene visualizzata la coda con gli elementi in sospeso, da cui è possibile cancellare singoli o tutti gli elementi, se necessario.
