---
title: Riutilizzare i frammenti di contenuto con MSM e Live Copy
description: Scopri come utilizzare la funzionalità Live Copy di MSM per utilizzare lo stesso contenuto di frammenti di contenuto, o simile, in più posizioni, durante la sincronizzazione con il contenuto sorgente.
badgeSaas: label="AEM Sites" type="Positive" tooltip="Si applica ad AEM Sites)."
feature: Content Fragments
role: User
solution: Experience Manager Sites
hide: true
hidefromtoc: true
index: false
source-git-commit: 85b72909597a95531aea51719c841bc5db9c1a21
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 3%

---

# Riutilizzare frammenti di contenuto con MSM {#reuse-content-fragments-using-msm}

Multi Site Manager (MSM) e la funzionalità Live Copy consentono di utilizzare lo stesso contenuto in più posizioni, sincronizzandolo con il contenuto sorgente.

<!-- CQDOC-23473 - feature is currently beta so page is hidden, see metadata -->
<!-- CQDOC-23473 - screenshots -->
<!-- CQDOC-23473 - only mentioned once in ToC, add entries -->
<!-- CQDOC-23473 - will work on folders -->

<!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

>[!CAUTION]
>
>MSM dalla console Frammenti di contenuto è attualmente funzionalità Beta ed è disponibile solo per clienti specifici.
>
>MSM per frammenti di contenuto è disponibile anche quando si utilizzano frammenti di contenuto tramite la console **Assets**.

* Con MSM Live Copy puoi:
   * Crea contenuto una volta
   * Riutilizzare questo contenuto in altre aree dello stesso sito, in altri siti o in applicazioni.
* MSM mantiene quindi le relazioni in tempo reale tra il contenuto sorgente e le relative Live Copy in modo che:
   * Quando modifichi il contenuto sorgente, la sorgente e le Live Copy vengono sincronizzate.
   * Puoi apportare modifiche solo al contenuto delle Live Copy disconnettendo la relazione live per singoli frammenti secondari e/o componenti.

<!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

Per una panoramica dettagliata dei concetti di MSM, consulta Riutilizzo dei contenuti: Multi Site Manager e Live Copy.

<!--
For a detailed overview of MSM concepts see [Reusing Content: Multi Site Manager and Live Copy](/help/sites-cloud/administering/msm/overview.md).
-->

<!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

>[!NOTE]
>
>La funzionalità Multi Site Manager (MSM) in Adobe Experience Manager consente agli utenti di riutilizzare i contenuti creati una sola volta e poi riutilizzati in più posizioni web.

<!--
>[!NOTE]
>
>[Multi Site Manager (MSM)](/help/sites-cloud/administering/msm/overview.md) functionality in Adobe Experience Manager enables users to reuse content that is authored once and then reused across multiple web-locations. 
-->

Utilizzando MSM per frammenti di contenuto puoi:

* Crea frammenti di contenuto una volta e quindi crea copie (collegate) di questi frammenti da riutilizzare in altre aree del sito o dell’applicazione.
* Mantieni più copie sincronizzate aggiornando la copia sorgente una sola volta, quindi inviando le modifiche alle copie (live).
* Apporta modifiche locali sospendendo temporaneamente o definitivamente il collegamento tra i frammenti padre e figlio, completamente o per le relative varianti o campi.

MSM per frammenti di contenuto, combinato con la funzionalità nell’Editor frammenti di contenuto, consente di interrompere e ripristinare l’ereditarietà a livello di campo.

<!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

>[!NOTE]
>
>In questa pagina sono illustrate le funzionalità di MSM quando si utilizza la console **Frammenti di contenuto**.
>
>MSM per frammenti di contenuto è disponibile anche quando si utilizzano frammenti di contenuto tramite la console **Assets**.

<!--
>[!NOTE]
>
>This page covers MSM functionality when using the **Content Fragments** console.
>
>MSM for Content Fragments is also available when using [Content Fragments via the **Assets** console](/help/assets/content-fragments/content-fragments-msm.md). 
-->

## Creare una Live Copy {#create-a-live-copy}

<!-- CQDOC-23473 - exclude children or referenced content fragments? -->

Per creare una Live Copy del frammento di contenuto:

1. Nella console Frammenti di contenuto passa alla posizione del frammento.
1. Seleziona il frammento.
1. Seleziona **Crea Live Copy** nella barra degli strumenti superiore.
1. Nella finestra di dialogo visualizzata, specifica la destinazione e continua con **Successivo**.
1. Specifica le proprietà. Puoi specificare il titolo, il nome e se la Live Copy deve escludere gli elementi secondari (frammenti nidificati).
1. Continua con **Avanti**.
1. Seleziona se desideri che la Live Copy venga creata immediatamente (**Ora**) o in una data e un&#39;ora **Più tardi**.
1. Conferma con **Crea Live Copy**.

   <!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

   >[!CAUTION]
   >
   >Se desideri utilizzare MSM per creare copie di frammenti di contenuto, tutti i vincoli **Unique** devono essere rimossi da qualsiasi tipo di dati utilizzato nei rispettivi modelli per frammenti di contenuto.

   <!--
   >[!CAUTION]
   >
   >If you want to use MSM to create copies of Content Fragments), then any **Unique** constraints should be removed from any Data Types used in the respective [Content Fragment Models](/help/assets/content-fragments/content-fragments-models.md).
   -->

