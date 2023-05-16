---
title: Gli schemi di metadati definiscono il layout della pagina delle proprietà dei metadati
description: Lo schema metadati definisce il layout della pagina delle proprietà e le proprietà dei metadati visualizzate per le risorse. Scopri come creare uno schema di metadati personalizzato, modificare lo schema di metadati e applicare lo schema di metadati alle risorse.
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: 9e94afeb-1c54-4653-bf52-b0910c0cb6c1
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '2642'
ht-degree: 9%

---

# Schemi di metadati {#metadata-schemas}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/metadata-schemas.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

Le organizzazioni hanno a disposizione un modello di metadati che migliora l’individuazione delle risorse, l’utilizzo, l’interoperabilità e così via. La correzione dell&#39;applicazione dei metadati è sacrosanta per mantenere flussi di lavoro e processi basati su metadati. Per aderire alla strategia e agli standard dei metadati a livello aziendale, puoi utilizzare schemi di metadati che aiutano gli utenti DAM ad allinearsi. [!DNL Adobe Experience Manager] consente di creare, gestire e applicare schemi di metadati in modo semplice e flessibile.

In [!DNL Adobe Experience Manager Assets], gli schemi contengono campi specifici per informazioni specifiche da compilare. Contiene inoltre informazioni sul layout per visualizzare i campi di metadati in modo semplice e intuitivo. Le proprietà dei metadati includono titolo, descrizione, tipi MIME, tag e altro ancora. È possibile utilizzare [!UICONTROL Forms schema metadati] per modificare gli schemi esistenti o aggiungere schemi di metadati personalizzati.

Per visualizzare e modificare la pagina delle proprietà di una risorsa, effettua le seguenti operazioni:

1. Fai clic sul pulsante **[!UICONTROL Visualizza proprietà]** dalle azioni rapide sulla porzione di risorsa nella vista a schede. In alternativa, seleziona una risorsa e fai clic su **[!UICONTROL Proprietà]** ![visualizza proprietà](assets/do-not-localize/info-circle-icon.png) dalla barra degli strumenti.

1. Puoi modificare le varie proprietà dei metadati modificabili nelle schede disponibili. Tuttavia, non è possibile modificare la risorsa [!UICONTROL Tipo] in [!UICONTROL Base] scheda della pagina delle proprietà.

   ![Scheda di base Proprietà risorsa, in cui il tipo di risorsa non può essere modificato](assets/asset-properties-basic-tab.png)

   *Figura: Scheda Base sulla risorsa [!UICONTROL Proprietà].*

   Per modificare il tipo MIME di una risorsa, utilizza un modulo schema metadati personalizzato o modifica un modulo esistente. Vedi [Modifica Forms schema metadati](#edit-metadata-schema-forms) per ulteriori informazioni. Se modifichi lo schema metadati di un tipo MIME, il layout della pagina delle proprietà per le risorse e tutti i sottotipi vengono modificati. Ad esempio, per modificare uno schema jpeg in `default/image` modifica solo il layout dei metadati (proprietà delle risorse) per le risorse con tipo MIME `image/jpeg`. Tuttavia, se modifichi lo schema predefinito, le modifiche apportate modificheranno il layout dei metadati per tutti i tipi di risorse.

## Moduli schema metadati {#default-metadata-schema-forms}

Per visualizzare un elenco di moduli o modelli, in [!DNL Experience Manager] interfaccia passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Schemi metadati]**.

[!DNL Experience Manager] fornisce i seguenti modelli di modulo schema metadati.

