---
title: Indicizzazione dopo la migrazione del contenuto
description: Scopri come il processo di migrazione indicizzerà i contenuti acquisiti nell’istanza del Cloud Service di destinazione.
exl-id: a13d5df4-b351-410a-9336-1b34a8af21b6
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 6%

---

# Indicizzazione dopo la migrazione del contenuto {#Indexing-content}

## Indicizzazione {#aem-indexing-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_indexing"
>title="Indicizzazione dei contenuti"
>abstract="Per indicizzazione di AEM si intende l’indicizzazione dei contenuti nell’istanza di Cloud Service dopo la migrazione di contenuti. L’indicizzazione è necessaria per supportare la ricerca di contenuti in tale istanza."

Una volta che Cloud Acceleration Manager ha completato l’acquisizione del contenuto nell’istanza di Cloud Service, è pronto per essere utilizzato. Inizialmente il contenuto non è indicizzato, probabilmente causando un ambiente instabile in cui sono prevedibili problemi quali contenuto non ricercabile e prestazioni ridotte.
Per prestazioni ottimali sull’istanza, il processo di migrazione avvierà automaticamente l’indicizzazione del contenuto. Non è necessario eseguire alcuna operazione, ad eccezione del monitoraggio dell’avanzamento dell’indicizzazione.

> Per informazioni su come avviare un’acquisizione, consulta [Acquisizione di contenuti nel Cloud Service](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md).

I passaggi seguenti mostrano il flusso generale che ci si aspetta di visualizzare nell’interfaccia utente durante l’indicizzazione. Alcune etichette forniscono un contesto utile nelle descrizioni, quindi accertati di passare il cursore sugli elementi per ulteriori informazioni sullo stato di indicizzazione corrente.

Per iniziare, passa a Cloud Acceleration Manager. Fai clic sulla scheda del progetto e quindi sulla scheda Content Transfer (Trasferimento contenuti). Accedi a **Processi di acquisizione**
e visualizzare i processi elencati.

>[!NOTE]
>Puoi visualizzare o scaricare i registri di indicizzazione utilizzando le azioni del processo di acquisizione dal menu a discesa .... I registri saranno disponibili nel
> Sezione Azioni del &#39;Registro di indicizzazione&#39;, al termine del processo di indicizzazione

### In sospeso

In questo modo verrà visualizzata la riga del processo di acquisizione quando l’acquisizione è in esecuzione, prima che il processo di indicizzazione sia stato avviato. Non è richiesta alcuna azione da parte dell’utente. Se l’acquisizione non riesce per qualsiasi motivo, la coda del processo di indicizzazione verrà annullata e non verrà avviata.

![immagine](/help/journey-migration/content-transfer-tool/assets-indexing/pending.png)

### In esecuzione

Quando l’acquisizione ha esito positivo, il processo di indicizzazione viene avviato automaticamente. Nella riga del processo di acquisizione viene visualizzata un’icona di avanzamento per lo stato di indicizzazione AEM. È possibile aprire la finestra di dialogo Durata per visualizzare l&#39;avanzamento del processo.

![immagine](/help/journey-migration/content-transfer-tool/assets-indexing/running.png)

### Completa

Quando il processo di indicizzazione ha esito positivo, l’istanza è pronta per essere utilizzata con prestazioni ottimali. A questo punto, i registri del processo di indicizzazione sono disponibili per la visualizzazione o il download per esaminarli.

![immagine](/help/journey-migration/content-transfer-tool/assets-indexing/complete.png)

### Errori

L’indicizzazione dell’istanza del Cloud Service di destinazione avrà molto probabilmente esito positivo. In alcuni casi, può non riuscire e la riga del processo di acquisizione viene visualizzata come segue. In tutti i casi, è possibile individuare alcuni dettagli dell&#39;errore passando sopra lo stato dell&#39;errore e potrebbero essere disponibili ulteriori informazioni per determinare i passaggi successivi. A questo punto, i registri del processo di indicizzazione sono disponibili per la visualizzazione o il download per individuare l’origine dell’errore. Se il passaggio successivo non è chiaro, contatta il supporto Adobe con i dettagli dell’acquisizione e del registro di indicizzazione.

![immagine](/help/journey-migration/content-transfer-tool/assets-indexing/failed.png)

## Passaggio successivo {#whats-next}

Una volta indicizzata l’istanza del servizio cloud di destinazione, puoi visualizzare i registri dei processi di indicizzazione e cercare dettagli ed errori.

Migrazione completata. È possibile avviare il test e la convalida dell’istanza del servizio cloud di destinazione.
