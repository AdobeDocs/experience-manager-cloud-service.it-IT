---
title: Utilizzare i set di regole per trasformare gli URL
description: Scopri come distribuire i set di regole in Dynamic Media per trasformare gli URL. I set di regole sono insiemi di istruzioni scritte in un linguaggio di script (ad esempio JavaScript) che valutano i dati XML e eseguono determinate azioni se tali dati soddisfano determinate condizioni.
contentOwner: Rick Brough
role: User
exl-id: f8010125-ba89-406a-bede-f6aa2f858c70
source-git-commit: 35caac30887f17077d82f3370f1948e33d7f1530
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 0%

---

# Utilizzare i set di regole per trasformare gli URL {#using-rulesets-to-transform-urls}

Puoi distribuire i set di regole in Dynamic Media per trasformare gli URL. I set di regole sono insiemi di istruzioni scritte in un linguaggio di script (ad esempio JavaScript) che valutano i dati XML e eseguono determinate azioni se tali dati soddisfano determinate condizioni. Ogni regola consiste di almeno una condizione e almeno un&#39;azione. Una regola valuta i dati XML in base alle condizioni e, se una condizione viene soddisfatta, esegue l&#39;azione appropriata. Esempi di set di regole includono:

* Aggiunta di un suffisso di tipo MIME. Molti servizi e siti web richiedono suffissi di immagini, ad esempio l&#39;aggiunta di `.jpg` a un URL.
* Creazione di un percorso di cartella per l’URL a scopo di ottimizzazione SEO (Search Engine Optimization).

   Vedi [Come Adobe Dynamic Media Classic supporta il SEO](/help/assets/dynamic-media/assets/s7_seo.pdf).

* Aggiunta di metadati all’URL per scopi SEO (Search Engine Optimization).

   Vedi [Come Adobe Dynamic Media Classic supporta il SEO](/help/assets/dynamic-media/assets/s7_seo.pdf).

* Impostazione della disposizione dei contenuti per attivare un download.
* Semplificare gli URL dei modelli di Image Server per la personalizzazione. Ad esempio, girare `rgb{XX,YY,ZZ}` in RTF-ready `\redXX\greenYY\blueZZ`

* Richiedere la codifica di alcuni caratteri, ad esempio `$`, `{`e `}`, e alcuni caratteri da decodificare verso ImageServer. Ad esempio, Facebook non funziona bene con gli URL contenenti caratteri speciali.

   Vedi [Rimuovere i caratteri speciali dagli URL](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html).

Nel contesto di Dynamic Media, i siti web che utilizzano un sistema basato su XML per gestire le informazioni sulle risorse possono caricare file XML in Dynamic Media. Puoi designare uno di questi file come file del set di regole di pre-elaborazione per il serving della risorsa Dynamic Media. Questo file ristruttura il formato del protocollo URL standard per soddisfare la logica aziendale dei sistemi che vengono integrati con Dynamic Media. È possibile specificare un file XML da utilizzare come percorso del file delle definizioni del set di regole.

>[!CAUTION]
>
>Prestare attenzione quando si utilizzano i set di regole; possono impedire la visualizzazione del contenuto Dynamic Media sul sito web.

Sono disponibili set di regole di esempio che possono aiutarti a creare un set di regole personalizzato.
Vedi [Riferimento set di regole](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html).

Come per la creazione di tutti i set di regole, assicurati che il file XML sia valido prima di caricarlo utilizzando un programma di convalida XML come xmlvalid.
Vedi anche [Risolvere i problemi relativi ai set di regole](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html).

Inoltre, verifica prima il set di regole in un ambiente di staging che non influisce sull’ambiente di produzione live.
Gli ambienti di produzione e gli ambienti di staging in genere richiedono accessi diversi.

Consulta la sezione [Applicazione desktop Adobe Dynamic Media Classic per informazioni di accesso](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

<!-- OBSOLETE CONTENT * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

Vedi anche [Utilizzo dell&#39;immagine &quot;asset&quot; invece di &quot;is&quot; in un set di regole](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html).

## Distribuire set di regole XML {#deploy-xml-rule-sets}

1. Apri [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account.

   Le credenziali e i dettagli di accesso sono stati forniti da Adobe al momento del provisioning. Se non disponi di tali informazioni, contatta l’Assistenza clienti.

1. Carica il file del set di regole facendo quanto segue:

   * Nella barra di navigazione globale, seleziona **[!UICONTROL Carica]**.
   * Sulla **[!UICONTROL Carica]** , seleziona **[!UICONTROL Sfoglia]**.
   * In **[!UICONTROL Apri]** aprire il file del set di regole (XML).
   * Seleziona il file , quindi seleziona **[!UICONTROL Apri]**.
   * Sul lato destro del **[!UICONTROL Carica]** selezionare una cartella di destinazione per il file del set di regole.
   * Nella parte inferiore della pagina, accertati che l’opzione Pubblica dopo il caricamento sia selezionata.
   * Nell’angolo in basso a destra della pagina, seleziona **[!UICONTROL Invia caricamento]**.
   * Nella barra di navigazione globale, seleziona **[!UICONTROL Processi]** per controllare lo stato del processo di caricamento. Quando il **[!UICONTROL Stato]** nella colonna **[!UICONTROL Processo]** In questa pagina viene visualizzato Carica completato e continua con i passaggi successivi.

1. Nella barra di navigazione accanto alla parte superiore della pagina, individua **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Pubblica installazione]** > **[!UICONTROL Server immagini]**.
1. Sulla **[!UICONTROL Pubblicazione su Image Server]** sotto **[!UICONTROL Gestione catalogo]** gruppo, individuare **[!UICONTROL Percorso file definizione set regole]**, quindi seleziona **[!UICONTROL Seleziona]**.
1. Sulla **[!UICONTROL Seleziona il file di definizione del set di regole (XML)]** , individua il file del set di regole, quindi seleziona nell’angolo in basso a destra della pagina **[!UICONTROL Seleziona]**.
1. Nell’angolo inferiore destro della pagina Configurazione, seleziona **[!UICONTROL Chiudi]**.
1. Esegui un processo di pubblicazione su Image Server.

   Le condizioni del set di regole vengono applicate alle richieste ai server di immagini Dynamic Media live.

   Se modifichi il file del set di regole, le modifiche vengono applicate immediatamente quando ricarichi e ripubblichi il file del set di regole aggiornato.
