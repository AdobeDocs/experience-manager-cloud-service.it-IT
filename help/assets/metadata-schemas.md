---
title: Gli schemi di metadati definiscono il layout della pagina delle proprietà dei metadati
description: Lo schema metadati definisce il layout della pagina delle proprietà e le proprietà dei metadati visualizzate per le risorse. Scopri come creare uno schema di metadati personalizzato, modificare lo schema di metadati e applicare uno schema di metadati alle risorse.
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: 9e94afeb-1c54-4653-bf52-b0910c0cb6c1
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '2627'
ht-degree: 9%

---

# Schemi metadati {#metadata-schemas}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/metadata-schemas.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

Le organizzazioni propongono un modello di metadati che migliora l’individuazione delle risorse, l’utilizzo, l’interoperabilità e così via. L’applicazione corretta dei metadati è indispensabile per mantenere i flussi di lavoro e i processi basati sui metadati. Per rispettare la strategia e gli standard per i metadati a livello di organizzazione, puoi utilizzare schemi di metadati che consentono agli utenti DAM di allinearsi. [!DNL Adobe Experience Manager] consente di creare, gestire e applicare schemi di metadati in modo semplice e flessibile.

In entrata [!DNL Adobe Experience Manager Assets], gli schemi contengono campi specifici per informazioni specifiche da compilare. Contiene inoltre informazioni di layout per visualizzare i campi di metadati in modo semplice e intuitivo. Le proprietà dei metadati includono titolo, descrizione, tipi MIME, tag e altro ancora. È possibile utilizzare [!UICONTROL Forms schema metadati] per modificare gli schemi esistenti o aggiungere schemi di metadati personalizzati.

Per visualizzare e modificare la pagina delle proprietà di una risorsa, effettua le seguenti operazioni:

1. Fai clic su **[!UICONTROL Visualizza proprietà]** nella vista a schede. In alternativa, seleziona una risorsa e fai clic su **[!UICONTROL Proprietà]** ![visualizza proprietà](assets/do-not-localize/info-circle-icon.png) dalla barra degli strumenti.

1. Puoi modificare le varie proprietà dei metadati modificabili nelle schede disponibili. Tuttavia, non puoi modificare la risorsa [!UICONTROL Tipo] nel [!UICONTROL Base] scheda della pagina delle proprietà.

   ![Scheda di base delle proprietà della risorsa, in cui il tipo di risorsa non può essere modificato](assets/asset-properties-basic-tab.png)

   *Figura: scheda Base della risorsa [!UICONTROL Proprietà].*

   Per modificare il tipo MIME di una risorsa, utilizza un modulo schema metadati personalizzato o modifica un modulo esistente. Consulta [Modifica Forms schema metadati](#edit-metadata-schema-forms) per ulteriori informazioni. Se modifichi lo schema metadati di un tipo MIME, viene modificato il layout della pagina delle proprietà per le risorse e tutti i sottotipi. Ad esempio, la modifica di uno schema jpeg in `default/image` modifica solo il layout dei metadati (proprietà risorsa) per le risorse di tipo MIME `image/jpeg`. Tuttavia, se modifichi lo schema predefinito, le modifiche modificano il layout dei metadati per tutti i tipi di risorse.

## Moduli schema metadati {#default-metadata-schema-forms}

Per visualizzare un elenco di moduli o modelli, in [!DNL Experience Manager] interfaccia passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Schemi metadati]**.

[!DNL Experience Manager] fornisce i seguenti modelli di modulo schema metadati.

