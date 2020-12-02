---
title: Replica
description: Distribuzione e risoluzione dei problemi di replica.
translation-type: tm+mt
source-git-commit: abb45225e880f3d08b9d26c29e243037564acef0
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 2%

---


# Replica {#replication}

Adobe Experience Manager utilizza, ad Cloud Service, la funzionalità [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html) per spostare il contenuto in modo che venga replicato in un servizio pipeline eseguito su  Adobe I/O esterno al runtime AEM.

>[!NOTE]
>
>Per ulteriori informazioni, leggere [Distribution](/help/core-concepts/architecture.md#content-distribution).

## Metodi di pubblicazione del contenuto {#methods-of-publishing-content}

### Annullamento/pubblicazione rapida - Annullamento/pubblicazione pianificata {#publish-unpublish}

Queste funzionalità standard AEM per gli autori non cambiano con AEM Cloud Service.

### Tempi di attivazione e disattivazione - Configurazione trigger {#on-and-off-times-trigger-configuration}

Le possibilità aggiuntive di **Ora di attivazione** e **Ora di disattivazione** sono disponibili nella scheda [Base di Proprietà pagina](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic).

Per realizzare la replica automatica, è necessario attivare la **Replica automatica** nella [configurazione OSGi](/help/implementing/deploying/configuring-osgi.md) **Configurazione attivatore automatico**:

![Configurazione attivatore OSGi attivato](/help/operations/assets/replication-on-off-trigger.png)

### Attivazione albero {#tree-activation}

Per eseguire l&#39;attivazione di una struttura ad albero:

1. Dal menu di avvio AEM passare a **Strumenti > Distribuzione > Distribuzione**
2. Selezionare la scheda **forwardPublisher**
3. Una volta nell&#39;interfaccia della console Web di Publisher, **selezionare Distribuisci**

   ![](assets/distribute.png "Distribuisci")
4. Selezionate il percorso nel browser dei percorsi, scegliete di aggiungere un nodo, una struttura ad albero o l&#39;eliminazione come necessario e selezionate **Invia**

## Risoluzione dei problemi {#troubleshooting}

Per risolvere i problemi di replica, andate alle code di replica nell&#39;interfaccia utente Web di AEM Author Service:

1. Dal menu di avvio AEM passare a **Strumenti > Distribuzione > Distribuzione**
2. Selezionare la scheda **forwardPublisher**
   ![](assets/status.png "StatusStatus")
3. Verificare lo stato della coda che deve essere verde
4. È possibile verificare la connessione al servizio di replica
5. Selezionate la scheda **Logs** che mostra la cronologia delle pubblicazioni di contenuto

![](assets/logs.png "LogsLogs")

Se non è stato possibile pubblicare il contenuto, l&#39;intera pubblicazione viene ripristinata da AEM Publish Service.
In tal caso, le code dovrebbero essere riviste per individuare quali elementi hanno causato l&#39;annullamento della pubblicazione. Facendo clic su una coda che mostra uno stato rosso, viene visualizzata la coda con gli elementi in sospeso, da cui è possibile cancellare singoli o tutti gli elementi, se necessario.
