---
title: Guida rapida alla creazione di una cartella Assets Headless
description: Utilizza AEM modelli di frammenti di contenuto per definire la struttura dei frammenti di contenuto, la base del contenuto headless.
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---


# Guida rapida alla creazione di cartelle di risorse headless {#creating-an-assets-folder}

Utilizza AEM modelli di frammenti di contenuto per definire la struttura dei frammenti di contenuto, la base del contenuto headless. I frammenti di contenuto vengono quindi memorizzati nelle cartelle delle risorse.

##  Cos’è una cartella di risorse? {#what-is-an-assets-folder}

[Dopo aver creato ](create-content-model.md) modelli per frammenti di contenuto che definiscono la struttura desiderata per i futuri frammenti di contenuto, è probabile che si sia entusiasti di creare alcuni frammenti.

Tuttavia, dovrai innanzitutto creare una cartella di risorse in cui memorizzarle.

Le cartelle delle risorse vengono utilizzate per [organizzare le risorse di contenuto tradizionale](/help/assets/manage-digital-assets.md) come immagini e video, nonché per i frammenti di contenuto.

## Come creare una cartella di risorse {#how-to-create-an-assets-folder}

Un amministratore deve creare le cartelle solo occasionalmente per organizzare i contenuti durante la creazione. Ai fini di questa guida introduttiva, è sufficiente creare una sola cartella.

1. Accedi a AEM come Cloud Service e dal menu principale seleziona **Navigazione -> Risorse -> File**.
1. Tocca o fai clic su **Crea -> Cartella**.
1. Fornisci un **Titolo** e un **Nome** per la cartella.
   * Il **Titolo** deve essere descrittivo.
   * Il **Nome** diventerà il nome del nodo nel repository.
      * Verrà generato automaticamente in base al titolo e verrà regolato in base alle convenzioni di denominazione [AEM.](/help/implementing/developing/introduction/naming-conventions.md)
      * Può essere regolato se necessario.

   ![Crea cartella](../assets/assets-folder-create.png)
1. Seleziona la cartella appena creata e quindi seleziona **Proprietà** dalla barra degli strumenti (oppure utilizza la scelta rapida da tastiera `p` [](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)).
1. Nella finestra **Proprietà**, selezionare la scheda **Cloud Services**.
1. Per la **Configurazione cloud** Seleziona la [configurazione creata in precedenza.](create-configuration.md)

   ![Configurare la cartella delle risorse](../assets/assets-folder-configure.png)
1. Tocca o fai clic su **Salva e chiudi**.
1. Tocca o fai clic su **OK** nella finestra di conferma.

   ![Finestra di conferma](../assets/assets-folder-confirmation.png)

È possibile creare ulteriori sottocartelle all’interno della cartella appena creata. Le sottocartelle erediteranno la **Configurazione cloud** della cartella principale. Tuttavia, questo può essere ignorato se desideri utilizzare modelli di un’altra configurazione.

Se utilizzi una struttura del sito localizzata, puoi [creare una directory principale della lingua](/help/assets/translate-assets.md) sotto la nuova cartella.

## Passaggi successivi {#next-steps}

Dopo aver creato una cartella per i frammenti di contenuto, puoi passare alla quarta parte della guida introduttiva e [creare frammenti di contenuto.](create-content-fragment.md)

>[!TIP]
>
>Per informazioni complete sulla gestione dei frammenti di contenuto, consulta la [documentazione sui frammenti di contenuto](/help/assets/content-fragments/content-fragments.md)
