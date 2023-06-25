---
title: Creare la struttura del contenuto per l’app
description: Scopri come utilizzare modelli per frammenti di contenuto AEM per creare la struttura che funge da base per i contenuti headless.
hidefromtoc: true
index: false
exl-id: ace9b9f3-8bc6-4a36-a51c-ff60cdd339ce
source-git-commit: f0e9fe0bdf35cc001860974be1fa2a7d90f7a3a9
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 34%

---


# Creare la struttura del contenuto per l’app {#content-structure}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview"
>title="Creare la struttura del contenuto per l’app"
>abstract="Seguendo questa serie di guide interattive, imparerai a creare una struttura (nota come modello per frammenti di contenuto) che funge da struttura fondamentale per i contenuti headless."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide"
>title="Avviare la console del modello"
>abstract="Scopriamo come creare uno schema riutilizzabile, denominato modello per frammenti di contenuto, per il contenuto in Adobe Experience Manager as a Cloud Service. Guarda il video per comprendere perché questo passaggio è importante. <br><br>In questo modulo di apprendimento, utilizzi un sito di viaggio come esempio e segui la creazione di un modello che rappresenta un viaggio.<br><br>Avvia questo modulo in una nuova scheda facendo clic sul pulsante sottostante e quindi segui questa guida."
>additional-url="https://video.tv.adobe.com/v/3413261?captions=ita" text="Video introduttivo sulla struttura dei contenuti"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide_footer"
>title="Congratulazioni. Hai imparato a creare un modello per frammenti di contenuto per rappresentare la struttura dei dati headless e hai fatto il primo passo per distribuire contenuti omni-channel in modo scalato e standard."
>abstract=""

## Creare un modello {#create-model}

La console Modelli per frammenti di contenuto si apre in una nuova scheda. Considera la console dei modelli Frammento di contenuto come una libreria di modelli in cui puoi creare modelli e gestire quelli esistenti.

Ad esempio, puoi creare un modello che rappresenta la struttura dati di un viaggio presente in un sito web di viaggi. Un viaggio che utilizza questo modello viene definito **Avventura**.

1. Nell’angolo superiore destro dello schermo, fai clic su **Crea** per iniziare a creare un modello per frammenti di contenuto.

1. La procedura guidata Crea modello assiste l&#39;utente durante la creazione del modello. Fornisci le seguenti informazioni obbligatorie.

   * **Titolo modello** - Breve etichetta del modello che in genere indica lo scopo del modello. È possibile chiamare il nuovo modello `Adventure`.
   * **Abilita modello** - Questa opzione è selezionata per impostazione predefinita e deve essere selezionata per poter creare frammenti di contenuto in base a questo modello.

1. Dopo aver compilato i campi obbligatori, fai clic su **Crea** in alto a sinistra per creare il modello.

1. Il **Completato** conferma la creazione del modello. Clic **Apri** nella finestra di dialogo, in modo da poter aprire il nuovo Modello per frammenti di contenuto nell’editor in una nuova scheda. Quindi procedi al passaggio successivo per aggiungere campi dati al modello.

![Passaggi due e tre della creazione di un modello di frammento di contenuto](assets/do-not-localize/create-model.png)

## Utilizzo dell’Editor modelli {#configure-model}

Ora disponi di un modello denominato **Avventura**, ma non contiene dettagli come durata, destinazione e attività. Prima di poter utilizzare il modello, è necessario definire la struttura dei dati.

Nell’editor modelli di frammento di contenuto è possibile configurare i tipi di dati e le proprietà che definiscono il contenuto del modello.

>[!TIP]
>
>È importante seguire gli schemi di denominazione nelle istruzioni seguenti perché a questi nomi specifici si fa riferimento nei moduli successivi.

1. Trascina un campo **Testo su riga singola** dal pannello **Tipi di dati** a destra dell’editor e rilascialo sul modello per frammenti di contenuto.

1. Una volta inserito un tipo di dati, il **Tipi di dati** viene modificata automaticamente in **Proprietà** , in cui è possibile definire i dettagli del tipo di dati inserito. Per questo primo campo, vuoi memorizzare il titolo del viaggio o dell’avventura. Immetti le seguenti proprietà.

   * **Rendering come:** **Campo di testo** - Quando crei un’avventura, in questo campo viene memorizzato il titolo dell’avventura.
   * **Etichetta campo:** `Title` : l’etichetta visualizzata per questo campo durante la creazione di un’avventura.

1. Dopo aver definito le proprietà del campo, puoi tornare al **Tipi di dati** nel pannello di destra e aggiungi altri campi trascinandoli.

In questo modo, puoi aggiungere al modello tutti i campi necessari per supportare qualsiasi struttura di dati ti serva. I tipi di campi dati variano, ma il processo di aggiunta al modello rimane lo stesso.

Procedi alla sezione successiva per aggiungere i campi necessari per completare e salvare **Avventura** modello

![Passaggi uno, due e tre per aggiungere campi al modello](assets/do-not-localize/define-model-fields.png)

## Aggiungi campi al modello {#additional-fields}

Hai già un campo per il titolo dell&#39;avventura. Ora è necessario aggiungere campi per acquisire la descrizione, il prezzo e un&#39;immagine rappresentativa dell&#39;avventura.

>[!TIP]
>
>Il modello di **Avventura** si basa sul sito di esempio WKND per AEM. Puoi [visitare il sito qui](https://wknd.site/us/en/adventures/yosemite-backpacking.html) per visualizzare il contenuto che utilizza il modello **Avventura**.

Segui gli stessi passaggi indicati sopra per aggiungere questi ulteriori campi. L&#39;unica differenza consiste nelle proprietà che dovete impostare.

1. Aggiungi un campo in modo da poter memorizzare la descrizione dell’avventura trascinando e rilasciando una **Testo su più righe** e immetti le seguenti proprietà:

   * **Rendering come:** **Area di testo** - Quando crei un’avventura, questo campo memorizza una breve descrizione del viaggio.
   * **Etichetta campo:** `Description` : l’etichetta visualizzata per questo campo durante la creazione di un’avventura.

1. Aggiungi un campo in modo da poter archiviare il prezzo dell’avventura trascinando e rilasciando un **Testo su riga singola** e immetti le seguenti proprietà:

   * **Rendering come:** **Campo di testo** - Quando crei un’avventura, questo campo memorizza il prezzo del viaggio.
   * **Etichetta campo:** `Price` : l’etichetta visualizzata per questo campo durante la creazione di un’avventura.

1. Aggiungi un campo in modo da poter memorizzare un’immagine che rappresenta il viaggio. Le immagini in AEM vengono memorizzate come un altro tipo di contenuto denominato **Risorse**. Per creare un campo per loro, trascina e rilascia una **Riferimento contenuto** campo che fa riferimento alla risorsa dell’immagine.

   * **Rendering come:** **Riferimento contenuto** - Quando crei un’avventura, questo campo punta alla risorsa immagine che rappresenta il viaggio.
   * **Etichetta campo:** `Image` : l’etichetta visualizzata per questo campo durante la creazione di un’avventura.

1. Dopo aver aggiunto i campi necessari per il modello Frammento di contenuto, in alto a destra della finestra, fai clic su **Salva**.

1. Il modello viene salvato e si torna alla console del modello di frammento di contenuto.
