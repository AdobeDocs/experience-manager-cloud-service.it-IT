---
title: Creare la struttura del contenuto per l’app
description: Scopri come utilizzare modelli per frammenti di contenuto AEM per creare la struttura che funge da base per i contenuti headless.
hidefromtoc: true
index: false
exl-id: ace9b9f3-8bc6-4a36-a51c-ff60cdd339ce
feature: Headless
role: Admin, User, Developer
source-git-commit: c9cddf9f0e344a2a24ee1a608b3ea920e258f34a
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 100%

---


# Creare la struttura del contenuto per l’app {#content-structure}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview"
>title="Creare la struttura del contenuto per l’app"
>abstract="Seguendo questa serie di guide interattive imparerai a creare la struttura (nota anche come modello per frammenti di contenuto) che funge da fondamento per tutti i contenuti headless."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide"
>title="Avvia la console Modelli"
>abstract="Scopriamo come creare uno schema riutilizzabile, denominato modello per frammenti di contenuto, per il contenuto in Adobe Experience Manager as a Cloud Service. Guarda il video per comprendere il motivo per cui questo passaggio è importante. <br><br>In questo modulo di apprendimento utilizzerai come esempio un sito di viaggi e vedrai in dettaglio come creare un modello che rappresenta un viaggio.<br><br>Avvia questo modulo in una nuova scheda facendo clic sul pulsante sottostante e quindi segui questa guida."
>additional-url="https://video.tv.adobe.com/v/3436548?captions=ita" text="Video introduttivo sulla struttura dei contenuti"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide_footer"
>title="Congratulazioni. Hai imparato a creare un modello per frammenti di contenuto per rappresentare la struttura dei dati headless e hai fatto il primo passo per distribuire contenuti omnicanale in modo scalato e standard."
>abstract=""

## Creare un modello {#create-model}

La console Modelli per frammenti di contenuto si apre in una nuova scheda. Considera la console Modelli per frammenti di contenuto come una libreria di modelli, in cui puoi creare modelli e gestire quelli esistenti.

In questo esempio, viene creato un modello che rappresenta la struttura dati di un viaggio. Un viaggio che utilizza questo modello viene definito come un’**Avventura**.

1. Fai clic su **Crea** in alto a destra per iniziare a creare un modello per frammenti di contenuto.

1. La procedura guidata Crea modello ti guida attraverso la creazione del modello. Fornisci le seguenti informazioni obbligatorie.

   * **Titolo modello**: breve etichetta del modello che in genere ne indica lo scopo. Assegna al nuovo modello il titolo `Adventure`.
   * **Abilita modello**: questa opzione è selezionata per impostazione predefinita e deve essere selezionata per poter creare frammenti di contenuto in base a questo modello.

1. Una volta compilati i campi obbligatori, fai clic su **Crea** in alto a destra per creare il modello.

1. La finestra di dialogo **Completato** conferma che il modello è stato creato. Fai clic su **Apri** nella finestra di dialogo per aprire il nuovo modello per frammenti di contenuto nell’editor in una nuova scheda. Quindi passa al passaggio successivo per aggiungere campi di dati al modello.

![Passaggi due e tre della creazione di un modello per frammenti di contenuto](assets/do-not-localize/create-model.png)

## Utilizzo dell’Editor modelli {#configure-model}

Ora hai un modello chiamato **Adventure** (Avventura), ma non dispone di dettagli come durata, destinazione e attività. Prima di poter utilizzare il modello, è necessario definire la struttura dei relativi dati.

Nell’editor di modelli per frammenti di contenuto è possibile configurare i tipi di dati e le proprietà che definiscono il contenuto del modello.

>[!TIP]
>
>È importante seguire gli schemi di denominazione nelle istruzioni seguenti, poiché nei moduli successivi si farà riferimento a questi stessi nomi.

