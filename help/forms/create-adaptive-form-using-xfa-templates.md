---
title: Come si crea un modulo adattivo basato su componenti core utilizzando i modelli di modulo XFA?
description: Scopri come creare un modulo adattivo utilizzando  [!DNL Experience Manager Forms] i modelli di modulo XFA o i file XDP.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
exl-id: f3c9b798-8b20-4674-9b96-a3a0b143d947
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 16%

---

# Creare un modulo adattivo (componenti core) basato su modelli di modulo XFA

<span class="preview"> La funzionalità è disponibile nel programma di adozione anticipata. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

AEM as a Cloud Service offre agli utenti la possibilità di creare Forms adattivo basato su componenti core utilizzando modelli di modulo XFA (XML Forms Architecture) o file `*.XDP` (XML Data Package). Questa funzione consente agli utenti di risparmiare tempo eseguendo la migrazione dei campi dal modello di modulo XFA o dai file XDP direttamente in Adaptive Forms.

Puoi riutilizzare il modello di modulo XFA o i modelli di modulo per file XDP per creare Forms adattivo basato su componenti core. Per riutilizzare, carica e associa un modello di modulo XFA o file XDP a un modulo adattivo. Gli elementi del modello di modulo XFA o dei file XDP diventano disponibili per l’utilizzo nel Finder di contenuti durante la creazione di moduli adattivi. Da Content Finder è possibile trascinare e rilasciare gli elementi del modello di modulo nel modulo.

## Vantaggi della creazione di moduli basati su modelli di moduli XFA o file XDP

Alcuni dei vantaggi della creazione di moduli basati su modelli di moduli XFA o su file XDP sono:

* **Risparmio di tempo**: puoi riutilizzare rapidamente i modelli di modulo XFA esistenti (file XDP) senza dover ricreare la struttura del modulo, risparmiando tempo e fatica durante il processo di authoring.
* **Migrazione semplificata**: se disponi già di modelli di modulo XFA in uso, questa opzione fornisce un facile percorso di migrazione ad Adaptive Forms, consentendoti di sfruttare i vantaggi dei moderni componenti core di AEM senza perdere i dati e la logica del modulo esistenti.
* **Esperienza utente migliorata**: i Forms adattivi sono più reattivi e personalizzabili dei moduli XFA. Passando ad Adaptive Forms, puoi garantire un’esperienza più semplice da usare su diversi dispositivi e dimensioni di schermo.
* **Integrazione migliorata**: Forms adattivo si integra meglio con altre funzioni, quali flussi di lavoro, associazione dati e invio di moduli, consentendo flussi di lavoro più fluidi e una migliore gestione complessiva dei moduli.

## Prerequisiti

Per creare un modulo adattivo basato su componenti core utilizzando modelli di modulo XFA o file XDP, è necessario quanto segue:

* [Abilita i componenti core adattivi di Forms per il tuo ambiente](enable-adaptive-forms-core-components.md).
* Si raccomanda di acquisire familiarità con le seguenti aree:
   * Creazione di un modulo adattivo
   * XFA (XML Forms Architecture)

## Come si crea un modulo adattivo utilizzando modelli di modulo XFA o file XDP?

Per creare un modulo adattivo utilizzando modelli di modulo XFA o XDP, effettua le seguenti operazioni:

1. Accedi all&#39;istanza dell&#39;autore [!DNL Experience Manager Forms].
1. Inserisci le credenziali nella pagina di accesso di Experience Manager. Dopo aver effettuato l’accesso, nell’angolo in alto a sinistra seleziona **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.

   ![Forms e documenti](/help/forms/assets/create-fdm.png)

1. Selezionare **[!UICONTROL Crea]** > **[!UICONTROL Forms adattivo]**.

   ![Crea modulo adattivo](/help/forms/assets/create-af.png)

   Viene visualizzata la procedura guidata di creazione del modulo.
1. Nella scheda **Source**, seleziona un modello basato su Componenti core.

   ![Seleziona modello](/help/forms/assets/select-template.png)

   Quando selezioni un modello, un tema e un&#39;azione di invio specificati nel modello vengono selezionati automaticamente e il pulsante **[!UICONTROL Crea]** è abilitato.

   ![Seleziona tema](/help/forms/assets/select-form-theme.png)

1. Seleziona **[!UICONTROL Crea]**. Viene visualizzata una finestra di dialogo che specifica il titolo, il nome e la posizione in cui salvare il modulo adattivo.
1. Specifica il titolo, il nome e la posizione.
1. Seleziona **[!UICONTROL Crea]**.
   ![Fornisci nome e titolo](/help/forms/assets/create-form.png)

   Viene creato un modulo adattivo che viene aperto nell’editor di moduli adattivi. L’editor visualizza i contenuti disponibili nel modello.
1. Seleziona ![Informazioni pagina](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Apri proprietà]**.

   ![Apri proprietà](/help/forms/assets/form-properties.png)

   Viene visualizzata la pagina Proprietà modulo.
1. Vai alla scheda **[!UICONTROL Modello modulo]** e scegli **Modelli modulo**.
1. Selezionare il file XDP dall&#39;elenco a discesa.

   ![Seleziona file XDP](/help/forms/assets/select-xdp-file.png)

   Sullo schermo viene visualizzata una finestra di avviso. Fare clic su **OK** per continuare.

   ![Finestra di dialogo di avviso](/help/forms/assets/fdm-warning.png)

1. Seleziona **[!UICONTROL Salva e chiudi]** per salvare le proprietà.

   >[!NOTE]
   >
   > Dopo aver selezionato **Modelli modulo** nella scheda Modulo **Modello**, non è possibile modificarli.


Viene creato un modulo adattivo che viene aperto nell’editor di moduli adattivi. L’editor mostra i contenuti disponibili nel modello.  In base al tipo di modulo adattivo, gli elementi del modulo presenti nel modello di modulo XFA associato vengono visualizzati nella scheda **[!UICONTROL Oggetti modello dati]** di **[!UICONTROL Browser contenuto]** nella barra laterale. Puoi anche trascinare questi elementi per creare il modulo adattivo.

>[!NOTE]
>
> Puoi disattivare gli script per i campi del modulo XDP utilizzando la barra degli strumenti del pannello del campo aggiunto. Creare logiche per i campi aggiunti utilizzando [Editor regole visive](/help/forms/rule-editor-core-components.md).

