---
title: Incorporare un modulo adattivo nella pagina AEM Sites
seo-title: Hwo to add an Adaptive Form to an AEM Sites page?
description: È possibile utilizzare il componente Adattivo Forms -Embed per aggiungere o incorporare Forms adattivo a una pagina AEM Sites per compilare e inviare un modulo senza uscire dalle pagine AEM Sites.
feature: Adaptive Forms
exl-id: 359b05e8-d8c1-4a77-9e70-6f6b6e668560
source-git-commit: 2a487654c3af2d2ec3aa43481caed5e1d4fc77a2
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 0%

---

# Incorporare un modulo adattivo in una pagina AEM siti {#embed-an-adaptive-form-to-aem-sites-page}

## Panoramica {#overview}

AEM Forms consente agli sviluppatori di moduli di incorporare facilmente Adaptive Forms in una pagina AEM Sites o in una pagina web ospitata all&#39;esterno di AEM. Il modulo adattivo incorporato è completamente funzionale e gli utenti possono compilare e inviare il modulo senza uscire dalla pagina. Consente all’utente di rimanere nel contesto di altri elementi della pagina web e di interagire contemporaneamente con il modulo.



<!-- For information about embedding an Adaptive Form in an external web page, see [Embed Adaptive Form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md). -->

Nella pagina AEM Sites è possibile aggiungere un modulo adattivo utilizzando:

* **Forms adattivo - Incorpora componente**
Adattivo Forms: il componente Incorpora consente agli autori di AEM Sites di includere un modulo adattivo esistente all’interno di una pagina AEM Sites, ottimizzando in tal modo la riutilizzabilità dei moduli adattivi. Gli Adaptive Forms esistenti possono essere utilizzati autonomamente o incorporati nella pagina del sito. Questa integrazione offre ai clienti un modo pratico per riutilizzare l&#39;Adaptive Forms già creato.

* **Browser risorse**
Tutti i moduli sono disponibili in Risorse. È possibile trascinare il modulo come risorsa sulla pagina.

## Prerequisiti {#prerequisites}

Per incorporare un modulo adattivo in una pagina AEM Sites che utilizza un modello modificabile, accertati che il componente Modulo AEM sia configurato come componente consentito nel modello associato.

Nel caso **Forms adattivo - Incorpora componente** non è visibile nella **Pannello del browser Componenti** della pagina AEM siti , esegui i seguenti passaggi come illustrato nel video.