| Modelli | | Descrizione |
|---|---|---|
| [!UICONTROL predefinito] | | Modulo schema metadati di base per le risorse. |
| | I seguenti moduli figlio ereditano le proprietà del [!UICONTROL predefinito] forma: | |
| | <ul><li>[!UICONTROL dm_video]</li></ul> | Modulo schema per video Dynamic Medie. |
| | <ul><li>[!UICONTROL immagine]</li></ul> | Modulo schema per immagini con tipo MIME, ad esempio `image/jpeg` e `image/png`. <br> Il [!UICONTROL immagine] il modulo include i seguenti modelli di modulo figlio: <ul><li> [!UICONTROL jpeg]: modulo schema per le risorse con sottotipo [!UICONTROL jpeg].</li> <li>[!UICONTROL tiff]: modulo schema per le risorse con sottotipo TIFF.</li></ul> |
| | <ul><li>[!UICONTROL applicazione]</li></ul> | Modulo schema per risorse di tipo MIME, ad esempio `application/pdf` e `application/zip`. <br>[!UICONTROL pdf]: modulo schema per le risorse con sottotipo PDF. |
| | <ul><li>[!UICONTROL video]</li></ul> | Modulo schema per risorse video di tipo MIME, ad esempio `video/avi` e `video/mp4`. |
| [!UICONTROL raccolta] | | Modulo schema per le raccolte. |
| [!UICONTROL contentfragment] | | Modulo schema per frammenti di contenuto. |
| [!UICONTROL moduli] | | Questo modulo schema si riferisce a [!DNL Adobe Experience Manager Forms]. |
| [!UICONTROL ugc_contentfragment] | | Modulo schema per contenuti e risorse generati dall’utente integrati in Experience Manager da social media. |

>[!NOTE]
>
>Per visualizzare i moduli figlio di un modulo schema, fare clic sul nome del modulo schema.

## Aggiungere un modulo schema metadati {#add-a-metadata-schema-form}

Per aggiungere un modulo schema metadati, effettua le seguenti operazioni:

1. Per aggiungere un modello personalizzato all’elenco, fai clic su **[!UICONTROL Crea]** dalla barra degli strumenti.

   >[!NOTE]
   >
   >Viene visualizzato un simbolo di blocco con i modelli non modificati. Se si personalizza un modello, questo non viene bloccato ![blocco chiuso](assets/do-not-localize/lock_closed_icon.svg).

1. Nella finestra di dialogo, specifica il titolo del modulo schema e fai clic su **[!UICONTROL Crea]** per completare il processo di creazione del modulo.

## Modificare i moduli schema metadati {#edit-metadata-schema-forms}

Puoi modificare un modulo schema metadati appena aggiunto o esistente. Il modulo schema metadati include schede ed elementi modulo all’interno di schede. Puoi mappare/configurare questi elementi modulo su un campo all’interno di un nodo di metadati nell’archivio CRX. È possibile aggiungere schede o elementi del modulo al modulo schema metadati. Le schede e gli elementi modulo derivati dall&#39;elemento padre sono nello stato bloccato. Non è possibile modificarli a livello di elemento secondario.

1. Il giorno [!UICONTROL Forms schema metadati] , selezionare un modulo e fare clic su **[!UICONTROL Modifica]** nella barra degli strumenti.

1. Il giorno **[!UICONTROL Editor modulo schema metadati]** , personalizzare il modulo metadati. Trascina i componenti necessari da **[!UICONTROL Genera modulo]** in una delle schede.

   ![Editor schema metadati per personalizzare la pagina Proprietà della risorsa](assets/metadata-schema-editor.png)

   *Figura: A [!UICONTROL Editor modulo schema metadati] pagina con schede disponibili.*

1. Per configurare un componente, selezionalo e modificane le proprietà in **[!UICONTROL Impostazioni]** scheda.

### Componenti all&#39;interno di [!UICONTROL Genera modulo] scheda {#components-within-the-build-form-tab}

Il **[!UICONTROL Genera modulo]** scheda elenca gli elementi del modulo utilizzati nel modulo schema. Il **[!UICONTROL Impostazioni]** fornisce gli attributi di ogni elemento selezionato nella scheda **[!UICONTROL Genera modulo]** scheda. Nella tabella seguente sono elencati gli elementi modulo disponibili in **[!UICONTROL Genera modulo]** scheda:

