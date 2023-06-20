---
title: Promozione dei lanci
description: È necessario promuovere le pagine di lancio per spostare nuovamente il contenuto nell’origine (produzione) prima di pubblicarlo.
exl-id: 5f5ed17c-43db-4ef6-ab79-c491326fa01c
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 46%

---

# Promozione dei lanci {#promoting-launches}

È necessario promuovere le pagine di lancio per spostare nuovamente il contenuto nell’origine (produzione) prima di pubblicarlo. Quando una pagina di lancio viene promossa, la pagina corrispondente nelle pagine sorgente viene sostituita con il contenuto della pagina promossa. Durante la promozione di una pagina di lancio sono disponibili le seguenti opzioni:

* Indica se promuovere solo la pagina corrente o l’intero lancio.
* Indica se promuovere le pagine figlie della pagina corrente.
* Indica se promuovere l’intero lancio o solo le pagine che sono state modificate.
* Se eliminare il lancio dopo essere stato promosso.

>[!NOTE]
>
>Dopo aver promosso le pagine di lancio nella destinazione (**Produzione**), è possibile attivare **Produzione** pagine come entità (per velocizzare il processo). Aggiungi le pagine a un pacchetto di flusso di lavoro e utilizzalo come payload per un flusso di lavoro che attiva un pacchetto di pagine. Devi creare il pacchetto del flusso di lavoro prima di promuovere il lancio. Consulta [Elaborazione di pagine promosse tramite flusso di lavoro AEM](#processing-promoted-pages-using-aem-workflow).

>[!CAUTION]
>
>Non è possibile promuovere contemporaneamente un singolo lancio. Due azioni di promozione sullo stesso lancio nello stesso momento possono causare un errore: `Launch could not be promoted` (con gli errori di conflitto nel registro).

>[!CAUTION]
>
>Durante la promozione dei lanci per *modificato* , vengono considerate le modifiche nei rami sorgente e lancio.

## Promozione delle pagine di lancio {#promoting-launch-pages}

>[!NOTE]
>
>In questo modo viene illustrata l’azione manuale di promozione delle pagine di lancio quando è presente un solo livello di lancio. Consulta:
>
>* [Promozione di un lancio nidificato](#promoting-a-nested-launch) quando nella struttura è presente più di un lancio.
>* [Lanci: l’ordine degli eventi](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events) per maggiori dettagli sulla promozione e la pubblicazione automatiche.
>

Puoi promuovere i lanci da **Sites** console o **Lanci** console:

1. Apri:
   * La console **Sites** durante la navigazione nelle pagine sorgente:
      1. Apri la [barra dei riferimenti](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) e seleziona la pagina sorgente desiderata utilizzando la [modalità di selezione](/help/sites-cloud/authoring/getting-started/basic-handling.md) (oppure seleziona e apri la barra dei riferimenti, l’ordine non è importante). Vengono visualizzati tutti i riferimenti.
      1. Seleziona **Lanci** (ad esempio Lanci (1)) per visualizzare un elenco dei lanci specifici.
      1. Seleziona il lancio specifico per visualizzare le azioni disponibili.
      1. Seleziona **Promuovi lancio** per aprire la procedura guidata.
   * La console **Sites** durante la navigazione nelle pagine di lancio:
      1. Seleziona la pagina di lancio desiderata utilizzando [modalità di selezione](/help/sites-cloud/authoring/getting-started/basic-handling.md).
      1. L&#39;azione **Promuovi** è disponibile nella barra degli strumenti.
   * La console **Launches**:
      1. Seleziona il lancio (tocca o fai clic sulla miniatura).
      1. Seleziona **Promuovi**.
1. Nel primo passaggio puoi specificare:
   * **Destinazione**
      * **Elimina lancio dopo la promozione**
   * **Ambito**
      * **Promuovi tutto il lancio**
      * **Promuovi pagine modificate**
      * **Promuovi pagine approvate**: a seconda del flusso di lavoro di approvazione del lancio
      * **Promuovi la pagina corrente**
      * **Promuovi la pagina corrente e le sottopagine**

     Ad esempio, quando selezioni solo la promozione delle pagine modificate:

     ![Promozione di un lancio](/help/sites-cloud/authoring/assets/launches-promote.png)

     >[!NOTE]
     >
     >In questo modo viene coperto un singolo lancio. Se hai dei lanci nidificati, vedi [Promozione di un lancio nidificato](#promoting-a-nested-launch).
1. Seleziona **Successivo** per procedere.
1. Puoi rivedere le pagine da promuovere, a seconda dell’intervallo di pagine scelto:

   ![Rivedi promozione](/help/sites-cloud/authoring/assets/launches-promote-review.png)

1. Seleziona **Promuovi**.

## Promozione delle pagine di Launch durante la modifica {#promoting-launch-pages-when-editing}

Quando modifichi una pagina di lancio, il **Promuovi lancio** L&#39;azione è disponibile anche da **Informazioni pagina**. Si aprirà la procedura guidata per raccogliere le informazioni necessarie.

![Promuovi il lancio dalle informazioni del sito](/help/sites-cloud/authoring/assets/launches-promote-page-info.png)

>[!NOTE]
>
>Questo è disponibile per singoli e [lanci nidificati](#promoting-a-nested-launch).

## Promozione di un lancio nidificato {#promoting-a-nested-launch}

Dopo aver creato un lancio nidificato, puoi promuoverlo nuovamente in qualsiasi origine, inclusa la sorgente principale (produzione).

![Un lancio nidificato](/help/sites-cloud/authoring/assets/launches-promoting-nested.png)

1. Come per la Creazione di un lancio nidificato, accedi e seleziona il lancio richiesto nella console **Lanci** o nella barra **Riferimenti**.
1. Seleziona **Promuovi lancio** per aprire la procedura guidata.
1. Immetti i dettagli necessari:
   * **Destinazione**
      * **Destinazione della promozione**: puoi promuovere su qualsiasi sorgente.
      * **Elimina lancio dopo la promozione**: dopo la promozione del lancio selezionato e dei lanci nidificati al suo interno, esso verrà eliminato.
   * **Ambito**: puoi scegliere se promuovere l’intero lancio o solo le pagine che sono state modificate. In quest’ultimo caso, puoi selezionare di includere/escludere le sottopagine. La configurazione predefinita prevede di promuovere solo le modifiche alla pagina corrente:
      * **Promuovi tutto il lancio**
      * **Promuovi pagine modificate**
      * **Promuovi pagine approvate**: a seconda del flusso di lavoro di approvazione del lancio
      * **Promuovi la pagina corrente**
      * **Promuovi la pagina corrente e le sottopagine**

   ![Promuovi impostazioni lancio](/help/sites-cloud/authoring/assets/launches-promote-settings.png)

1. Seleziona **Avanti**.
1. Rivedi i dettagli della promozione prima di selezionare **Promuovi**:

   ![Rivedi le impostazioni di promozione](/help/sites-cloud/authoring/assets/launches-promote-review-2.png)

   >[!NOTE]
   >
   >Le pagine elencate dipendono dal **Ambito** definite ed eventualmente le pagine che sono state modificate.

1. Le modifiche vengono promosse e riflesse in **Lanci** console:

   ![Nella console Launches](/help/sites-cloud/authoring/assets/launches-console.png)

## Elaborazione di pagine promosse tramite Flusso di lavoro AEM {#processing-promoted-pages-using-aem-workflow}

Utilizza i modelli di flusso di lavoro per eseguire l’elaborazione in blocco delle pagine dei lanci promossi:

1. Creare un pacchetto di flusso di lavoro.
1. Quando gli autori promuovono le pagine di Launch, le memorizzano nel pacchetto del flusso di lavoro.
1. Avvia un modello di flusso di lavoro utilizzando il pacchetto come payload.

Per avviare automaticamente un flusso di lavoro quando vengono promosse le pagine, configura un programma di avvio del flusso di lavoro per il nodo del pacchetto. <!--To start a workflow automatically when pages are promoted, [configure a workflow launcher](/help/sites-administering/workflows-starting.md#workflows-launchers) for the package node.-->

Ad esempio, puoi generare automaticamente le richieste di attivazione pagina non appena un autore promuove una pagina di lancio. Configura un modulo di avvio del flusso di lavoro per avviare il flusso di lavoro Attivazione richiesta quando viene modificato il nodo del pacchetto.

![Flusso di lavoro di promozione](/help/sites-cloud/authoring/assets/launches-create-workflow.png)
