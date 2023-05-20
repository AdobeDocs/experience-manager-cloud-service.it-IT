---
title: Incorporare un modulo adattivo nella pagina di AEM Sites
seo-title: Hwo to add an Adaptive Form to an AEM Sites page?
description: È possibile utilizzare il componente Forms adattivo - Incorpora per aggiungere o incorporare Forms adattivo in una pagina AEM Sites per compilare e inviare un modulo senza uscire dalle pagine AEM Sites.
feature: Adaptive Forms
exl-id: 359b05e8-d8c1-4a77-9e70-6f6b6e668560
source-git-commit: 2a487654c3af2d2ec3aa43481caed5e1d4fc77a2
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 0%

---

# Incorporare un modulo adattivo in una pagina dei siti AEM {#embed-an-adaptive-form-to-aem-sites-page}

## Panoramica {#overview}

AEM Forms consente agli sviluppatori di moduli di incorporare facilmente Forms adattivo in una pagina AEM Sites o in una pagina web ospitata al di fuori dell’AEM. Il modulo adattivo incorporato è completamente funzionante e gli utenti possono compilare e inviare il modulo senza uscire dalla pagina. Consente all’utente di rimanere nel contesto di altri elementi della pagina web e interagire contemporaneamente con il modulo.



<!-- For information about embedding an Adaptive Form in an external web page, see [Embed Adaptive Form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md). -->

Nella pagina di AEM Sites puoi aggiungere un modulo adattivo utilizzando:

* **Forms adattivo - Componente di incorporamento**
Forms adattivo: il componente Incorpora consente agli autori di AEM Sites di includere un modulo adattivo esistente all’interno di una pagina AEM Sites, migliorando in tal modo la riutilizzabilità dei moduli adattivi. Il Forms adattivo esistente può essere utilizzato da solo o incorporato nella pagina del sito. Questa integrazione offre ai clienti un modo pratico per riutilizzare i Forms adattivi già creati.

* **Browser risorse**
Tutti i moduli sono disponibili in Assets. Puoi trascinare il modulo come risorsa sulla pagina.

## Prerequisiti {#prerequisites}

Per incorporare un modulo adattivo in una pagina di AEM Sites che utilizza un modello modificabile, accertati che il componente Modulo AEM sia configurato come componente consentito nel modello associato.

Nel caso **Forms adattivo - Componente di incorporamento** non è visibile in **Pannello browser Componenti** nella pagina dei siti AEM, effettua le seguenti operazioni, come illustrato nel video.

