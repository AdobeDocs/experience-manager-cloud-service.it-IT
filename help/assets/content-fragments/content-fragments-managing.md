---
title: Gestione dei frammenti di contenuto
description: Scopri come utilizzare la console Risorse per gestire i frammenti di contenuto AEM, alla base dei contenuti headless.
feature: Frammenti di contenuto
role: Professionista
translation-type: tm+mt
source-git-commit: 6fa911f39d707687e453de270bc0f3ece208d380
workflow-type: tm+mt
source-wordcount: '1644'
ht-degree: 9%

---


# Gestione dei frammenti di contenuto {#managing-content-fragments}

Scopri come utilizzare la console Risorse per gestire i frammenti di contenuto AEM, alla base dei contenuti headless.

I frammenti di contenuto sono memorizzati come **Risorse**, quindi vengono gestiti principalmente dalla console **Risorse**.

>[!NOTE]
>
>I frammenti di contenuto possono essere utilizzati:
>
>* quando si creano pagine; consulta [Authoring delle pagine con frammenti di contenuto](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
>* per [Distribuzione di contenuti headless tramite frammenti di contenuto con GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).


## Creazione di frammenti di contenuto {#creating-content-fragments}

### Creazione di un modello di contenuto {#creating-a-content-model}

[È possibile abilitare e creare ](/help/assets/content-fragments/content-fragments-models.md) modelli di frammento di contenuto prima di creare frammenti di contenuto con contenuto strutturato.

### Creazione di un frammento di contenuto {#creating-a-content-fragment}

Il metodo di creazione di un frammento di contenuto è:

1. Passa alla cartella **Risorse** in cui desideri creare il frammento.
1. Per aprire la procedura guidata, seleziona **Crea**, quindi **Frammento di contenuto**.
1. Il primo passaggio della procedura guidata richiede di specificare la base del nuovo frammento.

   * [Modello](/help/assets/content-fragments/content-fragments-models.md) : utilizzato per creare un frammento che richiede contenuto strutturato; ad esempio il modello  **** Avventuremodel

      * Vengono visualizzati tutti i modelli disponibili.

   Dopo la selezione, utilizza **Avanti** per continuare.

   ![base del frammento](assets/cfm-managing-01.png)

1. Nel passaggio **Proprietà** specifica:

   * **Base**

      * **Titolo**

         Titolo del frammento.

         Obbligatorio.

      * **Descrizione**

      * **Tag**
   * **Avanzate**

      * **Nome**

         il nome; verrà utilizzato per formare l’URL.

         Obbligatorio; viene derivato automaticamente dal titolo, ma può essere aggiornato.


1. Seleziona **Crea** per completare l’azione, quindi **Apri** il frammento per la modifica oppure tornare alla console facendo clic su **Fine**.

   >[!NOTE]
   >In modalità **Elenco** della console è possibile aggiornare **Visualizza impostazioni** per abilitare la colonna **Modello frammento di contenuto**.

## Azioni per un frammento di contenuto nella console Assets {#actions-for-a-content-fragment-assets-console}

Nella console **Risorse** sono disponibili diverse azioni per i frammenti di contenuto:

* Dalla barra degli strumenti; dopo aver selezionato il frammento sono disponibili tutte le azioni appropriate.
* Come [azioni rapide](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions); un sottoinsieme di azioni disponibili per le singole schede di frammento.

![azioni](assets/cfm-managing-02.png)

Seleziona il frammento per visualizzare la barra degli strumenti con le azioni applicabili:

* **Rielabora risorse**
* **Crea**
* **Scarica**

   * Salvare il frammento come file ZIP; puoi definire se includere elementi, varianti, metadati.

* **Pagamento**
* **Proprietà**

   * Consente di visualizzare e/o modificare i metadati del frammento.

* **Modifica**

   * Consente di [aprire il frammento per la modifica di contenuto](/help/assets/content-fragments/content-fragments-variations.md) insieme ai relativi elementi, varianti, contenuti e metadati associati.

* **Pubblicazione rapida**
* **Gestisci pubblicazione**
* **Gestisci i tag**
* **Alla raccolta**
* **Copia**  (e  **Incolla**)
* **Sposta**
* **Elimina**

>[!NOTE]
>
>Molte di queste sono azioni [standard per Assets](/help/assets/manage-digital-assets.md) e/o l’ [AEM app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=it).

## Apertura dell’editor frammenti {#opening-the-fragment-editor}

Per aprire il frammento per la modifica:

>[!CAUTION]
>
>Per modificare un frammento di contenuto è necessario disporre delle [autorizzazioni appropriate](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). In caso di problemi, contatta l’amministratore di sistema.

>[!CAUTION]
>
>Per modificare un frammento di contenuto è necessario disporre delle autorizzazioni appropriate. In caso di problemi, contatta l’amministratore di sistema.

1. Utilizza la console **Risorse** per accedere alla posizione del frammento di contenuto.
1. Apri il frammento per la modifica:

   * Tocca o fai clic sul collegamento frammento o frammento (a seconda della vista della console).
   * Selezionando il frammento, quindi **Modifica** dalla barra degli strumenti.

1. Viene aperto l’editor frammenti. Apporta le modifiche necessarie:

   ![editor frammenti](assets/cfm-managing-03.png)

1. Dopo aver apportato le modifiche, utilizza **Salva e chiudi** o **Annulla** come necessario.

   >[!NOTE]
   >
   >Sia **Salva e chiudi** che **Annulla** usciranno dall&#39;editor. Per informazioni complete sul funzionamento di entrambe le opzioni per i frammenti di contenuto, consulta [Salva, Annulla e Versioni](#save-cancel-and-versions) .

## Modalità e azioni nell’Editor frammento di contenuto {#modes-actions-content-fragment-editor}

Sono disponibili varie modalità e azioni dall’Editor frammento di contenuto.

### Modalità nell’ Editor frammento di contenuto {#modes-in-the-content-fragment-editor}

Naviga tra le varie modalità utilizzando le icone nel pannello laterale:

* Variazioni: [Modifica del contenuto](#editing-the-content-of-your-fragment) e [Gestione delle varianti](#creating-and-managing-variations-within-your-fragment)

* [Annotazioni](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Contenuto associato](#associating-content-with-your-fragment)
* [Metadati](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [Albero struttura](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [Anteprima](/help/assets/content-fragments/content-fragments-json-preview.md)

![modalità](assets/cfm-managing-04.png)

### Azioni barra degli strumenti nell’ Editor frammento di contenuto {#toolbar-actions-in-the-content-fragment-editor}

Alcune funzioni nella barra degli strumenti superiore sono disponibili in diverse modalità:

![modalità](assets/cfm-managing-top-toolbar.png)

* Se in una pagina di contenuto è già presente un riferimento al frammento, viene visualizzato un messaggio. Puoi **Chiudere** il messaggio.

* Il pannello laterale può essere nascosto o visualizzato utilizzando l&#39;icona **Attiva/Disattiva pannello laterale** .

* Sotto il nome del frammento è possibile visualizzare il nome del [modello di frammento di contenuto](/help/assets/content-fragments/content-fragments-models.md) utilizzato per creare il frammento corrente:

   * Il nome è anche un collegamento che aprirà l&#39;editor modelli.

* Vedere lo stato del frammento; ad esempio, informazioni su quando è stato creato, modificato o pubblicato. Lo stato viene inoltre codificato in base al colore:

   * **Nuovo**: grigio
   * **Bozza**: blu
   * **Pubblicato**: verde
   * **Modificato**: arancia
   * **Disattivato**: rosso

* I tre punti (**...L’elenco a discesa** consente di accedere ad azioni aggiuntive:
   * **[Pubblicazione rapida](#publishing-and-referencing-a-fragment)**
   * **[Gestisci pubblicazione](#publishing-and-referencing-a-fragment)**

## Salva, Annulla e Versioni {#save-cancel-and-versions}

>[!NOTE]
>
>Le versioni possono anche essere [create, confrontate e ripristinate dalla Timeline](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

L’editor dispone di due opzioni:

* **Salva**

   Salva le modifiche più recenti e chiude l’editor.

   >[!CAUTION]
   >
   >Per modificare un frammento di contenuto è necessario disporre delle [autorizzazioni appropriate](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). In caso di problemi, contatta l’amministratore di sistema.

   >[!NOTE]
   >
   >È possibile rimanere nell&#39;editor, apportando una serie di modifiche, prima di selezionare **Salva**.

   >[!CAUTION]
   >
   >Oltre a salvare semplicemente le modifiche, **Salva** aggiorna anche tutti i riferimenti e assicura che il Dispatcher venga scaricato come necessario. L’elaborazione di queste modifiche può richiedere del tempo. Per questo motivo, può esserci un impatto sulle prestazioni su un sistema di grandi dimensioni/complesso/pesantemente caricato.
   >
   >
   >Tieni presente questo aspetto quando utilizzi **Salva** e poi accedi rapidamente all’editor frammenti per apportare e salvare ulteriori modifiche.

* **Annulla**

   Uscirà dall’editor senza salvare le modifiche più recenti.

Durante la modifica del frammento di contenuto AEM crea automaticamente delle versioni per garantire che il contenuto precedente possa essere ripristinato se si **Annulla** apportano modifiche:

1. Quando un frammento di contenuto viene aperto per la modifica AEM verifica l’esistenza del token basato su cookie che indica se esiste una *sessione di modifica*:

   1. Se viene trovato il token, il frammento viene considerato parte della sessione di modifica esistente.
   2. Se il token è *non* disponibile e l’utente inizia a modificare il contenuto, viene creata una versione e viene inviato un token per questa nuova sessione di modifica al client, dove viene salvato in un cookie.

2. In presenza di una sessione di modifica *attiva*, il contenuto in fase di modifica viene salvato automaticamente ogni 600 secondi (impostazione predefinita).

   >[!NOTE]
   >
   >L&#39;intervallo di salvataggio automatico è configurabile utilizzando il meccanismo `/conf`.
   >
   >Valore predefinito, vedi:
   >  `/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. Se l&#39;utente seleziona **Annulla** la modifica, la versione creata all&#39;inizio della sessione di modifica viene ripristinata e il token viene rimosso per terminare la sessione di modifica.
4. Se l’utente seleziona **Salva** le modifiche, gli elementi/le varianti aggiornati vengono mantenuti e il token viene rimosso per terminare la sessione di modifica.

## Modifica del contenuto del frammento {#editing-the-content-of-your-fragment}

Dopo aver aperto il frammento, puoi utilizzare la scheda [Variazioni](/help/assets/content-fragments/content-fragments-variations.md) per creare i contenuti.

## Creazione e gestione di varianti all’interno del frammento {#creating-and-managing-variations-within-your-fragment}

Dopo aver creato il contenuto principale, puoi creare e gestire [Variazioni](/help/assets/content-fragments/content-fragments-variations.md) di tale contenuto.

## Associazione di contenuto al frammento {#associating-content-with-your-fragment}

È inoltre possibile [associare il contenuto](/help/assets/content-fragments/content-fragments-assoc-content.md) a un frammento. Questa funzione consente di collegare in modo che le risorse (ad esempio le immagini) possano essere (facoltativamente) utilizzate con il frammento quando viene aggiunto a una pagina di contenuto.

## Visualizzazione e modifica dei metadati (proprietà) del frammento {#viewing-and-editing-the-metadata-properties-of-your-fragment}

È possibile visualizzare e modificare le proprietà di un frammento utilizzando la scheda [Metadati](/help/assets/content-fragments/content-fragments-metadata.md) .

## Timeline per i frammenti di contenuto {#timeline-for-content-fragments}

Oltre alle opzioni standard, [Timeline](/help/assets/manage-digital-assets.md#timeline) fornisce sia informazioni che azioni specifiche per i frammenti di contenuto:

* Visualizza informazioni su versioni, commenti e annotazioni
* Azioni per le versioni

   * **[Ripristina questa versione](#reverting-to-a-version)**  (seleziona un frammento esistente e quindi una versione specifica)

   * **[Confronta con corrente](#comparing-fragment-versions)**  (seleziona un frammento esistente, quindi una versione specifica)

   * Aggiungi un **Etichetta** e/o **Commento** (seleziona un frammento esistente, quindi una versione specifica)

   * **Salva come versione**  (seleziona un frammento esistente, quindi la freccia su nella parte inferiore della timeline)

* Azioni per le annotazioni

   * **Elimina**

>[!NOTE]
I commenti sono:
* Funzionalità standard per tutte le risorse
* Made in Timeline
* Correlato alla risorsa frammento

Le annotazioni (per i frammenti di contenuto) sono:
* Inserito nell’editor frammenti
* Specifica per un segmento di testo selezionato all’interno del frammento



Esempio:

![timeline](assets/cfm-managing-05.png)

## Confronto delle versioni dei frammenti {#comparing-fragment-versions}

L&#39;azione **Confronta con corrente** è disponibile dalla [Timeline](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) dopo aver selezionato una versione specifica.

Verrà aperto:

* la versione **Corrente** (più recente) (a sinistra)

* la versione selezionata **v&lt;*x.y*>** (a destra)

Vengono visualizzati uno accanto all’altro, dove:

* Eventuali differenze sono evidenziate

   * Testo eliminato - rosso
   * Testo inserito - verde
   * Testo sostituito - blu

* L’icona a schermo intero consente di aprire una delle due versioni da sola; quindi torna alla vista parallela
* È possibile **Ripristinare** alla versione specifica
* **** Verrai reindirizzato alla console

>[!NOTE]
Non è possibile modificare il contenuto del frammento quando si confrontano i frammenti.

![confronto](assets/cfm-managing-06.png)

## Ripristino di una versione {#reverting-to-a-version}

È possibile ripristinare una versione specifica del frammento:

* Direttamente dalla [Timeline](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

   Seleziona la versione richiesta, quindi l&#39;azione **Ripristina questa versione** .

* Mentre [confronta una versione con la versione corrente](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) puoi **Ripristinare** la versione selezionata.

## Pubblicazione e riferimento a un frammento {#publishing-and-referencing-a-fragment}

>[!CAUTION]
Se il frammento è basato su un modello, assicurati che il modello [sia stato pubblicato](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model).
Se pubblichi un frammento di contenuto per il quale il modello non è ancora stato pubblicato, un elenco di selezione lo indicherà e il modello verrà pubblicato con il frammento.

I frammenti di contenuto devono essere pubblicati per l’utilizzo nell’ambiente di pubblicazione. Possono essere pubblicati:

* Dopo la creazione; utilizzando le azioni [disponibili nella console Assets](#actions-for-a-content-fragment-assets-console).
* Dall’ [Editor frammento di contenuto](#toolbar-actions-in-the-content-fragment-editor).
* Quando si [pubblica una pagina che utilizza il frammento](/help/sites-cloud/authoring/fundamentals/content-fragments.md#publishing); il frammento viene elencato nei riferimenti di pagina.

>[!CAUTION]
Dopo la pubblicazione e/o il riferimento a un frammento, AEM un avviso quando un autore riapre il frammento per la modifica. In questo modo si avverte che le modifiche al frammento avranno effetto anche sulle pagine a cui si fa riferimento.

## Eliminazione di un frammento {#deleting-a-fragment}

Per eliminare un frammento:

1. Nella console **Risorse** individua la posizione del frammento di contenuto.
2. Selezionare il frammento.

   >[!NOTE]
   L&#39;azione **Elimina** non è disponibile come azione rapida.

3. Seleziona **Elimina** dalla barra degli strumenti.
4. Conferma l’azione **Elimina**.

   >[!CAUTION]
   Se in una pagina è già presente un riferimento al frammento, verrà visualizzato un messaggio di avviso e sarà necessario confermare che si desidera procedere con **Forza eliminazione**. Il frammento, insieme al relativo componente di frammento di contenuto, verrà eliminato da tutte le pagine di contenuto.
