---
title: Creare contenuti headless
description: Utilizza il modello Frammento di contenuto creato in precedenza per creare contenuti che possono essere utilizzati per la creazione delle pagine o come base per il contenuto headless.
hidefromtoc: true
index: false
exl-id: d74cf5fb-4c4a-4363-a500-6e2ef6811e60
feature: Headless
role: Admin, User, Developer
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: ht
source-wordcount: '688'
ht-degree: 100%

---


# Creare contenuti headless {#create-content}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_create_content"
>title="Creare contenuti headless"
>abstract="Basandoti sui modelli creati nel modulo precedente, imparerai a creare contenuti che possono essere utilizzati per l’authoring delle pagine o come base per contenuti headless."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_create_content_guide"
>title="Avvia la console Frammenti di contenuto"
>abstract="La creazione di contenuti coerenti e di alta qualità che funzionano perfettamente nelle applicazioni e nei siti web ti permette di offrire ai tuoi clienti esperienze eccezionali. Questo modulo ti guida nella creazione dei primi contenuti headless tramite la console Frammenti di contenuto.<br><br>Avvia questo modulo in una nuova scheda facendo clic sul pulsante sottostante, quindi segui questa guida."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_create_content_guide_footer"
>title="Ottimo lavoro! In questo modulo hai imparato a creare un contenuto headless come frammento di contenuto, basato sul modello creato in precedenza. Ora puoi comprendere come i team di contenuti possono creare e gestire contenuti per app e siti web indipendentemente dai cicli di sviluppo."
>abstract=""

## Creare un frammento di contenuto {#create-fragment}

I frammenti di contenuto rappresentano il contenuto headless dell’utente e si basano su strutture predefinite, denominate modelli di frammenti di contenuto. Hai già creato un modello in un modulo precedente.

In questo modulo viene creato un frammento di contenuto basato su tale modello, utilizzando la console Frammenti di contenuto. Considera la console Frammenti di contenuto come una libreria di contenuti headless. Utilizzala per creare nuovi frammenti di contenuto e gestire i frammenti esistenti.

La console Frammenti di contenuto viene utilizzata per creare e modificare contenuti headless tra canali di consegna e indipendenti dal contesto, che può rivelarsi il metodo più efficace in molti casi di authoring. In un modulo successivo scoprirai la modifica di contenuti headless nel contesto e locale.

1. Seleziona il pulsante **Crea** in alto a destra nella console.

1. La finestra di dialogo **Nuovo frammento di contenuto** si apre e lì puoi iniziare a creare un frammento di contenuto. La **Posizione** viene compilata automaticamente con le posizioni in cui verranno salvati i nuovi contenuti.

1. Nel menu a discesa **Modello di frammento di contenuto**, seleziona il modello di frammento di contenuto **Adventure** (Avventura) creato in precedenza.

1. Aggiungi `Tuscany` come **Titolo** descrittivo per il frammento di contenuto. In questo modo è possibile identificare il frammento nella console.

1. Seleziona **Crea e apri**.

![Creazione di un nuovo frammento di contenuto](assets/do-not-localize/create-content.png)

>[!TIP]
>
>A seconda delle impostazioni del browser, la nuova scheda del browser potrebbe essere rimossa da un blocco dei pop-up. Se il nuovo frammento non si apre dopo aver fatto clic su **Crea e apri**, verifica le impostazioni del browser.

## Aggiungi contenuti al frammento di contenuto {#add-content}

Dopo aver salvato e aperto il nuovo frammento di contenuto, l’editor frammento di contenuto si aprirà in una nuova scheda. Qui puoi aggiungere il contenuto del nuovo frammento.

1. L’editor Frammento di contenuto mostra i campi definiti nel modello selezionato. Qui puoi aggiungere contenuto a ogni campo per completare il frammento di contenuto. L’avanzamento viene salvato automaticamente.

1. Fornisci un **Titolo** per il frammento inserendo `Tuscan Adventure`.

1. Fornisci una **Descrizione** per il frammento incollandola nel testo seguente.

   ```text
   Visiting Tuscany on a bicycle is about experiencing the old world charm of Italy on your own terms. Your efforts on the climbs of Italy's rolling hills during this tour are rewarded with sunny Mediterranean landscapes and unmatched Italian hospitality. Tuscany's natural wonders have always been a well of inspiration for arts and culture. Find out why as you explore the Italian countryside and coastline on bicycle.
   ```

1. Fornisci un **Prezzo** per il frammento inserendo `$700`.

1. Fornisci un’**Immagine** rappresentativa del viaggio toccando o facendo clic su **Aggiungi risorsa** nel campo **Immagine**.

1. Nella finestra a comparsa della risorsa, seleziona **Sfoglia risorse** per selezionarne una esistente nella libreria delle risorse.

   ![Aggiungi risorsa](assets/do-not-localize/add-asset.png)

1. Viene visualizzata la finestra di dialogo **Seleziona risorsa**. Utilizzando il navigatore ad albero nel pannello a sinistra, passa a **All assets** > **aem-demo-assets** > **en** > **adventures** > **cycling-tuscany** (Tutte le risorse > aem-demo-assets > it > avventure > ciclismo-toscana).

1. I contenuti della cartella **cycling-tuscany** (ciclismo-toscana) vengono visualizzati a destra. Seleziona l’immagine `ADOBESTOCK_141786166.JPEG`.

1. Scegli **Seleziona**.

   ![Seleziona risorsa](assets/do-not-localize/select-asset.png)

1. L’immagine selezionata viene visualizzata nel frammento di contenuto. Le modifiche vengono salvate automaticamente dall’editor.

1. Al termine, seleziona il pulsante **Pubblica** in alto a destra nell’editor. Questo rende il frammento di contenuto disponibile per il consumo da parte di app esterne. Seleziona **Adesso** dal menu a discesa. Puoi anche pianificarlo per la pubblicazione in un secondo momento.

   ![Pubblica contenuto](assets/do-not-localize/publish.png)

1. Viene visualizzata la finestra di dialogo **Pubblica frammenti di contenuto**. AEM esegue automaticamente un controllo di riferimento per verificare che tutte le risorse necessarie siano pubblicate per il frammento di contenuto. In questo caso, dovrai anche pubblicare il modello creato. Seleziona **Pubblica**.

   ![Controllo di pubblicazione e riferimento](assets/do-not-localize/publish-confirm.png)

1. La pubblicazione è confermata da un banner.

Il contenuto è pubblicato e pronto per essere consegnato all’app o al sito web come frammento di contenuto.
