---
title: Come possiamo sincronizzare Forms adattivo con i modelli di modulo XFA?
description: Sincronizzazione di Forms adattivo con file XFA/XDP.
uuid: 92818132-1ae0-4576-84f2-ece485a34457
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: dac4539b-804d-4420-9170-68000ebb2638
docset: aem65
source-git-commit: 7a65aa82792500616f971df52b8ddb6d893ab89d
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 0%

---


# Sincronizzazione di Forms adattivo con i modelli di modulo XFA{#synchronizing-adaptive-forms-with-xfa-form-templates}

## Introduzione {#introduction}

È possibile creare un modulo adattivo basato su un modello di modulo XFA ( `*.XDP` file). Questo riutilizzo consente di mantenere l’investimento nei moduli XFA esistenti. Per informazioni su come utilizzare un modello di modulo XFA per creare un modulo adattivo, [Creare un modulo adattivo basato su un modello](creating-adaptive-form.md).

Puoi riutilizzare i campi del file XDP nel modulo adattivo. Questi campi sono denominati campi associati. Le proprietà dei campi associati (ad esempio script, etichette e formato di visualizzazione) vengono copiate dal file XDP. Puoi anche scegliere di ignorare il valore di alcune di queste proprietà.

[!DNL AEM Forms] consente di mantenere sincronizzati i campi del Forms adattivo con eventuali modifiche apportate successivamente ai campi corrispondenti nel file XDP. Questo articolo spiega come abilitare questa sincronizzazione.

![È possibile trascinare campi da un modulo XFA a un modulo adattivo](assets/drag-drop-xfa.gif.gif)

In [!DNL AEM Forms] ambiente di authoring, puoi trascinare i campi da un modulo XFA (a sinistra) a un modulo adattivo (a destra)

## Prerequisiti {#prerequisites}

Per utilizzare le informazioni contenute in questo articolo, si consiglia di acquisire familiarità con le seguenti aree:

* [Creazione di un modulo adattivo](creating-adaptive-form.md)

* XFA (XML Forms Architecture)