| Modelli |  | Descrizione |
|---|---|---|
| [!UICONTROL impostazione predefinita] |  | Il modulo schema metadati di base per le risorse. |
|  | I seguenti moduli secondari ereditano le proprietà di [!UICONTROL default] modulo: |  |
|  | <ul><li>[!UICONTROL dm_video]</li></ul> | Modulo schema per video Dynamic Media. |
|  | <ul><li>[!UICONTROL immagine]</li></ul> | Modulo schema per immagini con tipo MIME, ad esempio `image/jpeg` e `image/png`. <br> La [!UICONTROL immagine] Il modulo presenta i seguenti modelli di modulo figlio: <ul><li> [!UICONTROL jpeg]: Modulo schema per risorse con sottotipo [!UICONTROL jpeg].</li> <li>[!UICONTROL sciocco]: Modulo schema per le risorse con TIFF di sottotipo.</li></ul> |
|  | <ul><li>[!UICONTROL applicazione]</li></ul> | Modulo schema per risorse con tipo MIME, ad esempio `application/pdf` e `application/zip`. <br>[!UICONTROL pdf]: Modulo schema per risorse con PDF di sottotipo. |
|  | <ul><li>[!UICONTROL video]</li></ul> | Modulo di schema per le risorse video con tipo MIME, ad esempio `video/avi` e `video/mp4`. |
| [!UICONTROL raccolta] |  | Modulo schema per le raccolte. |
| [!UICONTROL contentfragment] |  | modulo schema per frammenti di contenuto. |
| [!UICONTROL forms] |  | Questo modulo schema si riferisce a [!DNL Adobe Experience Manager Forms]. |
| [!UICONTROL ugc_contentfragment] |  | Modulo di schema per elementi di contenuto generati dall’utente e risorse integrate in Experience Manager dai social media. |

>[!NOTE]
>
>Per visualizzare i moduli secondari di un modulo schema, fare clic sul nome del modulo schema.

## Aggiungere un modulo schema metadati {#add-a-metadata-schema-form}

Per aggiungere un modulo schema metadati, effettua le seguenti operazioni:

1. Per aggiungere un modello personalizzato all’elenco, fai clic su **[!UICONTROL Crea]** dalla barra degli strumenti.

   >[!NOTE]
   >
   >Viene visualizzato un simbolo di blocco con i modelli non modificati. Se si personalizza un modello, questo non viene bloccato ![serratura chiusa](assets/do-not-localize/lock_closed_icon.svg).

1. Nella finestra di dialogo, fornisci il titolo del modulo schema e fai clic su **[!UICONTROL Crea]** per completare il processo di creazione del modulo.

## Modifica dei moduli schema metadati {#edit-metadata-schema-forms}

È possibile modificare un modulo schema metadati appena aggiunto o esistente. Il modulo schema metadati include schede ed elementi modulo all’interno di schede. Puoi mappare/configurare questi elementi del modulo su un campo all’interno di un nodo di metadati nell’archivio CRX. È possibile aggiungere schede o elementi modulo al modulo schema metadati. Le schede e gli elementi del modulo derivati dall&#39;elemento padre sono nello stato bloccato. Non è possibile modificarli a livello di bambino.

1. Sulla [!UICONTROL Forms schema metadati] , seleziona un modulo e fai clic su **[!UICONTROL Modifica]** nella barra degli strumenti.

1. Sulla **[!UICONTROL Editor moduli schema metadati]** personalizzare il modulo metadati. Trascina i componenti necessari dalla sezione **[!UICONTROL Crea modulo]** in una delle schede.

   ![Editor schema metadati per personalizzare la pagina Proprietà risorsa](assets/metadata-schema-editor.png)

   *Figura: A [!UICONTROL Editor moduli schema metadati] con le schede disponibili.*

1. Per configurare un componente, selezionalo e modificane le proprietà nel **[!UICONTROL Impostazioni]** scheda .

### Componenti all’interno di [!UICONTROL Crea modulo] scheda {#components-within-the-build-form-tab}

La **[!UICONTROL Crea modulo]** elenca gli elementi del modulo utilizzati nel modulo schema. La **[!UICONTROL Impostazioni]** fornisce gli attributi di ogni elemento selezionato nella scheda **[!UICONTROL Crea modulo]** scheda . Nella tabella seguente sono elencati gli elementi del modulo disponibili nel **[!UICONTROL Crea modulo]** scheda:

