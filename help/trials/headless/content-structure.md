---
title: Creare la struttura del contenuto per l’app
description: Scopri come creare la struttura che funge da base per tutti i contenuti headless utilizzando modelli di frammenti di contenuto AEM.
hidefromtoc: true
index: false
exl-id: ace9b9f3-8bc6-4a36-a51c-ff60cdd339ce
source-git-commit: bcab02cbd84955ecdc239d4166ae38e5f79b3264
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Creare la struttura del contenuto per l’app {#content-structure}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview"
>title="Creare la struttura del contenuto per l’app"
>abstract="Seguendo questa serie di guide interattive imparate a creare una struttura, nota come modello per frammenti di contenuto, che funge da base per i contenuti headless."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide"
>title="Avvia la console del modello"
>abstract="Scopriamo come creare uno schema riutilizzabile, denominato modello per frammenti di contenuto, per il contenuto in Adobe Experience Manager as a Cloud Service. Guarda il video per capire perché questo è un passo importante. <br><br>Avvia questo modulo in una nuova scheda facendo clic sul pulsante sottostante e quindi segui questa guida."
>additional-url="https://video.tv.adobe.com/v/3413261" text="Video introduttivo sulla struttura dei contenuti"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide_footer"
>title="Congratulazioni. Hai imparato a creare un modello per frammenti di contenuto per rappresentare la struttura dei dati headless e hai fatto il primo passo per distribuire contenuti omni-channel in modo scalato e standard."
>abstract=""

## Creare un modello {#create-model}

Fai clic su **Avvia la console del modello** questo pulsante consente di aprire la console Modelli di frammento di contenuto in una nuova scheda.

![Console del modello Frammento di contenuto](assets/content-structure/content-fragment-model-console.png)

Considera la console del modello Frammento di contenuto come una libreria di modelli, in cui puoi creare nuovi modelli e gestire quelli esistenti. La console inizia vuota, quindi creiamo un nuovo modello!

1. Nella console del modello Frammento di contenuto , fai clic sul pulsante **Crea** in alto a destra dello schermo per iniziare a creare un modello di frammento di contenuto.

1. Viene avviata la procedura guidata Crea modello, che consente di guidarti.

   ![Procedura guidata del modello Frammento di contenuto](assets/content-structure/model-wizard.png)

   Fornire le informazioni obbligatorie.

   * **Titolo modello** - Questa è una breve descrizione del modello e in genere indica lo scopo del modello.
   * **Abilita modello** - Questa opzione è selezionata per impostazione predefinita e deve essere selezionata per poter creare frammenti di contenuto in base a questo modello.

1. Una volta compilati i campi obbligatori, fai clic su **Crea** in alto a sinistra per creare il modello.

1. La **Completato** viene confermato che il modello è stato creato.

   ![Finestra di dialogo di successo per la creazione di un nuovo modello di frammento di contenuto](assets/content-structure/success.png)

## Aggiungi campi al modello {#configure-model}

Prima di poter utilizzare il modello, è necessario definire la struttura dei relativi dati.

1. Fai clic su **Apri** in **Completato** finestra di dialogo del passaggio precedente per aprire il nuovo modello nell’editor modelli di frammenti di contenuto in cui puoi definirne i campi.

1. Trascina un campo dalla **Tipi di dati** a destra dell’editor e rilascialo sul modello per frammenti di contenuto.

   ![Aggiungere un tipo di dati](assets/content-structure/drop-fields.png)

1. Una volta inserito un tipo di dati, il **Tipi di dati** viene automaticamente modificata nella colonna **Proprietà** , che ti consente di definire i dettagli del tipo di dati appena inserito.

   ![Scheda Proprietà del campo dati](assets/content-structure/data-type-properties.png)

1. Dopo aver aggiunto tutti i campi necessari per il modello Frammento di contenuto, fai clic su **Salva** in alto a destra nella finestra.

Il modello viene salvato e torna alla console del modello a frammenti di contenuto, dove puoi aggiungere altri modelli in base alle necessità.

![Modulo completo](assets/content-structure/content-fragment-model-console-populated.png)
