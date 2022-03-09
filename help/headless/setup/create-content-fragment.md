---
title: 'Creazione di frammenti di contenuto: configurazione headless'
description: Scopri come utilizzare i Frammenti di contenuto AEM per progettare, creare, curare e utilizzare contenuti indipendenti dalla pagina per la consegna headless.
exl-id: a227ae2c-f710-4968-8a00-bfe48aa66145
source-git-commit: d35b60810a1624390d3d9c82c2a364140ea37536
workflow-type: ht
source-wordcount: '388'
ht-degree: 100%

---

# Creazione di frammenti di contenuto: configurazione headless {#creating-content-fragments}

Scopri come utilizzare i Frammenti di contenuto AEM per progettare, creare, curare e utilizzare contenuti indipendenti dalla pagina per la consegna headless.

## Cosa sono i Frammenti di contenuto? {#what-are-content-fragments}

[Ora che hai creato una cartella risorse](create-assets-folder.md) nella quale puoi archiviare i Frammenti di contenuto, puoi cominciare a crearli.

I Frammenti di contenuto ti consentono di progettare, creare, curare e pubblicare contenuti indipendenti dalle pagine. Consentono di preparare contenuti pronti per l’uso in più posizioni e su più canali.

I Frammenti di contenuto contengono contenuto strutturato e possono essere consegnati in formato JSON.

## Come creare un Frammento di contenuto {#how-to-create-a-content-fragment}

Gli autori dei contenuti creano un certo numero di Frammenti di contenuto per rappresentare il contenuto creato. Questa sarà l’attività principale dei Frammenti di contenuto in AEM. Ai fini di questa guida introduttiva, ne creeremo uno.

1. Accedi ad AEM as a Cloud Service e seleziona dal menu principale **Navigazione -> Risorse**.
1. Tocca o fai clic sulla [cartella creata in precedenza.](create-assets-folder.md)
1. Tocca o fai clic su **Crea -> Frammento di contenuto**.
1. La creazione di un Frammento di contenuto viene presentata come una procedura guidata in due passaggi. Seleziona innanzitutto il modello da utilizzare per creare il frammento di contenuto e tocca o fai clic su **Successivo**.
   * I modelli disponibili dipendono dalla [**configurazione cloud** definita per la cartella risorse](create-assets-folder.md) in cui stai creando il frammento di contenuto.
   * Se ricevi il messaggio `We could not find any models`, controlla la configurazione della cartella delle risorse.

   ![Seleziona modello di Frammento di contenuto](../assets/content-fragment-model-select.png)
1. Fornisci **Titolo**, **Descrizione** e **Tag** secondo necessità, quindi tocca o fai clic su **Crea**.

   ![Creare Frammento di contenuto](../assets/content-fragment-create.png)
1. Tocca o fai clic su **Apri** nella finestra di conferma.

   ![Conferma di creazione del Frammento di contenuto](../assets/content-fragment-confirmation.png)
1. Fornisci i dettagli del Frammento di contenuto nell’Editor frammento di contenuto.

   ![Editor frammento di contenuto](../assets/content-fragment-edit.png)
1. Tocca o fai clic su **Salva** o **Salva e chiudi**.

I Frammenti di contenuto possono fare riferimento ad altri Frammenti di contenuto, consentendo se necessario una struttura di contenuto nidificata.

I Frammenti di contenuto possono fare riferimento ad altre risorse in AEM. [Queste risorse devono essere memorizzate in AEM](/help/assets/manage-digital-assets.md) prima di creare un riferimento in un Frammento di contenuto.

## Passaggi successivi {#next-steps}

Dopo aver creato un Frammento di contenuto, puoi passare alla parte finale della guida introduttiva e [creare richieste API per accedere e distribuire frammenti di contenuto.](create-api-request.md)

>[!TIP]
>
>Per informazioni complete sulla gestione dei Frammenti di contenuto, consulta la sezione [Documentazione sui Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md)