| Nome componente | Descrizione |
| -------------------------------- | ----------------------------------------------------------------------------------- |
| [!UICONTROL Intestazione sezione] | Aggiungi un’intestazione di sezione per un elenco di componenti comuni. |
| [!UICONTROL Testo su riga singola] | Aggiungi una proprietà di testo a riga singola. Viene memorizzato come stringa. |
| [!UICONTROL Testo con più valori] | Aggiungi una proprietà di testo con più valori. Viene memorizzato come array di stringhe. |
| [!UICONTROL Numero] | Aggiungi un componente numerico. |
| [!UICONTROL Data] | Aggiungi un componente data . |
| [!UICONTROL A discesa] | Aggiungi un elenco a discesa. |
| [!UICONTROL Tag standard] | Aggiungi un tag. |
| [!UICONTROL Tag avanzati] | Aggiungi per migliorare le funzionalità di ricerca aggiungendo automaticamente tag di metadati. |
| [!UICONTROL Campo nascosto] | Aggiungi un campo nascosto. Viene inviato come parametro POST al momento del salvataggio della risorsa. |
| [!UICONTROL Risorsa con riferimento da] | Aggiungi questo componente per visualizzare l’elenco delle risorse a cui fa riferimento la risorsa. |
| [!UICONTROL Risorsa con riferimento a] | Aggiungi per visualizzare un elenco di risorse che fanno riferimento alla risorsa. |
| [!UICONTROL Riferimenti sui prodotti] | Aggiungi per visualizzare l’elenco dei prodotti collegati alla risorsa. |
| [!UICONTROL Metadati contestuali] | Aggiungi per controllare la visualizzazione di altre schede di metadati nella pagina delle proprietà delle risorse. |

<!-- TBD: Ratings are not available in Experience Manager as a Cloud Service. Removed via cqdoc-18089 ticket. 
| [!UICONTROL Asset Rating]        | Add to display options for rating the asset.                                       |
-->

#### Modifica del componente metadati {#edit-the-metadata-component}

Per modificare le proprietà di un componente metadati sul modulo, fai clic sul componente per modificare tutte o un sottoinsieme delle seguenti proprietà nel **[!UICONTROL Impostazioni]** scheda . È consigliabile mappare un solo campo a una determinata proprietà nello schema metadati. In caso contrario, il sistema seleziona il campo aggiunto più recente mappato alla proprietà.

**Etichetta campo**: Nome della proprietà di metadati visualizzata nella pagina delle proprietà della risorsa.

**Mappa su proprietà**: Questa proprietà specifica il percorso relativo o il nome del nodo della risorsa in cui viene salvato nell&#39;archivio CRX. Inizia con `./` per indicare che il percorso si trova sotto il nodo della risorsa.

Di seguito sono riportati alcuni esempi di valori validi per una proprietà:

* `./jcr:content/metadata/dc:title`: memorizza il valore come proprietà nel nodo di metadati della risorsa `dc:title`.

* `./jcr:created`: Memorizza la data e l’ora di creazione di una risorsa. È una proprietà protetta. Se configuri queste proprietà, Adobe consiglia di contrassegnarle come Disabilita modifica. In caso contrario, al momento di salvare le proprietà della risorsa si verifica l’errore “Impossibile modificare le risorse”.

Per garantire che il componente sia visualizzato correttamente nel modulo schema metadati, il percorso della proprietà non deve includere spazi.

* **Segnaposto**: Utilizzare questa proprietà per specificare il testo segnaposto pertinente relativo alla proprietà metadati.
* **Obbligatorio**: Utilizzare questa proprietà per contrassegnare una proprietà di metadati come obbligatoria nella pagina delle proprietà.
* **Disattiva modifica**: Utilizzare questa proprietà per non consentire alcuna modifica a una proprietà nella pagina delle proprietà.
* **Mostra campo vuoto in sola lettura**: Contrassegna questa proprietà per visualizzare una proprietà di metadati nella pagina delle proprietà anche se non ha valore. Per impostazione predefinita, quando una proprietà di metadati non ha alcun valore, non viene elencata nella pagina delle proprietà.
* **Mostra elenco ordinato**: Utilizzare questa proprietà per visualizzare un elenco ordinato di scelte.
* **Scelte**: Utilizzare questa proprietà per specificare le scelte in un elenco.
* **Descrizione** : Utilizza questa proprietà per aggiungere una breve descrizione per il componente metadati.
* **Classe**: Classe oggetto a cui è associata la proprietà.
* **Elimina**: Fai clic su [!UICONTROL Elimina] per eliminare un componente dal modulo schema.

