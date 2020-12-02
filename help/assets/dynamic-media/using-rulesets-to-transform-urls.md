---
title: Utilizzo dei set di regole per trasformare gli URL
description: Potete implementare i set di regole in Contenuti multimediali dinamici per trasformare gli URL. I set di regole sono insiemi di istruzioni scritte in un linguaggio di script (ad esempio JavaScript) che valutano i dati XML e eseguono determinate azioni se tali dati soddisfano determinate condizioni.
translation-type: tm+mt
source-git-commit: 1713cddf713afc24103a841a7dbae923941f6322
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 5%

---


# Utilizzo di set di regole per trasformare gli URL {#using-rulesets-to-transform-urls}

Potete implementare i set di regole in Contenuti multimediali dinamici per trasformare gli URL. I set di regole sono insiemi di istruzioni scritte in un linguaggio di script (ad esempio JavaScript) che valutano i dati XML e eseguono determinate azioni se tali dati soddisfano determinate condizioni. Ogni regola è costituita da almeno una condizione e almeno un&#39;azione. Una regola valuta i dati XML in base alle condizioni e, se una condizione è soddisfatta, esegue l&#39;azione appropriata. Esempi di set di regole:

* Aggiunta di un suffisso di tipo MIME. Molti servizi e siti Web richiedono suffissi per immagini, ad esempio l&#39;aggiunta di `.jpg` a un URL.
* Creazione di un percorso di cartella per l’URL per scopi SEO (Search Engine Optimization).

   Consultate [Come  Adobe Scene7 Publishing System supporta SEO](/help/assets/dynamic-media/assets/s7_seo.pdf).

* Aggiunta di metadati all’URL per scopi SEO (ottimizzazione motore di ricerca).

   Consultate [Come  Adobe Scene7 Publishing System supporta SEO](/help/assets/dynamic-media/assets/s7_seo.pdf).

* Impostazione della disposizione del contenuto per attivare un download.
* Semplificare gli URL dei modelli di Image Server per la personalizzazione. Ad esempio, trasformare `rgb{XX,YY,ZZ}` in formato RTF`\redXX\greenYY\blueZZ`

* Richiedete la codifica di alcuni caratteri, ad esempio `$`, `{` e `}`, e di alcuni caratteri da decodificare in ImageServer. Ad esempio, Facebook non funziona bene con gli URL contenenti caratteri speciali.

   Consultate [Rimozione di caratteri speciali dagli URL](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html).

Nel contesto dei file multimediali dinamici, i siti Web che utilizzano un sistema basato su XML per gestire le informazioni sulle risorse possono caricare file XML in contenuti multimediali dinamici. Potete designare uno di questi file come file del set di regole di pre-elaborazione per la trasmissione della risorsa multimediale dinamica. Questo file ristruttura il formato standard del protocollo URL per soddisfare la logica aziendale dei sistemi integrati con Dynamic Media. È possibile specificare un file XML da utilizzare come percorso del file di definizioni del set di regole.

>[!CAUTION]
>
>Prestare attenzione quando si utilizzano i set di regole; possono impedire la visualizzazione di contenuti multimediali dinamici sul sito Web.

Sono disponibili set di regole di esempio che possono facilitare la creazione di un set di regole personalizzato.
Vedere [Riferimento set di regole](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html).

Come per la creazione di tutti i set di regole, accertatevi che il file XML sia valido prima di caricarlo, utilizzando un programma di convalida XML come xmlvalid.
Vedere anche [Set di regole per la risoluzione dei problemi](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html).

Inoltre, verificare prima il set di regole in un ambiente di staging che non abbia alcun impatto sull&#39;ambiente di produzione live.
Gli ambienti di produzione e gli ambienti di pre-produzione in genere richiedono accessi diversi.

* **Una pagina di login** dell&#39;ambiente di staging:  [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **Pagina** di login dell&#39;ambiente di staging EMEA:  [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **Pagina** di login dell&#39;ambiente di staging JAPAC:  [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/)

Vedere anche [Utilizzo dell&#39;immagine &#39;asset&#39; invece di &#39;is&#39; in un set di regole](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html).

**Per distribuire i set di regole XML:**

1. Accedete al vostro account Dynamic Media Classic:

   [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   Le credenziali e l&#39;accesso sono stati forniti  Adobe al momento del provisioning. Se non disponete di tali informazioni, contattate il supporto tecnico.

1. Caricate il file del set di regole effettuando le seguenti operazioni:

   * Nella barra di navigazione globale, fate clic su **[!UICONTROL Carica]**.
   * Nella pagina **[!UICONTROL Upload]**, accanto all&#39;angolo superiore sinistro, fare clic su **[!UICONTROL Browse]**.
   * Nella finestra di dialogo **[!UICONTROL Apri]**, individuare il file del set di regole (XML).
   * Selezionare il file, quindi fare clic su **[!UICONTROL Apri]**.
   * Sul lato destro della pagina **[!UICONTROL Carica]**, selezionate una cartella di destinazione per il file del set di regole.
   * Vicino alla parte inferiore della pagina, verificare che l&#39;opzione **[!UICONTROL Pubblica dopo il caricamento]** sia selezionata.
   * Nell&#39;angolo inferiore destro della pagina, fate clic su **[!UICONTROL Invia caricamento]**.
   * Nella barra di navigazione globale, fate clic su **[!UICONTROL Processi]** per verificare lo stato del processo di caricamento. Quando la colonna **[!UICONTROL Status]** nella pagina **[!UICONTROL Job]** riporta Upload Done (Caricamento completato), continuate con i passaggi successivi.

1. Nella barra di navigazione accanto alla parte superiore della pagina, fate clic su **[!UICONTROL Configurazione > Impostazione applicazione > Impostazione pubblicazione > Server immagini]**.
1. Nella pagina **[!UICONTROL Pubblica su Image Server]**, seleziona il gruppo **[!UICONTROL Gestione catalogo]** e individua il **[!UICONTROL Percorso file definizione set regole]**, quindi fai clic su **[!UICONTROL Seleziona]**.
1. Nella pagina **[!UICONTROL Seleziona file definizione set regole (XML)]**, individua il file del set regole, quindi fai clic su **[!UICONTROL Seleziona]** nell’angolo inferiore destro della pagina.
1. Nell’angolo inferiore destro della pagina Configurazione, fate clic su **[!UICONTROL Chiudi]**.
1. Eseguire un processo di pubblicazione su Image Server.

   Le condizioni del set di regole vengono applicate alle richieste inviate ai server immagini per file multimediali dinamici dinamici in tempo reale.

   Se apportate modifiche al file del set di regole, le modifiche vengono applicate immediatamente quando caricate nuovamente e pubblicate nuovamente il file del set di regole aggiornato.

