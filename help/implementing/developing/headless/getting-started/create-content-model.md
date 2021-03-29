---
title: Guida rapida alla creazione di modelli di frammenti di contenuto headless
description: Definisci la struttura del contenuto che creerai e distribuirai utilizzando AEM funzionalità headless utilizzando Modelli per frammenti di contenuto .
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---


# Guida rapida alla creazione di modelli di frammenti di contenuto senza intestazione {#creating-content-fragment-models}

Definisci la struttura del contenuto che creerai e distribuirai utilizzando AEM funzionalità headless utilizzando Modelli per frammenti di contenuto .

## Cosa sono i modelli di frammento di contenuto? {#what-are-content-fragment-models}

[Dopo aver creato una configurazione, ](create-configuration.md) puoi utilizzarla per creare modelli di frammenti di contenuto.

I modelli per frammenti di contenuto definiscono la struttura dei dati e del contenuto che verranno creati e gestiti in AEM. Servono come una sorta di impalcatura per i vostri contenuti. Quando scegli di creare un contenuto, gli autori selezionano i modelli di frammento di contenuto da te definiti, che li guida nella creazione di contenuti.

## Come creare un modello di frammento di contenuto {#how-to-create-a-content-fragment-model}

Un architetto dell&#39;informazione eseguirà queste attività solo sporadicamente quando sono necessari nuovi modelli. Ai fini di questa guida introduttiva, è necessario creare un solo modello.

1. Accedi a AEM come Cloud Service e dal menu principale seleziona **Strumenti -> Risorse -> Modelli di frammento di contenuto**.
1. Tocca o fai clic sulla cartella creata creando la configurazione.

   ![La cartella dei modelli](../assets/models-folder.png)
1. Tocca o fai clic su **Crea**.
1. Fornisci un **Titolo modello**, **Tag** e **Descrizione**. È inoltre possibile selezionare/deselezionare **Abilita modello** per controllare se il modello è immediatamente abilitato al momento della creazione.

   ![Creare un modello](../assets/models-create.png)
1. Nella finestra di conferma, tocca o fai clic su **Apri** per configurare il modello.

   ![Finestra di conferma](../assets/models-confirmation.png)
1. Utilizzando l’ **Editor modello frammento di contenuto**, crea il modello di frammento di contenuto trascinando i campi dalla colonna **Tipi di dati**.

   ![Trascinare i campi](../assets/models-drag-and-drop.png)

1. Una volta inserito un campo, è necessario configurarne le proprietà. L’editor passerà automaticamente alla scheda **Proprietà** per il campo aggiunto in cui è possibile fornire i campi obbligatori.

   ![Configurare le proprietà](../assets/models-configure-properties.png)
1. Al termine della creazione del modello, tocca o fai clic su **Salva**. Il modello appena creato viene salvato in modalità **Bozza** .

   ![Modello in modalità bozza](../assets/models-draft.png)
1. Il modello deve essere abilitato per poterlo utilizzare (se non è già abilitato). Seleziona il modello appena creato, quindi tocca o fai clic su **Abilita**.

   ![Abilitazione del modello](../assets/models-enable.png)
1. Conferma l’abilitazione del modello toccando o facendo clic su **Abilita** nella finestra di dialogo di conferma.

   ![Attivare la finestra di dialogo di conferma](../assets/models-enabling.png)
1. Il modello è ora abilitato e pronto per essere utilizzato.

   ![Modello abilitato](../assets/models-enabled.png)

L’ **Editor modello frammento di contenuto** supporta molti tipi di dati diversi, ad esempio campi di testo semplici, riferimenti alle risorse, riferimenti ad altri modelli e dati JSON.

Puoi creare più modelli. I modelli possono fare riferimento ad altri frammenti di contenuto. Utilizza [configurazioni](create-configuration.md) per organizzare i modelli.

## Passaggi successivi {#next-steps}

Dopo aver definito le strutture dei frammenti di contenuto mediante la creazione di modelli, puoi passare alla terza parte della guida introduttiva e [creare cartelle in cui memorizzare i frammenti stessi.](create-assets-folder.md)

>[!TIP]
>
>Per informazioni complete sui modelli di frammenti di contenuto, consulta la [documentazione sui modelli di frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