## Visualizza proprietà e stato {#view-properties-and-status}

Per visualizzare le proprietà e lo stato del sorgente e della Live Copy:

1. Nella console Frammenti di contenuto passa alla posizione del frammento.
1. Seleziona il frammento.
1. Seleziona l&#39;icona Informazioni (i) nella colonna **Titolo** del frammento.
Si aprirà il pannello di informazioni corretto.
1. Seleziona la scheda per **Dettagli Live Copy**.

   ![Informazioni su una Live Copy](/help/sites-cloud/administering/content-fragments/assets/cf-msm-information.png)

## Propagare le modifiche {#propagate-modifications}

Per propagare le modifiche tra l’origine e la Live Copy.

### Sincronizza {#synchronize}

Per attivare una sincronizzazione che richiama gli aggiornamenti del contenuto dalla Live Copy alla sorgente:

1. Nella console Frammenti di contenuto passa alla posizione dell’origine del frammento.
1. Seleziona il frammento.
1. Seleziona **Sincronizza** nella barra degli strumenti.
1. Conferma **Sincronizza** nella finestra di dialogo.

### Rollout {#rollout}

Per attivare un Rollout che invia gli aggiornamenti sorgente alla Live Copy:

1. Nella console Frammenti di contenuto passa alla posizione del frammento Live Copy.
1. Seleziona il frammento.
1. Seleziona **Rollout** nella barra degli strumenti. Verrà avviata la procedura guidata per guidarti nel processo.
1. Seleziona le Live Copy da includere nel rollout e **Continua**.
1. Pianifica il rollout per immediatamente (**Ora**) o **Più tardi**.
1. **Continua** come appropriato.

<!-- CQDOC-23473 - feature is beta, is in authoring so remove here when GA -->

## Annullare e ripristinare l’ereditarietà nell’editor {#cancel-and-revert-to-inheritance-in-the-editor}

L’ereditarietà è il meccanismo in cui il contenuto può essere inviato automaticamente da un frammento all’altro. I campi ereditati e le varianti possono essere il prodotto della gestione multisito.

Puoi annullare (quindi ripristinare) l’ereditarietà nell’editor dei frammenti di contenuto. A seconda del contesto, questo può essere disponibile per una variante o per un singolo campo, se il frammento fa parte di una Live Copy.

Ad esempio:

* Annulla ereditarietà

  ![Icona Annulla ereditarietà](/help/sites-cloud/administering/content-fragments/assets/cf-authoring-cancel-inheritance.png)

* Ripristina ereditarietà (se l’ereditarietà è già annullata)

  ![Icona Ripristina ereditarietà](/help/sites-cloud/administering/content-fragments/assets/cf-authoring-revert-to-inheritance.png)

<!-- CQDOC-23473 - feature is currently beta reinstate Note for GA -->

<!--
## Cancel, and revert to, inheritance {#cancel-and-reinstate-inheritance}

Inheritance is the mechanism where content can be automatically pushed from one fragment to another. Inherited fields, and variations, can be the product of Multi-Site Management.

You can cancel (then revert) the inheritance. Depending on the context, this can be available for a variation, or an individual field, if the fragment is part of a live copy.
-->

<!--
>[!NOTE]
>
>For more details see [Cancel, and revert to, inheritance in the editor](/help/sites-cloud/administering/content-fragments/authoring.md#cancel-and-revert-to-inheritance).
-->

## Confrontare MSM per frammenti di contenuto e pagine di siti {#compare-msm-for-content-fragments-and-sites-pages}

<!-- CQDOC-23473 - needs a detailed review -->

Nella maggior parte degli scenari, MSM per Frammenti di contenuto corrisponde al comportamento di MSM per la funzionalità Sites Pages. Alcune differenze chiave da notare sono:

* Il blueprint in MSM per le pagine Sites è denominato sorgente Live Copy in MSM per i frammenti di contenuto.
* Per le pagine Sites, puoi confrontare una blueprint e la relativa Live Copy, ma non è possibile per i frammenti di contenuto confrontare un’origine con la relativa Live Copy.
* Non puoi modificare una Live Copy nella console Frammenti di contenuto.
* Le pagine Sites hanno in genere elementi secondari, ma non i frammenti di contenuto, anche se potrebbero aver fatto riferimento a frammenti. L’opzione per includere o escludere elementi figlio fa riferimento a questi frammenti di riferimento.
* La rimozione del passaggio Capitoli nella procedura guidata Crea sito non è supportata in MSM per Frammenti di contenuto.
* La configurazione dei blocchi MSM nelle proprietà della pagina non è supportata in MSM per i frammenti di contenuto.
* Per MSM per frammenti di contenuto, utilizza solo la **configurazione di rollout standard**. Altre configurazioni di rollout non sono disponibili per MSM per Frammenti di contenuto.

>[!NOTE]
>
>Ricorda che MSM per frammenti di contenuto a cui si accede tramite la console Frammenti di contenuto si basa sulla funzionalità Assets, perché sono memorizzati come Assets (anche se considerata una funzione Sites).

## Limitazioni {#limitations}

* I trigger durante la modifica e la configurazione di rollout associata non esistono per i frammenti di contenuto.
