---
title: Pubblicazione di contenuti con l’Editor pagina
description: Scopri come l’Editor pagina pubblica i contenuti.
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 5871e04d3bd78bdd8df55d42e7619c98ea3f38ca
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 44%

---


# Pubblicazione di contenuti con l’Editor siti {#publishing}

Scopri come l’Editor pagina pubblica i contenuti.

## Pubblicazione dall’Editor pagina {#publishing-from-the-page-editor}

Se stai modificando una pagina nell&#39;[editor di pagine](/help/sites-cloud/authoring/page-editor/introduction.md), puoi pubblicarla direttamente dall&#39;editor.

1. Seleziona l’icona **Informazioni pagina** per aprire il menu, quindi l’opzione **Pubblica pagina**.

   ![Pubblicazione di una pagina tramite le opzioni di pagina](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. A seconda che la pagina includa o meno riferimenti che devono essere pubblicati:

   * La pagina viene pubblicata direttamente, se non sono presenti riferimenti da pubblicare.
   * Se la pagina include riferimenti da pubblicare, questi sono elencati nella procedura guidata di **Pubblicazione**, dove è possibile:
      * Specifica le risorse, i tag e così via da pubblicare insieme alla pagina, quindi utilizza **Pubblica** per completare il processo.
      * Seleziona **Annulla** per annullare l’azione.

   ![Pubblicazione di riferimenti alla pagina](/help/sites-cloud/authoring/assets/publishing-references.png)

1. Se selezioni l’opzione **Pubblica**, la pagina verrà replicata nell’ambiente di pubblicazione. Nell’editor pagina viene visualizzato un banner informativo che conferma l’azione di pubblicazione.

   ![Banner informazioni stato di pubblicazione](/help/sites-cloud/authoring/assets/publishing-info.png)

   Quando visualizzi la stessa pagina nella console, lo stato aggiornato della pubblicazione è visibile.

   ![Stato di pubblicazione della pagina nella vista a colonne della console Sites](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>La pubblicazione dall’editor pagina è superficiale, ovvero vengono pubblicate solo le pagine selezionate e non le relative pagine figlie.

>[!NOTE]
>
>Impossibile pubblicare le pagine a cui accedono [alias](/help/sites-cloud/authoring/sites-console/page-properties.md#advanced) nell&#39;editor. Le opzioni di pubblicazione nell’editor sono disponibili solo per le pagine accessibili tramite i percorsi effettivi.

## Annullamento della pubblicazione dall’Editor pagina {#unpublishing}

Durante la modifica di una pagina tramite Editor pagine, se desideri annullare la pubblicazione della pagina, seleziona **Annulla pubblicazione pagina** nel menu **Informazioni pagina**, esattamente come [pubblicheresti la pagina](#publishing-from-the-editor).

>[!NOTE]
>
>Non è possibile annullare la pubblicazione delle pagine a cui accedono [alias](/help/sites-cloud/authoring/sites-console/page-properties.md#advanced) nell&#39;editor. Le opzioni di pubblicazione nell’editor sono disponibili solo per le pagine accessibili tramite i percorsi effettivi.

## Pubblicazione e annullamento della pubblicazione dalla console Sites {#publishing-sites-console}

Puoi anche pubblicare [dalla console Sites](/help/sites-cloud/authoring/sites-console/publishing-pages.md), utile quando desideri pubblicare più pagine di contenuto o pianificare la pubblicazione o l&#39;annullamento della pubblicazione.