| Nome componente | Descrizione |
| -------------------------------- | ----------------------------------------------------------------------------------- |
| [!UICONTROL Intestazione sezione] | Aggiungi un’intestazione di sezione per un elenco di componenti comuni. |
| [!UICONTROL Testo su riga singola] | Aggiungi una proprietà di testo a riga singola. Viene memorizzato come stringa. |
| [!UICONTROL Testo con più valori] | Aggiungi una proprietà di testo con più valori. Viene memorizzato come array di stringhe. |
| [!UICONTROL Numero] | Aggiungi un componente numero. |
| [!UICONTROL Data] | Aggiungi un componente data. |
| [!UICONTROL A discesa] | Aggiungi un elenco a discesa. |
| [!UICONTROL Tag standard] | Aggiungi un tag. |
| [!UICONTROL Tag avanzati] | Migliora le funzionalità di ricerca aggiungendo automaticamente tag di metadati. |
| [!UICONTROL Campo nascosto] | Aggiungi un campo nascosto. Viene inviato come parametro POST al salvataggio della risorsa. |
| [!UICONTROL Risorsa con riferimento da] | Aggiungi questo componente per visualizzare l’elenco delle risorse a cui fa riferimento la risorsa. |
| [!UICONTROL Risorsa con riferimento] | Aggiungi per visualizzare un elenco di risorse che fanno riferimento alla risorsa. |
| [!UICONTROL Riferimenti prodotti] | Aggiungi per visualizzare l’elenco dei prodotti collegati alla risorsa. |
| [!UICONTROL Metadati contestuali] | Aggiungi per controllare la visualizzazione di altre schede di metadati nella pagina delle proprietà delle risorse. |

<!-- TBD: Ratings are not available in Experience Manager as a Cloud Service. Removed via cqdoc-18089 ticket. 
| [!UICONTROL Asset Rating]        | Add to display options for rating the asset.                                       |
-->

#### Modificare il componente metadati {#edit-the-metadata-component}

Per modificare le proprietà di un componente di metadati nel modulo, fai clic sul componente per modificare tutte o un sottoinsieme delle seguenti proprietà nel **[!UICONTROL Impostazioni]** scheda. Si consiglia di mappare un solo campo a una determinata proprietà nello schema metadati. In caso contrario, il sistema seleziona l’ultimo campo aggiunto mappato alla proprietà.

**Etichetta campo**: nome della proprietà dei metadati visualizzata nella pagina delle proprietà della risorsa.

**Mappa su proprietà**: questa proprietà specifica il percorso relativo o il nome del nodo della risorsa in cui viene salvato nell’archivio CRX. Inizia con `./` per indicare che il percorso si trova sotto il nodo della risorsa.

Di seguito sono riportati alcuni esempi di valori validi per una proprietà:

* `./jcr:content/metadata/dc:title`: memorizza il valore come proprietà nel nodo di metadati della risorsa `dc:title`.

* `./jcr:created`: memorizza la data e l’ora di creazione di una risorsa. È una proprietà protetta. Se configuri queste proprietà, l’Adobe consiglia di contrassegnarle come Disattiva modifica. In caso contrario, al momento di salvare le proprietà della risorsa si verifica l’errore “Impossibile modificare le risorse”.

Per garantire che il componente venga visualizzato correttamente nel modulo dello schema metadati, il percorso della proprietà non deve includere spazi.