>[!NOTE]
>
>La [!UICONTROL Campo nascosto] Il componente non include questi attributi. ma include proprietà quali Nome, Valore, Etichetta campo e Descrizione. I valori per il componente Campo nascosto vengono inviati come parametro POST ogni volta che la risorsa viene salvata. Non viene salvato come metadati per la risorsa.

Se selezioni l’opzione **[!UICONTROL Obbligatorio]**, puoi cercare le risorse per le quali mancano i metadati obbligatori. Dal pannello **[!UICONTROL Filtri]**, espandi il predicato **[!UICONTROL Convalida metadati]** e seleziona l’opzione **[!UICONTROL Non valido]**. Nei risultati della ricerca vengono visualizzate le risorse per le quali mancano i metadati obbligatori, che sono stati configurati dal modulo schema.

Se aggiungi il componente Metadati contestuali a una qualsiasi scheda di qualsiasi modulo di schema, il componente viene visualizzato come un elenco nella pagina delle proprietà delle risorse a cui viene applicato lo schema specifico. L’elenco include tutte le altre schede eccetto la scheda a cui è stato applicato il componente Metadati contestuali . Attualmente, questa funzione fornisce funzionalità di base per controllare la visualizzazione dei metadati in base al contesto.

Per visualizzare una scheda nella pagina delle proprietà oltre alla scheda in cui è applicato il componente Metadati contestuali , selezionala dall’elenco. La scheda viene aggiunta alla pagina delle proprietà.

### Specificare le proprietà nel file JSON {#specify-properties-in-json-file}

Invece di specificare le proprietà delle opzioni nella scheda **[!UICONTROL Impostazioni]**, puoi definire le opzioni in un file JSON, specificando le coppie chiave-valore corrispondenti. Nel campo **[!UICONTROL Percorso JSON]**, specifica il percorso del file JSON.

#### Aggiunta o eliminazione di una scheda nel modulo schema {#add-delete-a-tab-in-the-schema-form}

L’editor dello schema consente di aggiungere o eliminare una scheda. Il modulo schema predefinito include **[!UICONTROL Base]**, **[!UICONTROL Avanzate]** , **[!UICONTROL IPTC]** e **[!UICONTROL Estensione IPTC]** schede.

![Schede predefinite nel modulo Schema metadati](assets/metadata-schema-form-tabs.png)

Fai clic su `+` per aggiungere una scheda a un modulo schema. Per impostazione predefinita, la nuova scheda ha il nome `Unnamed-1`. Puoi modificare il nome dalla **[!UICONTROL Impostazioni]** scheda . Fai clic su `X` per eliminare una scheda.

![Aggiunta o eliminazione di una scheda tramite l’Editor schema metadati](assets/metadata-schema-form-new-tab.png)

## Eliminare i moduli schema metadati {#deleting-metadata-schema-forms}

Experience Manager consente di eliminare solo i moduli schema personalizzati. Non consente di eliminare i moduli/modelli di schema predefiniti. Tuttavia, è possibile eliminare qualsiasi modifica personalizzata in questi moduli.

Per eliminare un modulo, selezionarlo e fare clic sull’icona Elimina.

>[!NOTE]
>
>Dopo aver eliminato le modifiche personalizzate a un modulo predefinito, l’icona a forma di lucchetto viene visualizzata nuovamente prima di essere visualizzata nell’interfaccia Schema metadati per indicare che il modulo è tornato allo stato predefinito.

>[!NOTE]
>
>* Dopo aver eliminato le modifiche personalizzate a un modulo predefinito, il blocco ![serratura chiusa](assets/do-not-localize/lock_closed_icon.svg) viene visualizzata nuovamente prima del modulo. Indica che il modulo viene ripristinato allo stato predefinito.
>* Non è possibile eliminare i moduli schema metadati predefiniti in [!DNL Assets].