>[!VIDEO](https://video.tv.adobe.com/v/3410544)

Se la pagina Sites utilizza un modello statico, devi configurarlo nel sistema paragrafo della pagina del sito.

## Incorporazione di un modulo adattivo {#af-component}

Per incorporare un modulo adattivo utilizzando **[!UICONTROL Forms adattivo - Incorpora]** componente:

1. Apri la pagina dei siti AEM, in modalità di modifica, in cui desideri incorporare un modulo adattivo.
1. Dal pannello del browser Componenti, trascina [!UICONTROL Forms adattivo - Incorpora] sulla pagina. In alternativa, puoi cercare un modulo adattivo nel browser Risorse e trascinarlo sulla pagina Sites. Puoi aggiungere un nuovo modulo adattivo o incorporarne uno esistente.

   >[!NOTE]
   >
   >Forms adattivo multiplo: non sono supportati i componenti incorporati in una pagina.

1. Per creare e incorporare un nuovo modulo, sulla barra degli strumenti del componente tocca **Crea modulo** icona. Viene visualizzata una finestra per creare la maschera.

1. Tocca il componente Forms adattivo incorporato - Incorpora nella pagina Sites, quindi tocca ![icona_impostazioni](assets/settings_icon.png) sulla barra delle azioni. Il **[!UICONTROL Modifica Forms adattivo - Incorpora]** viene visualizzata una finestra di dialogo.
1. Nella finestra di dialogo Modifica Forms adattivo - Incorpora, specifica quanto segue.

   **Tipo risorsa:** Seleziona il tipo di risorsa da incorporare.
   * **Percorso risorsa**: sfoglia e seleziona il modulo adattivo da incorporare. Viene compilato automaticamente se viene rilasciato dal browser Risorse.
   * **Invio post** : seleziona l’azione da attivare all’invio del modulo. Puoi scegliere di visualizzare un messaggio di ringraziamento o una pagina di ringraziamento.
      * Mostra

      * **Messaggio di ringraziamento**: scrivi un messaggio utilizzando l’editor Rich Text. Questa opzione è disponibile solo quando si sceglie di visualizzare un messaggio di ringraziamento.
      * **Pagina di ringraziamento**: sfoglia e seleziona la pagina da visualizzare all’invio del modulo. Questa opzione è disponibile solo quando si sceglie di visualizzare una pagina di ringraziamento.
         * **Reindirizza alla pagina di ringraziamento**: abilita l’opzione per sostituire la pagina contenente il modulo adattivo incorporato con la pagina di ringraziamento. In caso contrario, la pagina di ringraziamento sostituisce il modulo adattivo nel [!UICONTROL Forms adattivo - Incorpora] senza aggiornare i siti sottostanti nella pagina. Questa opzione è disponibile solo quando si sceglie di visualizzare una pagina di ringraziamento.
   * **Usa lingua della pagina**: utilizza la lingua locale della pagina AEM Sites invece della lingua del modulo adattivo.
   * **Imposta stato attivo sul modulo**: seleziona per impostare lo stato attivo sul primo campo del modulo adattivo.
   * **Tema**: seleziona un tema che definisce lo stile dei componenti del modulo adattivo. Lo stile include proprietà di aspetto quali lo stile del carattere, il colore di sfondo, le dimensioni e l&#39;allineamento.
   * **La forma copre l&#39;intera larghezza della cornice**: se questa opzione è selezionata, iframe non viene utilizzato per il rendering del modulo.
   * **Altezza**: specifica l’altezza del contenitore. Lascia vuoto questo campo per ridimensionare automaticamente il contenitore.
   * **Libreria client CSS**: specifica il percorso di una libreria client CSS.

1. Salva le impostazioni. Il modulo adattivo è ora incorporato nella pagina.

Il sito AEM consente inoltre di creare al volo un modulo adattivo utilizzando il componente Forms adattivo - Incorpora. Per creare un modulo adattivo utilizzando la funzione **Forms adattivo - Componente di incorporamento** nella pagina dedicata ai siti AEM:
1. Apri la pagina dei siti AEM, in modalità di modifica, in cui desideri incorporare un modulo adattivo.
1. Dal pannello del browser Componenti, trascina il componente Forms adattivo - Incorpora nella pagina.
1. Fai clic su **Più** e si viene reindirizzati alla procedura guidata di creazione del modulo.

   ![Forms adattivo: componente Incorpora](/help/forms/assets/aemformcontainer.png)

1. È ora possibile incorporare un modulo adattivo nelle pagine del sito AEM utilizzando [!UICONTROL Componente Contenitore AEM Forms].

## Pubblicazione di un modulo adattivo incorporato {#publishing-embedded-adaptive-form}

Prendiamo in considerazione i seguenti scenari per la pubblicazione di un modulo adattivo incorporato nella pagina dei siti AEM:

* Se pubblichi la pagina dei siti AEM per la prima volta e include un modulo adattivo incorporato, pubblica la pagina dei siti e la risorsa incorporata.
* Se hai modificato solo il modulo adattivo incorporato in una pagina del sito pubblicata, pubblica la risorsa originale e le modifiche si riflettono nella pagina del sito pubblicata. La pagina del sito pubblicata include un riferimento alla risorsa e non richiede la ripubblicazione della pagina.
* Se hai modificato la pagina Sites e il modulo adattivo incorporato, ripubblica la pagina Sites e la risorsa incorporata.

## Modifica di un modulo adattivo incorporato  {#modifying-embedded-adaptive-form}

Nella pagina dei siti AEM viene mantenuto un riferimento al modulo adattivo in Adaptive Forms - Embed. Pertanto, tutte le configurazioni e le proprietà, come il tema, gli stili e l’azione di invio, configurate nel modulo adattivo originale vengono mantenute nel modulo adattivo incorporato.

Per modificare una configurazione o una proprietà del modulo adattivo incorporato, effettuate una delle seguenti operazioni.

* Apri il modulo originale nei moduli adattivi nei rispettivi editor e modificali.
* In modalità di modifica, tocca il modulo adattivo all’interno della pagina del sito, quindi tocca **[!UICONTROL Modifica in una nuova finestra]**. Il modulo originale viene aperto in modalità di modifica modificabile.

>[!NOTE]
>
>Le modifiche apportate nel modulo adattivo originale si riflettono automaticamente nel modulo incorporato. Tuttavia, ripubblica il modulo adattivo o la pagina del sito per riflettere le modifiche nella pagina pubblicata.

## Considerazioni e best practice {#considerations-and-best-practices}

Quando incorpori moduli adattivi nelle pagine dei siti AEM, considera gli aspetti seguenti:

* Intestazione e piè di pagina nel modulo originale non sono inclusi nel modulo incorporato.
* Le bozze utente e gli invii di moduli incorporati sono supportati e visibili nelle schede Bozze e Forms inviate nel portale Forms.
* L’azione di invio configurata nel modulo originale viene mantenuta nel modulo incorporato.
* Se hai configurato Adobe Analytics per il modulo originale, i dati di analisi del modulo incorporato vengono acquisiti in Adobe Analytics. Tuttavia, non è disponibile nel rapporto di analisi di Forms.