Per utilizzare le risorse fornite per l’esempio di cui all’articolo, scarica il pacchetto di esempio come spiegato nella sezione successiva, [Pacchetto di esempio](synchronizing-adaptive-forms-xfa.md#p-sample-package-p).

## Pacchetto di esempio {#sample-package}

L’articolo utilizza un esempio per dimostrare come sincronizzare il modulo adattivo con un modello di modulo XFA aggiornato. Le risorse utilizzate nell’esempio sono disponibili in un pacchetto, che può essere scaricato da [Download](synchronizing-adaptive-forms-xfa.md#p-downloads-p) in questo articolo.

Dopo aver caricato il pacchetto, puoi visualizzare queste risorse in [!DNL AEM Forms] UI.

Installa il pacchetto utilizzando Gestione pacchetti: `https://<server>:<port>/crx/packmgr/index.jsp`

Il pacchetto contiene le seguenti risorse:

1. `sample-form.xdp`: modello di modulo XFA utilizzato come esempio

1. `sample-xfa-af`: modulo adattivo basato sul file sample-form.xdp. Questo modulo adattivo, tuttavia, non include alcun campo. Nel passaggio successivo, aggiungeremo contenuto a questo modulo adattivo.

### Aggiungere contenuto al modulo adattivo {#add-content-to-adaptive-form-br}

1. Passa a https://&lt;server>:&lt;port>/aem/forms.html. Se richiesto, immettere le credenziali.
1. Apri sample-af-xfa per la modifica in modalità di authoring.
1. Dal browser Contenuto nella barra laterale, scegli la scheda Oggetti modello dati. Trascina NumericField1 e TextField1 nel modulo adattivo.
1. Cambia il titolo di NumericField1 da **Campo numerico** a **Campo numerico AF.**

>[!NOTE]
>
>Nei passaggi precedenti, abbiamo sovrascritto una proprietà di un campo nel file XDP. Pertanto, questa proprietà non verrà sincronizzata se la proprietà corrispondente nel file XDP viene modificata in un secondo momento.

## Rilevamento delle modifiche nel file XDP {#detecting-changes-in-xdp-file}

Ogni volta che si verificano modifiche in un file XDP o in un frammento, il [!DNL AEM Forms] L’interfaccia utente contrassegna tutti i Forms adattivi basati sul file XDP o sul frammento.

Dopo aver aggiornato un file XDP, devi caricarlo nuovamente in [!DNL AEM Forms] Interfaccia utente per la segnalazione delle modifiche.

Ad esempio, aggiorniamo il `sample-form.xdp` esegui i seguenti passaggi:

1. Accedi a `https://<server>:<port>/projects.html.` Immettere le credenziali, se richiesto.
1. Fai clic sulla scheda Forms a sinistra.
1. Scarica il file `sample-form.xdp` sul computer locale. Il file XDP viene scaricato come `.zip` file, che può essere estratto utilizzando qualsiasi utilità di decompressione dei file.

1. Apri `sample-form.xdp` e modificare il titolo del campo TextField1 da **Campo di testo** a **Campo di testo personale**.

1. Carica `sample-form.xdp` file di nuovo in [!DNL AEM Forms] UI.

Se un file XDP viene aggiornato, quando modifichi il Forms adattivo in base al file XDP nell’editor viene visualizzata un’icona. Questa icona indica che il modulo adattivo non è sincronizzato con il file XDP. Nell’immagine seguente, vedi l’icona accanto nella barra laterale.

![Icona per visualizzare che il modulo adattivo non è sincronizzato con il file XDP](assets/sync-af-xfa.png)

## Sincronizzazione di Adaptive Forms con il file XDP più recente {#synchronizing-adaptive-forms-with-the-latest-xdp-file}

Quando un modulo adattivo non sincronizzato con il file XDP viene aperto per la creazione la volta successiva, viene visualizzato il seguente messaggio: **Lo schema o il modello per il modulo adattivo è stato aggiornato. `Click Here` per basarlo sulla nuova versione.**

Facendo clic sul messaggio, i campi del modulo adattivo vengono sincronizzati con i campi corrispondenti nel file XDP.

Nell’esempio utilizzato in questo articolo, apri `sample-xfa-af` in modalità authoring. Il messaggio viene visualizzato verso la parte inferiore del modulo adattivo.

![Messaggio che richiede di sincronizzare il modulo adattivo con il file XDP](assets/sync-af-xfa-1.png)

### Aggiornamento delle proprietà {#updating-the-properties}

Tutte le proprietà copiate dal file XDP nel modulo adattivo vengono aggiornate, ad eccezione di quelle esplicitamente ignorate dall’autore nel modulo adattivo (dalla finestra di dialogo dei componenti). L’elenco delle proprietà aggiornate è disponibile nei registri del server.

Per aggiornare le proprietà nell’esempio di modulo adattivo, fai clic sul collegamento (etichettato `"Click Here"`) nel messaggio. Il titolo di TextField1 cambia da **Campo di testo** a **Campo di testo personale**.

![update-property](assets/update-property.png)

>[!NOTE]
>
>Il campo numerico AF dell’etichetta non è stato modificato perché hai ignorato questa proprietà dalla finestra di dialogo delle proprietà del componente, come descritto in [Aggiungere contenuto a Forms adattivo](synchronizing-adaptive-forms-xfa.md#p-add-content-to-adaptive-form-br-p).

### Aggiunta di nuovi campi dal file XDP al modulo adattivo   {#adding-new-fields-from-xdp-file-to-adaptive-form-nbsp}

Tutti i campi aggiunti successivamente al file XDP originale vengono visualizzati nella scheda Gerarchia modulo e puoi trascinare i nuovi campi nel modulo adattivo.

Non è necessario fare clic sul collegamento nel messaggio di errore per aggiornare i campi nella scheda Gerarchia modulo.

### Campi eliminati nel file XDP {#deleted-fields-in-xdp-file}

Se un campo copiato in precedenza in un modulo adattivo viene eliminato da un file XDP, nella modalità di creazione viene visualizzato un messaggio di errore che informa che il campo non esiste nel file XDP. In questi casi, elimina manualmente il campo dal modulo adattivo o cancella il `bindRef` nella finestra di dialogo del componente.

I passaggi seguenti illustrano questo flusso di utilizzo per le risorse nell’esempio utilizzato in questo articolo:

1. Aggiornare il `sample-form.xdp` ed eliminare NumericField1.
1. Carica `sample-form.xdp` file in [!DNL AEM Forms] UI
1. Apri `sample-xfa-af` Modulo adattivo per l’authoring. Viene visualizzato il seguente messaggio di errore: Lo schema o il modello di modulo per il modulo adattivo è stato aggiornato. `Click Here` per basarlo sulla nuova versione.

1. Fai clic sul collegamento (con etichetta &quot; `Click Here`&quot;). Viene visualizzato un messaggio di errore per segnalare che il campo non esiste più nel file XDP.

![Errore visualizzato quando si elimina un elemento nel file XDP](assets/no-element-xdp.png)

Anche il campo che è stato eliminato è contrassegnato da un&#39;icona per indicare un errore nel campo.

![Icona di errore nel campo](assets/error-field.png)

>[!NOTE]
>
>I campi nel modulo adattivo con un’associazione non corretta (non valida) `bindRef` nella finestra di dialogo per modifica) sono considerati come campi eliminati. Se l’autore non corregge questi errori e pubblica il modulo adattivo, il campo viene considerato come un normale campo modulo adattivo non associato e viene incluso nella sezione non associata del file XML di output.

## Download {#downloads}

Pacchetto di contenuti per l’esempio in questo articolo

[Ottieni file](assets/sample-xfa-af-sync-1.0.zip)