## Moduli schema per tipi MIME {#schema-forms-for-mime-types}

[!DNL Experience Manager] fornisce moduli predefiniti per vari tipi MIME predefiniti. Tuttavia, puoi aggiungere moduli personalizzati per risorse di vari tipi MIME.

### Aggiungere nuovi moduli per i tipi MIME {#adding-new-forms-for-mime-types}

Creare un modulo con il tipo appropriato. Ad esempio, per aggiungere un modello per `image/png` sottotipo, creare il modulo sotto i moduli &quot;immagine&quot;. Il titolo del modulo schema è il nome del sottotipo. In questo caso, il titolo è `png`.

#### Utilizza un modello di schema esistente per vari tipi MIME {#use-an-existing-schema-template-for-various-mime-types}

Puoi utilizzare un modello esistente per un tipo MIME diverso. Ad esempio, utilizza `image/jpeg` modulo per le risorse di tipo MIME `image/png`.

In questo caso, crea un nodo in `/etc/dam/metadataeditor/mimetypemappings` nell’archivio CRX. Specifica un nome per il nodo e definisci le seguenti proprietà:

| Nome | Descrizione | Tipo | Valore |
|------|-------------|------|-------|
| `exposedmimetype` | Nome del modulo esistente da mappare | `String` | `image/jpeg` |
| `mimetypes` | Elenco dei tipi MIME che utilizzano il modulo definito in `exposedmimetype` attributo | `String` | `image/png` |

[!DNL Assets] mappa i seguenti tipi MIME e moduli di schema:

| Modulo schema | Tipi MIME |
|---|---|
| image/jpeg | image/pjpeg |
| image/tiff | image/x-tiff |
| application/pdf | application/postscript |
| application/x-ImageSet | Multipart/Related; type=application/x-ImageSet |
| application/x-SpinSet | Multipart/Related; type=application/x-SpinSet |
| application/x-MixedMediaSet | Multipart/Related; type=application/x-MixedMediaSet |
| video/quicktime | video/x-quicktime |
| video/mpeg4 | video/mp4 |
| video/avi | video/avi, video/msvideo, video/x-msvideo |
| video/wmv | video/x-ms-wmv |
| video/flv | video/x-flv |

## Concedere l’accesso agli schemi di metadati {#grant-access-to-metadata-schemas}

La funzione Schema metadati è disponibile solo per gli amministratori. Tuttavia, gli amministratori possono fornire l&#39;accesso ai non amministratori modificando alcune autorizzazioni. Fornisci agli utenti non amministratori le autorizzazioni di creazione, modifica ed eliminazione per `/conf` cartella.

## Applicare metadati specifici per le cartelle {#applying-folder-specific-metadata}

[!DNL Assets] consente di definire una variante di uno schema di metadati e di applicarlo a una cartella specifica.

Ad esempio, puoi definire una variante dello schema metadati predefinito e applicarlo a una cartella. Quando si applica lo schema modificato, questo sostituisce lo schema metadati predefinito originale applicato alle risorse all’interno della cartella.

Solo le risorse caricate nella cartella a cui viene applicato lo schema sono conformi ai metadati modificati definiti nello schema dei metadati della variante. [!DNL Assets] in altre cartelle in cui lo schema originale viene applicato continuano a essere conformi ai metadati definiti nello schema originale.

L’ereditarietà dei metadati da parte delle risorse si basa sullo schema applicato alla cartella di livello superiore nella gerarchia. Lo stesso schema viene applicato o ereditato dalle sottocartelle. Se a livello di sottocartella viene applicato uno schema diverso, l’ereditarietà si interrompe.

1. In [!DNL Experience Manager] interfaccia, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Schemi metadati]**. Viene visualizzata la pagina **[!UICONTROL Moduli schema metadati]**.
1. Selezionare la casella di controllo prima di un modulo, ad esempio il modulo metadati predefinito, quindi fare clic sul pulsante **[!UICONTROL Copia]** e salvarlo come modulo personalizzato. Specifica un nome personalizzato per il modulo, ad esempio `my_default`. In alternativa, è possibile creare un modulo personalizzato.