* **Segnaposto**: utilizza questa proprietà per specificare il testo segnaposto rilevante relativo alla proprietà dei metadati.
* **Obbligatorio**: utilizza questa proprietà per contrassegnare una proprietà di metadati come obbligatoria nella pagina delle proprietà.
* **Disattiva modifica**: utilizza questa proprietà per non consentire alcuna modifica a una proprietà nella pagina delle proprietà.
* **Mostra campo vuoto in sola lettura**: contrassegna questa proprietà per visualizzare una proprietà di metadati nella pagina delle proprietà anche se non ha un valore. Per impostazione predefinita, quando una proprietà di metadati non ha un valore, non viene elencata nella pagina delle proprietà.
* **Mostra elenco ordinato**: utilizza questa proprietà per visualizzare un elenco ordinato di scelte.
* **Scelte**: utilizzare questa proprietà per specificare le scelte in un elenco.
* **Descrizione** : utilizza questa proprietà per aggiungere una breve descrizione del componente metadati.
* **Classe**: classe oggetto a cui è associata la proprietà.
* **Elimina**: fai clic [!UICONTROL Elimina] per eliminare un componente dal modulo schema.

>[!NOTE]
>
>Il [!UICONTROL Campo nascosto] Il componente non include questi attributi. Include invece proprietà, come gli attributi Nome, Valore, Etichetta campo e Descrizione. I valori del componente Campo nascosto vengono inviati come parametro POST ogni volta che la risorsa viene salvata. Non deve essere salvato come metadati della risorsa.

Se selezioni l’opzione **[!UICONTROL Obbligatorio]**, puoi cercare le risorse per le quali mancano i metadati obbligatori. Dal pannello **[!UICONTROL Filtri]**, espandi il predicato **[!UICONTROL Convalida metadati]** e seleziona l’opzione **[!UICONTROL Non valido]**. Nei risultati della ricerca vengono visualizzate le risorse per le quali mancano i metadati obbligatori, che sono stati configurati dal modulo schema.

Se aggiungi il componente Metadati contestuali a una scheda di qualsiasi modulo schema, il componente viene visualizzato come elenco nella pagina delle proprietà delle risorse a cui viene applicato lo schema specifico. L’elenco include tutte le altre schede, ad eccezione della scheda a cui è stato applicato il componente Metadati contestuali. Attualmente, questa funzione fornisce funzionalità di base per controllare la visualizzazione dei metadati in base al contesto.

Per visualizzare qualsiasi scheda nella pagina delle proprietà oltre alla scheda in cui viene applicato il componente Metadati contestuali, seleziona la scheda dall’elenco. La scheda viene aggiunta alla pagina delle proprietà.

### Specificare le proprietà nel file JSON {#specify-properties-in-json-file}

Invece di specificare le proprietà delle opzioni nella scheda **[!UICONTROL Impostazioni]**, puoi definire le opzioni in un file JSON, specificando le coppie chiave-valore corrispondenti. Nel campo **[!UICONTROL Percorso JSON]**, specifica il percorso del file JSON.

#### Aggiungere o eliminare una scheda nel modulo schema {#add-delete-a-tab-in-the-schema-form}

L’editor dello schema consente di aggiungere o eliminare una scheda. Il modulo schema predefinito include **[!UICONTROL Base]**, **[!UICONTROL Avanzate]** , **[!UICONTROL IPTC]**, e **[!UICONTROL Estensione IPTC]** schede.

![Schede predefinite nel modulo Schema metadati](assets/metadata-schema-form-tabs.png)

Clic `+` per aggiungere una scheda a un modulo schema. Per impostazione predefinita, il nome della nuova scheda è `Unnamed-1`. Puoi modificare il nome dalla sezione **[!UICONTROL Impostazioni]** scheda. Clic `X` per eliminare una scheda.

![Aggiungere o eliminare una scheda tramite Editor schema metadati](assets/metadata-schema-form-new-tab.png)

## Eliminare i moduli schema metadati {#deleting-metadata-schema-forms}

Experience Manager consente di eliminare solo i moduli schema personalizzati. Non consente di eliminare i moduli/modelli di schema predefiniti. Tuttavia, è possibile eliminare qualsiasi modifica personalizzata in questi moduli.

