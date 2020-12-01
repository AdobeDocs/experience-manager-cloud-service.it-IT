---
title: Creazione di una guida rapida alla configurazione senza titolo
description: Come primo passo per iniziare a utilizzare il AEM headless come Cloud Service, è necessario creare una configurazione.
translation-type: tm+mt
source-git-commit: 7ed96dc0da879800d731983a0399b4f4fb3d7d41
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 2%

---


# Creazione di una guida rapida all&#39;avvio headless di configurazione {#creating-configuration}

Come primo passo per iniziare a utilizzare il AEM headless come Cloud Service, è necessario creare una configurazione.

## Cos&#39;è una configurazione? {#what-is-a-configuration}

Il browser di configurazione fornisce un API di configurazione generica, una struttura di contenuto, un meccanismo di risoluzione per le configurazioni in AEM.

Nel contesto della gestione dei contenuti headless in AEM, considera una configurazione come luogo di lavoro all&#39;interno AEM quale è possibile creare i modelli di contenuto, che definiscono la struttura dei futuri frammenti di contenuto e di contenuto. Potete avere più configurazioni per separare questi modelli.

Se avete familiarità con i modelli di pagina [in un&#39;implementazione AEM a stack completo,](/help/sites-cloud/authoring/features/templates.md) l&#39;utilizzo delle configurazioni per la gestione dei modelli di contenuto è simile.

## Come creare una configurazione {#how-to-create-a-configuration}

Un amministratore dovrebbe creare una configurazione solo una volta, o molto raramente quando è necessaria una nuova area di lavoro per organizzare i modelli di contenuto. Ai fini di questa guida introduttiva, è sufficiente creare una sola configurazione.

1. Accedete AEM come Cloud Service e dal menu principale selezionate **Strumenti -> Generale -> Browser di configurazione**.
1. Specificare un **Titolo** e un **Nome** per la configurazione.
   * Il **Titolo** deve essere descrittivo.
   * Il **Nome** diventerà il nome del nodo nella directory archivio.
      * Verrà generato automaticamente in base al titolo e verrà modificato in base alle convenzioni di denominazione [AEM.](/help/implementing/developing/introduction/naming-conventions.md)
      * Può essere regolato se necessario.
1. Selezionare le opzioni seguenti:
   * **Modelli per frammenti di contenuto**
   * **GraphQL - Query persistenti**

   ![Crea configurazione](../assets/create-configuration.png)

1. Tocca o fai clic su **Crea**

Se necessario, potete creare più configurazioni. È inoltre possibile nidificare le configurazioni.

>!![NOTE]
Le opzioni di configurazione oltre a **Modelli di frammenti di contenuto** e **GraphQL Persistent Query** potrebbero essere necessarie a seconda dei requisiti di implementazione.

## Passaggi successivi {#next-steps}

Utilizzando questa configurazione, ora puoi passare alla seconda parte della guida introduttiva e [creare modelli di frammenti di contenuto.](create-content-model.md)

>!![TIP]
Per informazioni complete sul browser di configurazione, consultare la documentazione del browser di configurazione.[](/help/implementing/developing/introduction/configurations.md)