1. In **[!UICONTROL Forms schema metadati]** , seleziona la `my_default` modulo, quindi fare clic su **[!UICONTROL Modifica]**.
1. In **[!UICONTROL Editor schema metadati]** aggiungere un campo di testo al modulo schema. Ad esempio, aggiungi un campo con l’etichetta **[!UICONTROL Categoria]**.
1. Fai clic su **[!UICONTROL Salva]**. Il modulo modificato è elencato nella **[!UICONTROL Forms schema metadati]** pagina.
1. Tocca o fai clic **[!UICONTROL Applica a cartelle]** dalla barra degli strumenti per applicare i metadati personalizzati a una cartella.
1. Seleziona la cartella in cui applicare lo schema modificato, quindi tocca o fai clic su **[!UICONTROL Applica]**.
1. Se alla cartella è stato applicato lo schema di altri metadati, viene visualizzato un messaggio di avviso che informa che lo schema di metadati esistente sta per essere sovrascritto. Fai clic su **Sovrascrittura**.
1. Fai clic su **OK** per chiudere il messaggio di successo.
1. Passa alla cartella alla quale hai applicato lo schema di metadati modificato.

## Definizione dei metadati obbligatori {#defining-mandatory-metadata}

Puoi definire campi obbligatori a livello di cartella, che vengono applicati alle risorse caricate nella cartella. Se carichi risorse con metadati mancanti per i campi obbligatori definiti in precedenza, nella vista Scheda viene visualizzata un’indicazione visiva dei metadati mancanti sulle risorse.

>[!NOTE]
>
>Un campo di metadati può essere definito obbligatorio in base al valore di un altro campo. Nella vista Schede, in Experience Manager non viene visualizzato il messaggio di avviso relativo ai metadati mancanti per tali campi di metadati obbligatori.

1. Fai clic sul logo dell’Experience Manager, quindi passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Schemi metadati]**. Viene visualizzata la pagina **[!UICONTROL Moduli schema metadati]**.
1. Salvare il modulo metadati predefinito come modulo personalizzato. Ad esempio, salvalo con nome `my_default`.
1. Modificare il modulo personalizzato. Aggiungi un campo obbligatorio. Ad esempio, aggiungi un **[!UICONTROL Categoria]** e rendere il campo obbligatorio.
1. Fai clic su **[!UICONTROL Salva]**. Il modulo modificato è elencato nella **[!UICONTROL Forms schema metadati]** pagina. Seleziona il modulo e tocca o fai clic su **[!UICONTROL Applica a cartelle]** dalla barra degli strumenti per applicare i metadati personalizzati a una cartella.
1. Passa alla cartella e carica alcune risorse con metadati mancanti per il campo obbligatorio aggiunto al modulo personalizzato. Nella vista Scheda della risorsa viene visualizzato un messaggio per i metadati mancanti per il campo obbligatorio.
1. (Facoltativo) Accesso `https://[server]:[port]/system/console/components/`. Configura e abilita `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` componente disattivato per impostazione predefinita. Imposta una frequenza con cui l’Experience Manager controlla la validità dei metadati sulle risorse.

   Questa configurazione aggiunge una proprietà `hasValidMetadata` a `jcr:content` delle attività. Utilizzando questa proprietà, Experience Manager può filtrare i risultati in una ricerca.

   >[!NOTE]
   >
   >Se una risorsa viene aggiunta dopo il controllo pianificato, la risorsa non viene contrassegnata con `hasValidMetadata` fino al controllo pianificato successivo. Le risorse non vengono visualizzate nei risultati di ricerca intermedi.

   >[!CAUTION]
   >
   >I controlli di convalida dei metadati richiedono molte risorse e possono influire sulle prestazioni del sistema. Pianifica i controlli di conseguenza. Se il server non è in grado di gestire il carico, provare a disabilitare questo processo

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cercare risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco di metadati](metadata-import-export.md)
