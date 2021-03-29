---
title: Guida rapida alla creazione di frammenti di contenuto senza intestazione
description: Scopri come utilizzare AEM frammenti di contenuto per progettare, creare, curare e utilizzare contenuti indipendenti dalla pagina per la distribuzione headless.
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 1%

---


# Guida rapida alla creazione di frammenti di contenuto senza intestazione {#creating-content-fragments}

Scopri come utilizzare AEM frammenti di contenuto per progettare, creare, curare e utilizzare contenuti indipendenti dalla pagina per la distribuzione headless.

## Cosa sono i frammenti di contenuto? {#what-are-content-fragments}

[Dopo aver creato una ](create-assets-folder.md) cartella risorse in cui memorizzare i frammenti di contenuto, ora puoi creare i frammenti.

I frammenti di contenuto consentono di progettare, creare, curare e pubblicare contenuti indipendenti dalla pagina. Consentono di preparare i contenuti pronti per l’uso in più posizioni e su più canali.

I frammenti di contenuto contengono contenuto strutturato e possono essere consegnati in formato JSON.

## Come creare un frammento di contenuto {#how-to-create-a-content-fragment}

Gli autori dei contenuti creeranno un numero qualsiasi di frammenti di contenuto per rappresentare il contenuto creato. Questo sarà il loro compito principale in AEM. Ai fini di questa guida introduttiva, è sufficiente crearne una.

1. Accedi a AEM come Cloud Service e dal menu principale seleziona **Navigazione -> Risorse**.
1. Tocca o fai clic sulla cartella [creata in precedenza.](create-assets-folder.md)
1. Tocca o fai clic su **Crea -> Frammento di contenuto**.
1. La creazione di un frammento di contenuto viene presentata come una procedura guidata in due passaggi. Seleziona innanzitutto il modello da utilizzare per creare il frammento di contenuto e tocca o fai clic su **Avanti**.
   * I modelli disponibili dipendono dalla [**Configurazione cloud** definita per la cartella delle risorse](create-assets-folder.md) in cui si sta creando il frammento di contenuto.
   * Se ricevi il messaggio `We could not find any models`, controlla la configurazione della cartella delle risorse.

   ![Seleziona modello frammento di contenuto](../assets/content-fragment-model-select.png)
1. Fornisci un **Titolo**, **Descrizione** e **Tag** a seconda delle necessità e tocca o fai clic su **Crea**.

   ![Crea frammento di contenuto](../assets/content-fragment-create.png)
1. Tocca o fai clic su **Apri** nella finestra di conferma.

   ![Conferma creata dal frammento di contenuto](../assets/content-fragment-confirmation.png)
1. Fornisci i dettagli del frammento di contenuto nell’Editor frammento di contenuto.

   ![Editor frammento di contenuto ](../assets/content-fragment-edit.png)
1. Tocca o fai clic su **Salva e chiudi**.

I frammenti di contenuto possono fare riferimento ad altri frammenti di contenuto, consentendo se necessario una struttura di contenuto nidificata.

I frammenti di contenuto possono fare riferimento ad altre risorse in AEM. [Queste risorse devono essere memorizzate in ](/help/assets/manage-digital-assets.md) AEM prima di creare un frammento di contenuto di riferimento.

## Passaggi successivi {#next-steps}

Dopo aver creato un frammento di contenuto, puoi passare alla parte finale della guida introduttiva e [creare richieste API per accedere e distribuire frammenti di contenuto.](create-api-request.md)

>[!TIP]
>
>Per informazioni complete sulla gestione dei frammenti di contenuto, consulta la [documentazione sui frammenti di contenuto](/help/assets/content-fragments/content-fragments.md)
