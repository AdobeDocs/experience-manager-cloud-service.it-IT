---
title: Modelli per creare pagine modificabili con l’Editor universale
description: Scopri come creare modelli da utilizzare per creare pagine modificabili con Universal Editor, risparmiando tempo e garantendo un branding coerente.
solution: Experience Manager Sites
feature: Authoring
role: User
exl-id: f0d60086-e92e-4492-ad50-bef84fed2a82
source-git-commit: 3238b11cdd891cf18048199d4103397e3af75edf
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 26%

---


# Modelli per creare pagine modificabili con l’Editor universale {#page-templates}

Scopri come creare modelli da utilizzare per creare pagine modificabili con Universal Editor, risparmiando tempo e garantendo un branding coerente.

>[!NOTE]
>
>[Sono disponibili anche modelli per la creazione di pagine modificabili con Editor pagina](/help/sites-cloud/authoring/page-editor/templates.md).

## Che cosa sono i modelli di pagina? {#what-are}

Le linee guida di branding e marketing spesso impongono layout particolari per le pagine di contenuti. Spesso è anche una realtà pratica che molte delle tue pagine condividano la stessa struttura e layout. Per risparmiare tempo agli autori di contenuti, le pagine possono essere create dai modelli.

I modelli di pagina fungono da copie master dei layout di pagina. Quando crei una pagina da un modello, il contenuto iniziale del modello viene copiato nella nuova pagina, consentendo di predefinire il layout e il contenuto di base della pagina per l’autore di contenuto, risparmiando tempo.

## Abilitazione dei modelli di pagina {#enabling-templates}

Per utilizzare i modelli per la creazione di pagine modificabili con l’Editor universale, è necessario abilitare l’opzione.

Innanzitutto, abilita i modelli modificabili per la configurazione del sito.

1. Utilizza la console **Sites** e [seleziona la directory principale del tuo sito](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources).
1. Dopo aver selezionato la directory principale del sito, tocca o fai clic sull&#39;icona [**Proprietà**](/help/sites-cloud/authoring/sites-console/page-properties.md) nella barra degli strumenti.
1. Nella scheda **Avanzate** della finestra di dialogo delle proprietà, prendi nota del valore nel campo **Configurazione cloud**.
1. Dalla navigazione principale, scegli **Strumenti** -> **Generale** -> **Browser configurazioni**.
1. Nel **[Browser configurazioni](/help/implementing/developing/introduction/configurations.md)**, seleziona la configurazione indicata nel passaggio precedente e tocca o fai clic su **Proprietà** nella barra degli strumenti.
1. Nella finestra **Proprietà di configurazione**, seleziona l&#39;opzione **Modelli modificabili**.
1. Tocca o fai clic su **Salva e chiudi**.

Una volta abilitata la configurazione, devi consentire i modelli per il sito.

1. Utilizza la console **Sites** e [seleziona la directory principale del tuo sito](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources).
1. Dopo aver selezionato la directory principale del sito, tocca o fai clic sull&#39;icona [**Proprietà**](/help/sites-cloud/authoring/sites-console/page-properties.md) nella barra degli strumenti.
1. Nella scheda **Advanced** della finestra di dialogo delle proprietà nella sezione **Template Settings**, tocca o fai clic sul pulsante **Add**.
1. Nel nuovo campo vuoto visualizzato in **Modelli consentiti**, aggiungi il percorso `/conf/<site>/settings/wcm/templates/.*`.
1. Tocca o fai clic su **Salva e chiudi**.

È ora possibile utilizzare i modelli per creare pagine per il sito. Questa operazione deve essere eseguita una sola volta per ogni sito/configurazione in cui si desidera utilizzare i modelli durante la creazione di pagine modificabili con Universal Editor.

## Creazione di un nuovo modello {#create-new}

È possibile [creare una nuova pagina](/help/sites-cloud/authoring/sites-console/creating-pages.md) da utilizzare come modello oppure utilizzare una pagina esistente come base di un modello.

1. Utilizza la console **Sites** per [passare alla pagina nuova o esistente](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources) che desideri utilizzare come modello e tocca o fai clic su di essa per selezionarla.

1. Dopo aver selezionato la pagina, tocca o fai clic sull&#39;icona [**Proprietà**](/help/sites-cloud/authoring/sites-console/edit-page-properties.md) nella barra degli strumenti.

1. Nella scheda **Avanzate** della finestra di dialogo delle proprietà nella sezione **Impostazioni modello**, seleziona l&#39;opzione **Usa pagina come modello**.

1. Tocca o fare clic su **Salva e chiudi**.

Puoi ora utilizzare la nuova pagina come modello durante la creazione di nuove pagine.

## Creazione di una pagina da un modello {#creating-from-template}

La creazione di una pagina da un modello modificabile con l&#39;Editor universale equivale al flusso di lavoro di [creazione di qualsiasi altra pagina](/help/sites-cloud/authoring/sites-console/creating-pages.md).

1. Utilizza la console **Sites** per [passare al percorso](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources) in cui desideri creare la nuova pagina.

1. Tocca o fai clic su **Crea** -> **Pagina**.

1. Nella scheda **Modello** della procedura guidata **Crea pagina**, è possibile selezionare il modello su cui basare la nuova pagina. Tocca o fai clic sul modello per selezionarlo, quindi tocca o fai clic su **Successivo**.

Completa la procedura guidata come faresti per qualsiasi altra pagina e hai creato la nuova pagina in base al modello selezionato.

## Pagine e modelli {#pages-vs-templates}

I modelli di pagina definiscono solo il contenuto iniziale delle pagine. Le pagine sono quindi completamente modificabili con l’Editor universale.

* Le pagine create da modelli di pagina sono copie indipendenti del modello.
* Se il modello cambia, le pagine esistenti basate su quel modello non cambiano.
* L’autore del contenuto può modificare e aggiornare il contenuto della pagina risultante, se necessario, senza limitazioni dal modello.

## Modelli modificabili {#editable-templates}

Anche le pagine create con [Editor pagina](/help/sites-cloud/authoring/page-editor/introduction.md) possono essere basate su modelli. I modelli utilizzati per la creazione di pagine per l&#39;Editor universale e l&#39;Editor pagina sfruttano entrambi i [modelli modificabili](/help/implementing/developing/components/templates.md) di AEM.

I modelli utilizzati per creare pagine modificabili con Editor pagina utilizzano tutte le funzioni dei modelli modificabili. I modelli utilizzati per creare pagine modificabili con Universal Editor utilizzano solo la funzione di contenuto iniziale.
