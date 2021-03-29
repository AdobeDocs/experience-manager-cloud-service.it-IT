---
title: Guida rapida alla creazione di un headless di configurazione
description: Crea una configurazione come primo passo per iniziare a utilizzare headless in AEM come Cloud Service.
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 2%

---


# Guida rapida alla creazione di un titolo di configurazione {#creating-configuration}

Come primo passo per iniziare a utilizzare senza testa in AEM come Cloud Service, devi creare una configurazione.

## Cos&#39;è una configurazione? {#what-is-a-configuration}

Il browser di configurazione fornisce un’API di configurazione generica, una struttura del contenuto e un meccanismo di risoluzione per le configurazioni in AEM.

Nel contesto della gestione dei contenuti headless in AEM, considera una configurazione come luogo di lavoro all’interno di AEM dove puoi creare i modelli di contenuto, che definiscono la struttura dei contenuti e dei frammenti di contenuto futuri. Puoi avere più configurazioni per separare questi modelli.

Se hai familiarità con i modelli di pagina [in un&#39;implementazione AEM a stack completo,](/help/sites-cloud/authoring/features/templates.md) l&#39;utilizzo delle configurazioni per la gestione dei modelli di contenuto è simile.

## Come creare una configurazione {#how-to-create-a-configuration}

Un amministratore deve creare una configurazione solo una volta oppure molto raramente quando è necessaria una nuova area di lavoro per organizzare i modelli di contenuto. Ai fini di questa guida introduttiva, è sufficiente creare una sola configurazione.

1. Accedi a AEM come Cloud Service e dal menu principale seleziona **Strumenti -> Generale -> Browser di configurazione**.
1. Specifica un **titolo** e un **nome** per la configurazione.
   * Il **Titolo** deve essere descrittivo.
   * Il **Nome** diventerà il nome del nodo nel repository.
      * Verrà generato automaticamente in base al titolo e verrà regolato in base alle convenzioni di denominazione [AEM.](/help/implementing/developing/introduction/naming-conventions.md)
      * Può essere regolato se necessario.
1. Controlla le seguenti opzioni:
   * **Modelli per frammenti di contenuto**
   * **Query persistenti GraphQL**

   ![Crea configurazione](../assets/create-configuration.png)

1. Tocca o fai clic su **Crea**

Se necessario, puoi creare più configurazioni. È inoltre possibile nidificare le configurazioni.

>[!NOTE]
>
>Le opzioni di configurazione oltre a **Modelli di frammento di contenuto** e **Query persistenti GraphQL** potrebbero essere necessarie a seconda dei requisiti di implementazione.

## Passaggi successivi {#next-steps}

Utilizzando questa configurazione, ora puoi passare alla seconda parte della guida introduttiva e [creare modelli di frammenti di contenuto.](create-content-model.md)

>[!TIP]
>
>Per informazioni complete sul Browser configurazioni, [vedere la documentazione del Browser configurazioni.](/help/implementing/developing/introduction/configurations.md)