1. Trascina un campo **Testo su riga singola** dal pannello **Tipi di dati** a destra dell’editor e rilascialo sul modello per frammenti di contenuto.

1. Una volta inserito un tipo di dati, la colonna **Tipi di dati** lascia automaticamente il posto alla scheda **Proprietà**, che consente di definire i dettagli del tipo di dati inserito. Per questo primo campo, memorizza il titolo del viaggio o dell’avventura. Immetti le seguenti proprietà.

   * **Rendering come:** **Campo di testo** - Quando si crea un’avventura, questo campo ne memorizza il titolo.
   * **Etichetta campo:** `Title` - Questa è l’etichetta che viene visualizzata per questo campo quando si crea un’avventura.

1. Una volta definite le proprietà del campo, puoi tornare alla scheda **Tipi di dati** nel pannello a destra e aggiungere altri campi mediante trascinamento.

In questo modo, puoi aggiungere al modello tutti i campi necessari per supportare qualsiasi struttura dati necessaria. I tipi di campi dati variano, ma il processo di aggiunta al modello rimane lo stesso.

Procedi alla sezione successiva per aggiungere i campi necessari per completare e salvare il modello **Adventure** (Avventura)

![Passaggi uno, due e tre per aggiungere campi al modello](assets/do-not-localize/define-model-fields.png)

## Aggiungi campi al modello {#additional-fields}

Hai già un campo per il titolo dell&#39;avventura. Ora devi aggiungere dei campi per acquisire la descrizione, il prezzo e un’immagine rappresentativa dell’avventura.

>[!TIP]
>
>Il modello **Adventure** (Avventura) si basa sul sito di esempio WKND per AEM. Puoi [visitare il sito WKND qui](https://wknd.site/us/en/adventures/yosemite-backpacking.html) per visualizzare il contenuto che utilizza il modello **Adventure** (Avventura).

Segui gli stessi passaggi indicati sopra per aggiungere questi ulteriori campi. L’unica differenza consiste nelle proprietà che devi impostare.

1. Per aggiungi un campo in cui memorizzare la descrizione dell’avventura, trascina un campo **Testo su più righe** e immetti le seguenti proprietà:

   * **Rendering come:** **Area di testo** - Quando crei un’avventura, in questo campo puoi memorizzare una breve descrizione del viaggio.
   * **Etichetta campo:** `Description` - Questa è l’etichetta che viene visualizzata per questo campo quando si crea un’avventura.
   * **Tipo predefinito**: **testo normale**: formato richiesto per questo esempio.

1. Per aggiungere un campo in cui memorizzare il prezzo dell’avventura, trascina un campo **Testo su riga singola** e immetti le seguenti proprietà:

   * **Rendering come:** **Campo di testo** - Quando crei un’avventura, in questo campo viene memorizzato il prezzo del viaggio.
   * **Etichetta campo:** `Price` - Questa è l’etichetta che viene visualizzata per questo campo quando si crea un’avventura.

1. Aggiungi un campo in cui memorizzare un’immagine che rappresenta il viaggio. Le immagini in AEM vengono memorizzate come un altro tipo di contenuto denominato **Risorse**. Per creare un campo per immagini, trascina un campo **Riferimento contenuto** che fa riferimento alla risorsa dell’immagine.

   * **Rendering come:** **Riferimento contenuto** - Quando crei un’avventura, questo campo punta alla risorsa immagine che rappresenta questo viaggio.
   * **Etichetta campo:** `Image` - Questa è l’etichetta che viene visualizzata per questo campo quando si crea un’avventura.
   * **Percorso directory principale:** `/content/dam/aem-demo-assets/en`: specifica un percorso del punto iniziale durante l’esplorazione delle risorse con il Selettore risorse.

1. Dopo aver aggiunto i campi necessari per il modello per frammenti di contenuto, fai clic su **Salva** in alto a destra.

1. Il modello viene salvato e si torna alla console del modello per frammenti di contenuto.
