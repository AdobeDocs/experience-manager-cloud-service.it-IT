---
title: Creazione di una configurazione - Configurazione headless
description: Crea una configurazione come primo passo per iniziare a utilizzare headless in AEM as a Cloud Service.
exl-id: 48801599-f279-4e55-8033-9c418d2af5bb
source-git-commit: e81b852dc90e3cc5abc8b9f218f48d0fc1cc66eb
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 3%

---

# Creazione di una configurazione - Configurazione headless {#creating-configuration}

Come primo passo per iniziare a utilizzare headless in AEM as a Cloud Service, devi creare una configurazione.

## Cos&#39;è una configurazione? {#what-is-a-configuration}

Il browser di configurazione fornisce un’API di configurazione generica, una struttura del contenuto e un meccanismo di risoluzione per le configurazioni in AEM.

Nel contesto della gestione dei contenuti headless in AEM, considera una configurazione come luogo di lavoro all’interno di AEM dove puoi creare i modelli di contenuto, che definiscono la struttura dei contenuti e dei frammenti di contenuto futuri. Puoi avere più configurazioni per separare questi modelli.

Se hai familiarità con [modelli di pagina in un’implementazione AEM a stack completo,](/help/sites-cloud/authoring/features/templates.md) l’utilizzo delle configurazioni per la gestione dei modelli di contenuto è simile.

## Come creare una configurazione {#how-to-create-a-configuration}

Un amministratore deve creare una configurazione solo una volta oppure molto raramente quando è necessaria una nuova area di lavoro per organizzare i modelli di contenuto. Ai fini di questa guida introduttiva, è sufficiente creare una sola configurazione.

1. Accedi AEM as a Cloud Service e seleziona dal menu principale **Strumenti -> Generale -> Browser di configurazione**.
1. Fornisci un **Titolo** e **Nome** per la configurazione.
   * La **Titolo** deve essere descrittivo.
   * La **Nome** diventerà il nome del nodo nel repository.
      * Viene generato automaticamente in base al titolo e viene regolato in base a [AEM convenzioni di denominazione.](/help/implementing/developing/introduction/naming-conventions.md)
      * Può essere regolato se necessario.
1. Controlla le seguenti opzioni:
   * **Modelli per frammenti di contenuto**
   * **Query persistenti GraphQL**

   ![Crea configurazione](../assets/create-configuration.png)

1. Tocca o fai clic su **Crea**

Se necessario, puoi creare più configurazioni. È inoltre possibile nidificare le configurazioni.

>[!NOTE]
>
>Opzioni di configurazione oltre a **Modelli per frammenti di contenuto** e **Query persistenti GraphQL** può essere necessario in base ai requisiti di implementazione.

## Passaggi successivi {#next-steps}

Utilizzando questa configurazione, ora puoi passare alla seconda parte della guida introduttiva e [creare modelli di frammenti di contenuto.](create-content-model.md)

>[!TIP]
>
>Per informazioni complete sul Browser di configurazione, [consulta la documentazione del browser di configurazione .](/help/implementing/developing/introduction/configurations.md)