Per eliminare un modulo, selezionarlo e fare clic sull&#39;icona Elimina.

>[!NOTE]
>
>Dopo aver eliminato le modifiche personalizzate apportate a un modulo predefinito, nell&#39;interfaccia dello schema metadati viene visualizzata nuovamente l&#39;icona di blocco per indicare che il modulo è tornato allo stato predefinito.

>[!NOTE]
>
>* Dopo aver eliminato le modifiche personalizzate a un modulo predefinito, il blocco ![blocco chiuso](assets/do-not-localize/lock_closed_icon.svg) viene nuovamente visualizzato prima del modulo. Indica che il modulo viene ripristinato allo stato predefinito.
>* Non è possibile eliminare i moduli schema metadati predefiniti in [!DNL Assets].

## Moduli schema per tipi MIME {#schema-forms-for-mime-types}

[!DNL Experience Manager] fornisce moduli predefiniti per vari tipi MIME. Tuttavia, puoi aggiungere moduli personalizzati per risorse di vari tipi MIME.

### Aggiungere nuovi moduli per i tipi MIME {#adding-new-forms-for-mime-types}

Crea un modulo con il tipo appropriato. Ad esempio, per aggiungere un modello per `image/png` sottotipo, crea il modulo sotto i moduli &quot;image&quot;. Il titolo del modulo schema è il nome del sottotipo. In questo caso, il titolo è `png`.

#### Utilizza un modello di schema esistente per vari tipi MIME {#use-an-existing-schema-template-for-various-mime-types}

Puoi utilizzare un modello esistente per un tipo MIME diverso. Ad esempio, utilizza `image/jpeg` modulo per risorse di tipo MIME `image/png`.

In questo caso, crea un nodo `/etc/dam/metadataeditor/mimetypemappings` nell’archivio CRX. Specifica un nome per il nodo e definisci le seguenti proprietà:

| Nome | Descrizione | Tipo | Valore |
|------|-------------|------|-------|
| `exposedmimetype` | Nome del modulo esistente da mappare | `String` | `image/jpeg` |
| `mimetypes` | Elenco dei tipi MIME che utilizzano il modulo definito nella `exposedmimetype` attributo | `String` | `image/png` |

[!DNL Assets] associa i tipi MIME e i moduli schema seguenti:

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

La funzione Schema metadati è disponibile solo per gli amministratori. Tuttavia, gli amministratori possono fornire l’accesso ai non amministratori modificando alcune autorizzazioni. Fornire agli utenti non amministratori le autorizzazioni per creare, modificare ed eliminare `/conf` cartella.

## Applicare metadati specifici della cartella {#applying-folder-specific-metadata}

[!DNL Assets] consente di definire una variante di uno schema di metadati e applicarla a una cartella specifica.

Ad esempio, puoi definire una variante dello schema metadati predefinito e applicarla a una cartella. Quando applichi lo schema modificato, questo sovrascrive lo schema metadati predefinito originale applicato alle risorse all’interno della cartella.

Solo le risorse caricate nella cartella a cui è applicato questo schema sono conformi ai metadati modificati definiti nello schema di metadati della variante. [!DNL Assets] nelle altre cartelle in cui viene applicato lo schema originale, continuano a essere conformi ai metadati definiti nello schema originale.

L’ereditarietà dei metadati da parte delle risorse si basa sullo schema applicato alla cartella di livello superiore nella gerarchia. Lo stesso schema viene applicato o ereditato dalle sottocartelle. Se a livello di sottocartella viene applicato uno schema diverso, l’ereditarietà si interrompe.

1. In entrata [!DNL Experience Manager] , passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Schemi metadati]**. Viene visualizzata la pagina **[!UICONTROL Moduli schema metadati]**.
1. Selezionare la casella di controllo che precede un modulo, ad esempio il modulo di metadati predefinito, e fare clic su **[!UICONTROL Copia]** e salvarlo come modulo personalizzato. Specifica un nome personalizzato per il modulo, ad esempio: `my_default`. In alternativa, è possibile creare un modulo personalizzato.

