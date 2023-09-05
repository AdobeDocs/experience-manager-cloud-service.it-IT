---
title: 'Creazione di frammenti di contenuto: configurazione headless'
description: Scopri come utilizzare i Frammenti di contenuto AEM per progettare, creare, curare e utilizzare contenuti indipendenti dalla pagina per la consegna headless.
exl-id: a227ae2c-f710-4968-8a00-bfe48aa66145
source-git-commit: 7d09cafc4f8518fee185d3f9efc76c33ec20f9a3
workflow-type: ht
source-wordcount: '347'
ht-degree: 100%

---

# Creazione di frammenti di contenuto: configurazione headless {#creating-content-fragments}

Scopri come utilizzare i Frammenti di contenuto AEM per progettare, creare, curare e utilizzare contenuti indipendenti dalla pagina per la consegna headless.

## Cosa sono i Frammenti di contenuto? {#what-are-content-fragments}

[Ora che hai creato una cartella risorse](create-assets-folder.md) nella quale puoi archiviare i Frammenti di contenuto, puoi cominciare a crearli.

I Frammenti di contenuto ti consentono di progettare, creare, curare e pubblicare contenuti indipendenti dalle pagine. Consentono di preparare contenuti pronti per l’uso in più posizioni e su più canali.

I Frammenti di contenuto contengono contenuto strutturato e possono essere consegnati in formato JSON.

## Come creare un Frammento di contenuto {#how-to-create-a-content-fragment}

Gli autori dei contenuti creano un certo numero di Frammenti di contenuto per rappresentare il contenuto creato. Questa sarà l’attività principale in AEM. Ai fini di questa guida introduttiva, ne creeremo uno.

1. Accedi ad AEM as a Cloud Service, quindi dal menu principale seleziona **Navigazione** -> **Frammenti di contenuto**.

1. Tocca o fai clic sulla [cartella creata in precedenza.](create-assets-folder.md)
1. Tocca o fai clic su **Crea**.
1. La creazione di un frammento di contenuto viene presentata come una finestra di dialogo.
Seleziona la posizione e il modello da utilizzare per creare il frammento di contenuto.

   * I modelli disponibili dipendono dalla [**configurazione cloud** definita per la cartella risorse](create-assets-folder.md) in cui stai creando il frammento di contenuto.
   * Se il modello non è disponibile, controlla la configurazione della cartella delle risorse.

   Aggiungi Titolo, Nome e, se necessario, Descrizione.

   ![Finestra di dialogo Crea nuovo frammento di contenuto](/help/sites-cloud/administering/content-fragments/assets/cfc-console-create.png)

1. Tocca o fai clic su **Crea** o **Crea e apri**.

I Frammenti di contenuto possono fare riferimento ad altri Frammenti di contenuto, consentendo se necessario una struttura di contenuto nidificata.

I Frammenti di contenuto possono fare riferimento ad altre risorse in AEM. [Queste risorse devono essere memorizzate in AEM](/help/assets/manage-digital-assets.md) prima di creare un riferimento in un Frammento di contenuto.

## Passaggi successivi {#next-steps}

Dopo aver creato un Frammento di contenuto, puoi passare alla parte finale della guida introduttiva e [creare richieste API per accedere e distribuire frammenti di contenuto.](create-api-request.md)

>[!TIP]
>
>Per informazioni complete sulla gestione dei Frammenti di contenuto, consulta la sezione [Documentazione sui Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/overview.md).
