---
title: Guida rapida alla creazione di frammenti di contenuto senza titolo
description: I frammenti di contenuto consentono di progettare, creare, curare e utilizzare contenuti indipendenti dalla pagina che possono essere distribuiti senza problemi da AEM.
translation-type: tm+mt
source-git-commit: 712a99095494ab333cf0ebb2ac9fffe3f5945f3b
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 1%

---


# Guida rapida alla creazione di frammenti di contenuto senza titolo {#creating-content-fragments}

I frammenti di contenuto consentono di progettare, creare, curare e utilizzare contenuti indipendenti dalla pagina che possono essere distribuiti senza problemi da AEM.

## Che cosa sono i frammenti di contenuto? {#what-are-content-fragments}

[Dopo aver creato una ](create-assets-folder.md) cartella delle risorse in cui memorizzare i frammenti di contenuto, è ora possibile creare i frammenti.

I frammenti di contenuto consentono di progettare, creare, curare e pubblicare contenuti indipendenti dalla pagina. Consentono di preparare i contenuti pronti per l’uso in più posizioni e su più canali.

I frammenti di contenuto contengono contenuto strutturato e possono essere inviati in formato JSON.

## Come creare un frammento di contenuto {#how-to-create-a-content-fragment}

Gli autori dei contenuti creeranno un numero qualsiasi di frammenti di contenuto per rappresentare il contenuto creato. Questo sarà il loro compito principale in AEM. Ai fini di questa guida introduttiva, sarà sufficiente crearne una.

1. Accedi al AEM come Cloud Service e dal menu principale seleziona **Navigazione -> Risorse**.
1. Toccate o fate clic sulla [cartella creata in precedenza.](create-assets-folder.md)
1. Toccate o fate clic su **Crea -> Frammento di contenuto**.
1. La creazione di un frammento di contenuto viene presentata come procedura guidata in due passaggi. Selezionare innanzitutto il modello da utilizzare per creare il frammento di contenuto e toccare o fare clic su **Avanti**.
   * I modelli disponibili dipendono dalla [**Configurazione cloud** definita per la cartella delle risorse](create-assets-folder.md) in cui si sta creando il frammento di contenuto.
   * Se ricevete il messaggio `We could not find any models`, controllate la configurazione della cartella delle risorse.

   ![Seleziona modello frammento di contenuto](../assets/content-fragment-model-select.png)
1. Specificare un **Titolo**, **Descrizione** e **Tag** a seconda delle necessità, quindi toccare o fare clic su **Crea**.

   ![Crea frammento di contenuto](../assets/content-fragment-create.png)
1. Toccate o fate clic su **Apri** nella finestra di conferma.

   ![Conferma creata per frammento di contenuto](../assets/content-fragment-confirmation.png)
1. Fornire i dettagli del frammento di contenuto nell&#39;Editor frammento di contenuto.

   ![Editor frammento di contenuto ](../assets/content-fragment-edit.png)
1. Toccate o fate clic su **Salva**.

I frammenti di contenuto possono fare riferimento ad altri frammenti di contenuto, consentendo se necessario una struttura di contenuto nidificata.

I frammenti di contenuto possono fare riferimento ad altre risorse in AEM. [Queste risorse devono essere memorizzate in ](/help/assets/manage-digital-assets.md) AEM prima di creare un frammento di contenuto di riferimento.

## Passaggi successivi {#next-steps}

Dopo aver creato un frammento di contenuto, puoi passare alla parte finale della guida introduttiva e [creare richieste API per accedere e distribuire frammenti di contenuto.](create-api-request.md)

>!![TIP]
Per informazioni complete sulla gestione dei frammenti di contenuto, consultare la [documentazione relativa ai frammenti di contenuto](/help/assets/content-fragments/content-fragments.md)