1. In **[!UICONTROL Forms schema metadati]** , seleziona la `my_default` e quindi fare clic su **[!UICONTROL Modifica]**.
1. In **[!UICONTROL Editor schema metadati]** , aggiungere un campo di testo al modulo schema. Ad esempio, aggiungi un campo con l’etichetta **[!UICONTROL Categoria]**.
1. Clic **[!UICONTROL Salva]**. Il modulo modificato è elencato in **[!UICONTROL Forms schema metadati]** pagina.
1. Seleziona **[!UICONTROL Applica a cartelle]** dalla barra degli strumenti per applicare i metadati personalizzati a una cartella.
1. Seleziona la cartella in cui applicare lo schema modificato, quindi seleziona **[!UICONTROL Applica]**.
1. Se alla cartella è applicato l’altro schema metadati, viene visualizzato un messaggio che informa che stai per sovrascrivere lo schema metadati esistente. Clic **Sovrascrivere**.
1. Clic **OK** per chiudere il messaggio di operazione riuscita.
1. Passa alla cartella in cui è stato applicato lo schema metadati modificato.

## Definizione dei metadati obbligatori {#defining-mandatory-metadata}

Puoi definire campi obbligatori a livello di cartella, che vengono applicati alle risorse caricate nella cartella. Se carichi risorse con metadati mancanti per i campi obbligatori definiti in precedenza, nella vista a schede viene visualizzata un’indicazione visiva di metadati mancanti.

>[!NOTE]
>
>Un campo di metadati può essere definito come obbligatorio in base al valore di un altro campo. Nella vista Schede, in Experience Manager non viene visualizzato il messaggio di avvertenza relativo a metadati mancanti per tali campi di metadati obbligatori.

1. Fai clic sul logo dell’Experience Manager, quindi passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Schemi metadati]**. Viene visualizzata la pagina **[!UICONTROL Moduli schema metadati]**.
1. Salva il modulo metadati predefinito come modulo personalizzato. Ad esempio, salvala con nome `my_default`.
1. Modifica il modulo personalizzato. Aggiungi un campo obbligatorio. Ad esempio, aggiungi un **[!UICONTROL Categoria]** e rendere il campo obbligatorio.
1. Clic **[!UICONTROL Salva]**. Il modulo modificato è elencato in **[!UICONTROL Forms schema metadati]** pagina. Seleziona il modulo, quindi fai clic su **[!UICONTROL Applica a cartelle]** dalla barra degli strumenti per applicare i metadati personalizzati a una cartella.
1. Passa alla cartella e carica alcune risorse con metadati mancanti per il campo obbligatorio aggiunto al modulo personalizzato. Nella vista a schede della risorsa viene visualizzato un messaggio per i metadati mancanti per il campo obbligatorio.
1. (Facoltativo) Accesso `https://[server]:[port]/system/console/components/`. Configurare e abilitare `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` componente disabilitato per impostazione predefinita. Imposta la frequenza con cui Experience Manager controlla la validità dei metadati delle risorse.

   Questa configurazione aggiunge una proprietà `hasValidMetadata` a `jcr:content` delle risorse. Utilizzando questa proprietà, Experience Manager può filtrare i risultati in una ricerca.

   >[!NOTE]
   >
   >Se una risorsa viene aggiunta dopo il controllo pianificato, la risorsa non viene contrassegnata con `hasValidMetadata` fino al prossimo controllo pianificato. Le risorse non vengono visualizzate nei risultati di ricerca intermedi.

   >[!CAUTION]
   >
   >I controlli di convalida dei metadati richiedono molte risorse e possono influire sulle prestazioni del sistema. Pianificare i controlli di conseguenza. Se il server non è in grado di gestire il carico, provare a disattivare il processo

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