>[!VIDEO](https://video.tv.adobe.com/v/3410544)

Nel caso in cui la pagina Sites utilizzi un modello statico, devi configurarlo nel sistema di paragrafi della pagina del sito.

## Incorporazione di un modulo adattivo {#af-component}

Per incorporare un modulo adattivo utilizzando **[!UICONTROL Forms adattivo - Incorporamento]** componente:

1. Aprire la pagina AEM siti in modalità di modifica in cui si desidera incorporare un modulo adattivo.
1. Dal pannello del browser Componenti, trascina [!UICONTROL Forms adattivo - Incorporamento] nella pagina. In alternativa, puoi cercare un modulo adattivo nel browser Risorse e trascinarlo nella pagina Sites . È possibile aggiungere un nuovo modulo adattivo o incorporare un modulo adattivo esistente.

   >[!NOTE]
   >
   >Forms adattivo multiplo : i componenti da incorporare in una pagina non sono supportati.

1. Per creare e incorporare un nuovo modulo, sulla barra degli strumenti del componente, tocca **Crea modulo** icona. Viene visualizzata una finestra per creare il modulo.

1. Tocca il componente Forms adattivo incorporato - Incorpora nella pagina Sites , quindi tocca ![settings_icon](assets/settings_icon.png) sulla barra delle azioni. La **[!UICONTROL Modifica Forms adattivo - Incorpora]** viene visualizzata la finestra di dialogo .
1. Nella finestra di dialogo Modifica Forms adattivo - Incorpora , specifica quanto segue.

   **Tipo risorsa:** Seleziona il tipo di risorsa da incorporare.
   * **Percorso risorsa**: Sfoglia e seleziona il modulo adattivo da incorporare. Viene compilato automaticamente se viene rilasciato dal browser Risorse.
   * **Invia invio** : Selezionare l’azione da attivare all’invio del modulo. Puoi scegliere di mostrare un messaggio di ringraziamento o una pagina di ringraziamento.
      * Mostra

      * **Messaggio di ringraziamento**: Scrivere un messaggio utilizzando l’editor Rich Text da visualizzare durante l’invio del modulo. Questa opzione è disponibile solo quando scegli di mostrare un messaggio di ringraziamento.
      * **Pagina di ringraziamento**: Individuare e selezionare la pagina da visualizzare durante l’invio del modulo. Questa opzione è disponibile solo quando scegli di mostrare una pagina di ringraziamento.
         * **Reindirizza alla pagina di ringraziamento**: Abilita l’opzione per sostituire la pagina contenente il modulo adattivo incorporato con la pagina di ringraziamento. In caso contrario, la pagina di ringraziamento sostituisce il Modulo adattivo nel [!UICONTROL Forms adattivo - Incorporamento] senza aggiornare i siti sottostanti la pagina. Questa opzione è disponibile solo quando scegli di mostrare una pagina di ringraziamento.
   * **Usa lingua pagina**: Utilizza locale della pagina AEM Sites invece delle impostazioni internazionali del modulo adattivo.
   * **Imposta lo stato attivo sul modulo**: Selezionare questa opzione per impostare lo stato attivo sul primo campo del modulo adattivo.
   * **Tema**: Seleziona un tema che definisce lo stile dei componenti del modulo adattivo. Lo stile include proprietà di aspetto quali stile font, colore di sfondo, dimensioni e allineamento.
   * **Il modulo copre l&#39;intera larghezza del frame**: Se questa opzione è selezionata, l’iframe non viene utilizzato per il rendering del modulo.
   * **Altezza**: Specifica l’altezza del contenitore. Lascia vuoto per ridimensionare automaticamente il contenitore.
   * **Libreria client CSS**: Specifica il percorso di una libreria client CSS.

1. Salva le impostazioni. Il modulo adattivo è ora incorporato nella pagina .

AEM sito consente inoltre di creare al volo un Modulo adattivo utilizzando il componente Forms adattivo - Incorpora . Segui i passaggi per creare un modulo adattivo utilizzando **Forms adattivo - Incorpora componente** nella pagina AEM siti:
1. Aprire la pagina AEM siti in modalità di modifica in cui si desidera incorporare un modulo adattivo.
1. Dal pannello del browser Componenti , trascina sulla pagina il componente Forms adattivo - Incorpora .
1. Fai clic sul pulsante **Plus** e si viene reindirizzati alla procedura guidata di creazione del modulo.

   ![Forms adattivo - Componente da incorporare](/help/forms/assets/aemformcontainer.png)

1. È ora possibile incorporare un modulo adattivo AEM pagine del sito utilizzando [!UICONTROL Componente contenitore AEM Forms].

## Pubblicazione di un modulo adattivo incorporato {#publishing-embedded-adaptive-form}

Consideriamo i seguenti scenari per pubblicare un modulo adattivo incorporato nella pagina AEM siti:

* Se pubblichi la pagina dei siti di AEM per la prima volta e include un modulo adattivo incorporato, pubblica la pagina dei siti e la risorsa incorporata.
* Se hai modificato solo il modulo adattivo incorporato in una pagina del sito pubblicata, pubblica la risorsa originale e le modifiche si riflettono nella pagina del sito pubblicata. La pagina del sito pubblicata include un riferimento alla risorsa e non richiede la ripubblicazione della pagina.
* Se hai modificato la pagina dei siti e il modulo adattivo incorporato , ripubblica la pagina dei siti e la risorsa incorporata.

## Modifica del modulo adattivo incorporato  {#modifying-embedded-adaptive-form}

AEM pagina siti mantiene un riferimento al Modulo adattivo in Forms adattivo - Incorpora. Pertanto, tutte le configurazioni e proprietà, come il tema, gli stili e l’azione di invio, configurate nel modulo adattivo originale vengono mantenute nel modulo adattivo incorporato.

Per modificare una configurazione o una proprietà del modulo adattivo incorporato, effettuare una delle operazioni seguenti.

* Apri il modulo originale in moduli adattivi nei rispettivi editor e modificalo.
* Tocca Modulo adattivo dalla pagina del sito in modalità di modifica, quindi tocca **[!UICONTROL Modifica in una nuova finestra]**. Il modulo originale viene aperto in modalità di modifica che è possibile modificare.

>[!NOTE]
>
>Le modifiche apportate al modulo adattivo originale si riflettono automaticamente nel modulo incorporato. Tuttavia, ripubblica il modulo adattivo o la pagina del sito per riflettere le modifiche nella pagina pubblicata.

## Considerazioni e best practice {#considerations-and-best-practices}

Quando incorpori moduli adattivi nelle pagine dei siti AEM tenere a mente quanto segue:

* Le intestazioni e i piè di pagina nel modulo originale non sono inclusi nel modulo incorporato.
* Le bozze degli utenti e gli invii dei moduli incorporati sono supportati e visibili nelle schede Bozze e Inviate Forms sul portale Forms.
* L’azione di invio configurata sul modulo originale viene mantenuta nel modulo incorporato.
* Se Adobe Analytics è stato configurato per il modulo originale, i dati analitici del modulo incorporato vengono acquisiti in Adobe Analytics. Tuttavia, non è disponibile nel rapporto di analisi dei moduli.
