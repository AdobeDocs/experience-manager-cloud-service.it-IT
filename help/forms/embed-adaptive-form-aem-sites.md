---
title: 'Come incorporare un modulo adattivo in una pagina AEM siti? '
description: È possibile incorporare Adaptive Forms nelle pagine AEM siti. Gli utenti possono compilare e inviare i moduli senza uscire dalle pagine del sito.
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 1%

---


# Incorporare un modulo adattivo nella pagina AEM siti {#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-page}

[!DNL AEM Forms] consente agli sviluppatori di moduli di incorporare facilmente Adaptive Forms in una pagina AEM Sites o in una pagina web ospitata all&#39;esterno di AEM. Il modulo adattivo incorporato è completamente funzionale e gli utenti possono compilare e inviare il modulo senza uscire dalla pagina. Consente all’utente di rimanere nel contesto di altri elementi della pagina web e di interagire contemporaneamente con il modulo .

<!-- For information about embedding an Adaptive Form in an external web page, see [Embed Adaptive Form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md). -->

Nella pagina AEM Sites è possibile aggiungere un modulo adattivo utilizzando:

* **[[!DNL AEM Forms] Componente contenitore](#af-component)**
   [!DNL AEM Forms] fornisce un componente che è possibile aggiungere alle pagine del sito. La [!DNL AEM Forms] Il componente Contenitore consente di incorporare un modulo adattivo.

* **[Browser risorse](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)**
Tutti i moduli creati sono disponibili in Risorse. È possibile trascinare il modulo come risorsa sulla pagina.

## Prerequisiti {#prerequisites}

Per incorporare un modulo adattivo in una pagina AEM siti che utilizza un modello modificabile, assicurati che il componente Modulo AEM sia configurato come componente consentito nel modello associato. Per ulteriori informazioni, consulta **Criteri e proprietà (contenitore di layout)** sezione [Creazione di modelli di pagina](/help/sites-authoring/templates.md).

Nel caso di una pagina Sites che utilizza un modello statico, devi configurarla nel sistema di paragrafi della pagina del sito. Per ulteriori informazioni, consulta [Configurazione dei componenti in modalità Progettazione](/help/sites-authoring/default-components-designmode.md).

## Incorporazione di un modulo adattivo  {#af-component}

Per incorporare un modulo adattivo utilizzando [!DNL AEM Forms] Componente contenitore:

1. Apri la pagina AEM siti in modalità di modifica in cui desideri incorporare un modulo adattivo .
1. Dal pannello del browser Componenti, trascina [!DNL AEM Forms] Componente contenitore nella pagina.

   In alternativa, puoi cercare un modulo adattivo nel browser Risorse e trascinarlo nella pagina Sites . Incorpora il modulo in un [!DNL AEM Forms] Contenitore.

   >[!NOTE]
   >
   >Multipli [!DNL AEM Forms] I componenti contenitore in una pagina non sono supportati.

1. Toccare l’incorporato [!DNL AEM Forms] Componente contenitore nella pagina Sites, quindi tocca ![settings_icon](assets/settings_icon.png) sulla barra delle azioni. La **[!UICONTROL Modifica contenitore AEM Forms]** viene visualizzata la finestra di dialogo .
1. Nella finestra di dialogo Modifica [!DNL AEM Forms] Nella finestra di dialogo Contenitore , specifica quanto segue.

   * **Tipo risorsa:** Seleziona il tipo di risorsa da incorporare. Le opzioni sono Modulo adattivo
   * **Percorso risorsa**: Sfoglia e seleziona il modulo adattivo da incorporare. Viene compilato automaticamente se viene rilasciato dal browser Risorse.
   * (Solo per modulo adattivo) **Invia invio**: Selezionare l’azione da attivare all’invio del modulo. Puoi scegliere di mostrare un messaggio di ringraziamento o una pagina di ringraziamento.

      * **Messaggio di ringraziamento**: Scrivere un messaggio utilizzando l’editor Rich Text da visualizzare durante l’invio del modulo. Questa opzione è disponibile solo quando scegli di mostrare un messaggio di ringraziamento.
      * **Pagina di ringraziamento**: Individuare e selezionare la pagina da visualizzare durante l’invio del modulo. Questa opzione è disponibile solo quando scegli di mostrare una pagina di ringraziamento.
      * **Aggiorna pagina all’invio**: Abilita l’aggiornamento della pagina contenente il modulo adattivo incorporato per visualizzare la pagina di ringraziamento. In caso contrario, la pagina di ringraziamento sostituisce il Modulo adattivo nel [!DNL AEM Forms] , senza aggiornare la pagina. Questa opzione è disponibile solo quando scegli di mostrare una pagina di ringraziamento.
   * **Tema**: Seleziona un tema che definisce lo stile dei componenti del modulo adattivo . Lo stile include proprietà di aspetto quali stile font, colore di sfondo, dimensioni e allineamento.
   * **Altezza**: Specifica l’altezza del contenitore. Lascia vuoto per ridimensionare automaticamente il contenitore.
   * **Libreria client CSS**: Specifica il percorso di una libreria client CSS.


1. Salva le impostazioni. Il modulo adattivo è ora incorporato nella pagina .

## Pubblicazione di un modulo adattivo incorporato {#publishing-embedded-adaptive-form}

Consideriamo i seguenti scenari per la pubblicazione di una risorsa incorporata (Modulo adattivo ) nella pagina AEM siti:

* Se pubblichi la pagina dei siti di AEM per la prima volta e include un modulo adattivo incorporato , pubblica la pagina dei siti e la risorsa incorporata.
* Se hai modificato solo il modulo adattivo incorporato in una pagina del sito pubblicata, pubblica la risorsa originale e le modifiche si riflettono nella pagina del sito pubblicata. La pagina del sito pubblicata include un riferimento alla risorsa e non richiede la ripubblicazione della pagina.
* Se hai modificato la pagina dei siti e il modulo adattivo incorporato , ripubblica la pagina dei siti e la risorsa incorporata.

## Modifica del modulo adattivo incorporato {#modifying-embedded-adaptive-form-and-interactive-communication}

AEM pagina dei siti mantiene un riferimento al Modulo adattivo nel [!DNL AEM Forms] Contenitore. Pertanto, tutte le configurazioni e proprietà, come il tema, gli stili e l’azione di invio, configurate nel modulo adattivo originale vengono mantenute nel modulo adattivo incorporato.

Per modificare una configurazione o una proprietà del modulo adattivo incorporato, effettuare una delle operazioni seguenti.

* Apri il modulo originale in Adaptive Forms nei rispettivi editor e modificalo.
* Tocca Modulo adattivo dalla pagina del sito in modalità di modifica, quindi tocca **[!UICONTROL Modifica in una nuova finestra]**. Il modulo originale viene aperto in modalità di modifica che è possibile modificare.

>[!NOTE]
>
>Le modifiche apportate al modulo adattivo originale si riflettono automaticamente nel modulo incorporato. Tuttavia, ripubblica il modulo adattivo o la pagina del sito per riflettere le modifiche nella pagina pubblicata.

## Considerazioni e best practice {#considerations-and-best-practices}

Quando incorpori Adaptive Forms nelle pagine dei siti di AEM, ricorda quanto segue:

* Le intestazioni e i piè di pagina nel modulo originale non sono inclusi nel modulo incorporato.
* Le bozze degli utenti e gli invii dei moduli incorporati sono supportati e visibili nelle schede Bozze e Inviate Forms sul portale dei moduli.
* L’azione di invio configurata sul modulo originale viene mantenuta nel modulo incorporato.
* Il targeting delle esperienze e i test A/B configurati sul modulo originale non funzionano nel modulo incorporato. Tuttavia, puoi utilizzare il targeting delle esperienze nella pagina Sites per presentare moduli diversi basati sui profili utente.
* Se Adobe Analytics è stato configurato per il modulo originale, i dati analitici del modulo incorporato vengono acquisiti in Adobe Analytics. Tuttavia, non è disponibile nel rapporto di analisi dei moduli.

