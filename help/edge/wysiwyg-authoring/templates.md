---
title: Utilizzo dei modelli di pagina con l’Editor universale
description: Scopri come creare e utilizzare i modelli di pagina con Universal Editor.
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 773ce75975f4dcc2c5310422bcc377b487ebec25
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 2%

---


# Utilizzo dei modelli di pagina con l’Editor universale {#page-templates}

Scopri come creare e utilizzare i modelli di pagina con Universal Editor.

>[!NOTE]
>
>Questa funzione sarà disponibile in una delle prossime versioni di AEM as a Cloud Service.

## Cosa sono i modelli di pagina? {#what-are}

Le linee guida di branding e marketing spesso impongono layout particolari per le pagine di contenuti. Spesso è anche una realtà pratica che molte delle tue pagine condividano la stessa struttura e layout. Per risparmiare tempo agli autori di contenuti, le pagine possono essere create dai modelli.

I modelli di pagina fungono da copie master dei layout di pagina. Quando crei una pagina da un modello, il contenuto del modello viene copiato nella nuova pagina, consentendo di predefinire il layout e il contenuto iniziale della pagina per l’autore di contenuto, risparmiando tempo.

## Creazione di un modello di pagina {#creating}

Puoi creare un modello di pagina creando una nuova pagina o utilizzando una pagina esistente come modello. In entrambi i casi si utilizza la console [**Sites**.](/help/sites-cloud/authoring/sites-console/introduction.md)

### Creazione di un nuovo modello {#create-new}

1. Utilizza la console **Sites** per passare al percorso in cui desideri creare la nuova pagina da utilizzare come modello e [creare la pagina come faresti con qualsiasi altro utente.](/help/sites-cloud/authoring/sites-console/creating-pages.md)

1. Dopo aver creato la pagina e essere tornato alla console, selezionala e tocca o fai clic sull&#39;icona [**Proprietà**](/help/sites-cloud/authoring/sites-console/page-properties.md) nella barra degli strumenti.

1. Nella scheda **Avanzate** della finestra di dialogo delle proprietà nella sezione **Impostazioni modello**, seleziona l&#39;opzione **Usa come modello**.

1. Nel campo **Nome modello**, fornisci un nome descrittivo.

   * Questo è il nome che mostrerà la creazione di nuove pagine di contenuto e selezioni un modello su cui basare la nuova pagina.

1. Toccare o fare clic su **Salva e chiudi**.

È ora possibile utilizzare la nuova pagina come modello durante la creazione di nuove pagine.

### Utilizzo di una pagina esistente come modello {#existing-page}

1. Utilizza la console **Sites** per [passare alla posizione della pagina](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources) che desideri utilizzare come modello.

1. Seleziona la pagina, quindi tocca o fai clic sull&#39;icona [**Proprietà**](/help/sites-cloud/authoring/sites-console/page-properties.md) nella barra degli strumenti.

1. Nella scheda **Avanzate** della finestra di dialogo delle proprietà nella sezione **Impostazioni modello**, seleziona l&#39;opzione **Usa come modello**.

1. Nel campo **Nome modello**, fornisci un nome descrittivo.

   * Questo è il nome che mostrerà la creazione di nuove pagine di contenuto e selezioni un modello su cui basare la nuova pagina.

1. Toccare o fare clic su **Salva e chiudi**.

È ora possibile utilizzare la pagina selezionata come modello durante la creazione di nuove pagine.

## Creazione di una pagina da un modello {#creating-from-template}

La creazione di una pagina da un modello per l&#39;utilizzo con l&#39;Editor universale è lo stesso flusso di lavoro utilizzato per [la creazione della pagina.](/help/sites-cloud/authoring/sites-console/creating-pages.md)

1. Utilizza la console **Sites** per [passare al percorso](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources) in cui desideri creare la nuova pagina.

1. Tocca o fai clic su **Crea** -> **Pagina**.

1. Nella scheda **Modello** della procedura guidata **Crea pagina**, è possibile selezionare il modello su cui basare la nuova pagina. Tocca o fai clic sul modello desiderato per selezionarlo, quindi tocca o fai clic su **Avanti**.

Completa la procedura guidata come faresti per qualsiasi altra pagina e hai creato la nuova pagina in base al modello selezionato.

## Editor universale e Editor pagina {#page-vs-universal}

I modelli di pagina per l&#39;Editor universale risolvono lo stesso problema dei [ modelli di pagina per l&#39;Editor pagine AEM:](/help/sites-cloud/authoring/page-editor/templates.md) per poter riutilizzare il contenuto per creare rapidamente le pagine in base a un set di layout predefiniti. Tuttavia risolvono il problema in modi molto diversi. Se utilizzi l’Editor pagina, tieni presente queste differenze.

* Le pagine create da modelli di pagine per l’Editor universale sono copie indipendenti del modello.
* Pertanto, se il modello cambia, le pagine risultanti non cambiano.
* L’autore del contenuto può modificare e aggiornare il contenuto della pagina risultante, se necessario, senza limitazioni dal modello.
