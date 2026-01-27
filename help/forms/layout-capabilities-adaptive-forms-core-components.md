---
title: Quali sono le funzionalità di layout di Adaptive Forms basate sui componenti core?
description: Il layout e l’aspetto di Adaptive Forms su vari dispositivi sono regolati dalle impostazioni di layout. Comprendere i vari layout e come applicarli.
feature: Adaptive Forms, Core Components
keywords: Layout del modulo adattivo basato su componenti core, layout diversi per i moduli, layout di moduli dinamici AEM, layout di moduli di AEM Cloud Service, tipi di layout di moduli nei componenti core di AEM, layout di moduli adattivi
role: User, Developer, Admin
exl-id: dcc01d84-0d39-4fa8-ac47-71a9aba91b1e
source-git-commit: 5b55a280c5b445d366c7bf189b54b51e961f6ec2
workflow-type: tm+mt
source-wordcount: '2142'
ht-degree: 16%

---

# Funzionalità di layout di Forms adattivo basate sui componenti core


| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/layout-capabilities-adaptive-forms.html?lang=it) |
| AEM as a Cloud Service (componenti di base) | [Fai clic qui](/help/forms/layout-capabilities-adaptive-forms.md) |
| AEM as a Cloud Service (componenti core) | Questo articolo |

Adaptive Forms fornisce componenti di prima classe per il layout e la progettazione efficace dei moduli. Il layout controlla il modo in cui i componenti vengono visualizzati in un modulo. Forms adattivo supporta vari layout: pannello, procedura guidata, pannello a soffietto, schede nelle schede superiore/orizzontale e schede nelle schede sinistra/verticale.

<!-- ![Types of Layout](/help/forms/assets/generic-layout-hero-image.png){align="center"}-->

## Applicabilità e casi d’uso

### Assicurazione

## AEM Forms supporta i moduli di richiesta di risarcimento assicurativo in più fasi?

Sì. AEM Forms supporta moduli adattivi guidati in più passaggi con logica condizionale, consentendo agli assicuratori di raccogliere informazioni sulle richieste di rimborso in modo progressivo in base al tipo e al contesto.

## I clienti possono caricare in modo sicuro i documenti di richiesta di risarcimento utilizzando AEM Forms?

Sì. AEM Forms supporta il caricamento sicuro dei documenti durante l’invio dei moduli, con controlli di accesso e gestione sicura dei dati allineati ai requisiti di sicurezza aziendali.


## Tipi di layout Forms adattivi

Il modulo adattivo basato su componenti core supporta i seguenti tipi di layout:

* **Layout pannello**
* **Layout guidato**
* **Layout verticale**
* **Layout orizzontale**
* **Layout Accordion**

>[!BEGINTABS]

>[!TAB Layout pannello]

Il layout pannello è utile per organizzare i campi correlati in modo da semplificare la navigazione e la ricerca del contenuto corrispondente. Il layout del pannello dispone i componenti del modulo all’interno di sezioni o pannelli distinti in un modulo adattivo.

![Layout pannello](/help/forms/assets/panel-layout.png)

Layout pannello

È possibile utilizzare il [componente pannello](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) per aggiungere il layout pannello in un modulo. Per istruzioni dettagliate su come configurare varie proprietà del componente pannello, consulta l’articolo [Componente pannello](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel).

>[!TAB Layout procedura guidata]

Il layout procedura guidata semplifica un modulo complesso suddividendolo in passaggi distinti. Ogni passaggio rappresenta una parte diversa del processo e gli utenti possono spostarsi tra i passaggi in sequenza, spesso con i pulsanti **Successivo** e **Precedente**. È possibile utilizzare il layout procedura guidata per creare un modulo che comprende più sezioni o passaggi.

![Layout procedura guidata](/help/forms/assets/wizard-layout-compare.gif)

Layout procedura guidata

È possibile utilizzare il [componente procedura guidata](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard) per aggiungere il layout procedura guidata in un modulo. Per istruzioni dettagliate su come configurare le varie proprietà del componente procedura guidata, consulta l’articolo [Componente procedura guidata](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard).

>[!TAB Layout schede verticale]

Il layout delle schede verticali è noto anche come tabulazioni nel layout sinistro. Il layout tabulazioni verticali organizza pannelli o sezioni lungo il lato sinistro di un modulo. Si tratta di un layout comune per i moduli in cui pannelli/sezioni sono impilati verticalmente per facilitarne la lettura e la navigazione.

![Layout verticale](/help/forms/assets/vertical-tab.gif)

Layout schede verticali

È possibile utilizzare il componente [schede verticali](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs) per aggiungere il layout delle schede verticali in un modulo. Per istruzioni dettagliate su come configurare le varie proprietà del componente Schede verticali, consulta l&#39;articolo [Componente Schede verticali](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs).


>[!TAB Layout schede orizzontali]

Il layout delle schede orizzontali è noto anche come Tabulazioni nel layout superiore. Il layout tabulazioni orizzontali dispone i pannelli o le sezioni affiancate in una riga. Questo layout presenta le sezioni del modulo in modo lineare per tutta la larghezza del modulo o del pannello.


![Layout orizzontale](/help/forms/assets/horizontal-layout.gif)

Layout schede orizzontali

È possibile utilizzare il componente [schede orizzontali](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs) per aggiungere il layout delle schede orizzontali in un modulo. Per istruzioni dettagliate su come configurare le varie proprietà del componente schede orizzontali, consulta l&#39;articolo [componente schede orizzontali](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs).


>[!TAB Layout pannello a soffietto]

Il layout pannello a soffietto mostra il contenuto in sezioni o pannelli comprimibili in un modulo adattivo. Quando una sezione viene espansa, viene mostrato il contenuto all’interno, mentre le altre sezioni rimangono compresse. Questo layout è ideale per visualizzare grandi quantità di informazioni in un formato compatto.

![Layout pannello a soffietto](/help/forms/assets/accordion-layout-compare.gif)

Layout pannello a soffietto

È possibile utilizzare il [componente pannello a soffietto](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion) per aggiungere il layout pannello a soffietto in un modulo. Per istruzioni dettagliate su come configurare le varie proprietà del componente pannello a soffietto, consulta l’articolo [Componente pannello a soffietto](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion).

>[!ENDTABS]

Per informazioni su come inserire un layout e aggiungervi componenti modulo, consultare la sezione [Come inserire un layout e aggiungervi componenti modulo?](#how-to-insert-a-layout-and-add-form-components-to-it)

### Come scegliere il layout corretto per i moduli adattivi?

È importante selezionare il layout corretto per il modulo adattivo per ottimizzare l’esperienza utente e la funzionalità dei moduli. La tabella ti aiuta a comprendere le diverse opzioni di layout disponibili e ti guida nella selezione del layout più adatto in base alle tue esigenze e ai tuoi casi d’uso specifici:

| Funzione | Layout pannello | Layout procedura guidata | Schede nel layout Schede superiori/verticali | Schede nel layout Schede a sinistra/orizzontale | Layout pannello a soffietto |
|--------------------------|-----------------------------------------------------|----------------------------------------------------|-----------------------------------------------------|--------------------------------------------------------|--------|
| **Scopo** | Raggruppa il contenuto correlato in sezioni distinte | Guida gli utenti attraverso un processo o un modulo in più fasi | Consente il passaggio tra sezioni/viste sulla stessa pagina | Simile alle schede superiori ma disposte verticalmente a sinistra | Organizza il contenuto in sezioni comprimibili |
| **Struttura** | Sezioni distinte | Passaggi/pagine sequenziali | Schede orizzontali nella parte superiore | Schede verticali a sinistra | Pannelli/sezioni comprimibili |
| **Navigazione** | Fai clic sulle intestazioni del pannello per spostarti | - In avanti: pulsante “Avanti”<br>- All’indietro: pulsante “Indietro”<br>- Salto dei passaggi facoltativo | Fai clic sulle schede per cambiare sezione | Fai clic sulle schede per cambiare sezione | Fai clic sulle intestazioni per espandere/comprimere le sezioni |
| **Esperienza utente** | Organizza grandi quantità di contenuti in modo gestibile | Guida dettagliata, riduzione del sovraccarico | Passaggio da una visualizzazione all&#39;altra chiaro e accessibile | Utilizzo efficiente dello spazio verticale, schede sempre visibili | Vista compatta con sezioni espanse/compresse |
| **Caso d’uso** | Moduli complessi con sezioni suddivise in categorie | Processi di configurazione, moduli complessi | Organizzazione delle impostazioni o delle categorie di contenuto | Dashboard, visualizzazioni dati complesse | Domande frequenti, menu delle impostazioni e sezioni contenuto dettagliate |


## Come si inserisce un layout e vi si aggiungono i componenti del modulo?

Nel diagramma seguente vengono illustrati i passaggi necessari per inserire un layout in un modulo e aggiungervi componenti modulo:

![Flusso di lavoro per aggiungere un layout e componenti modulo](/help/forms/assets/workflow-to-add-component-to-a-layout.png)

Considera il **modulo di richiesta IT** visualizzato nella sezione [Tipi di layout di Forms adattivi](#adaptive-forms-layout-types). Il modulo raccoglie informazioni dai dipendenti che riscontrano problemi tecnici relativi alla rete o al notebook. Include tre pannelli:

* **Dettagli dipendente**: il pannello raccoglie informazioni sul dipendente e contiene tre caselle di testo con etichetta Nome, ID e-mail e Reparto.

* **Dettagli del problema**: il pannello acquisisce i dettagli del problema. Include una casella di controllo per la categoria del problema con tre opzioni: Rete, Computer o Altro. Sono inoltre presenti due caselle di testo con l&#39;etichetta Please Specify (Specifica) e Comments (Commenti).

* **Allegati**: il pannello consente agli utenti di caricare documenti di supporto relativi al problema.

Esaminiamo il processo dettagliato per l’inserimento di un layout e l’aggiunta di componenti. In questo esempio, in un modulo viene inserito un layout con schede orizzontali.

### &#x200B;1. Inserire un componente layout in un modulo

1. Accedi all&#39;istanza [!DNL Experience Manager Forms].
1. Nell&#39;angolo superiore sinistro selezionare **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Apri un modulo adattivo esistente in modalità di modifica, se è già stato creato.

   ![Aprire un modulo adattivo](/help/forms/assets/insert-layout.png)

   In alternativa, puoi anche [creare un nuovo modulo adattivo](/help/forms/creating-adaptive-form-core-components.md).

1. Individua la sezione all’interno del generatore di moduli che consente di aggiungere un layout.

   ![Generatore di moduli](/help/forms/assets/form-editor.png)
1. Fai clic sull&#39;icona **Aggiungi**. L’icona è un segno più (+) che indica l’opzione per aggiungere nuovi componenti.

   ![Inserisci layout](/help/forms/assets/insert-layout-add-icon.png)

   Facendo clic sull&#39;icona **Aggiungi** viene visualizzata una finestra di dialogo **Inserisci nuovo componente** in cui sono visualizzati vari componenti da inserire.

   >[!NOTE]
   >
   > In alternativa, puoi anche [trascinare e rilasciare il componente layout](#extra-bytes).

1. Sfoglia i componenti disponibili nella finestra di dialogo e seleziona il layout desiderato dall’elenco. Nel nostro caso, selezioniamo il componente Schede orizzontali per inserire il layout delle schede orizzontali.

   ![Seleziona schede orizzontali](/help/forms/assets/select-horizontal-tab.png)

   Quando si aggiunge al modulo il componente Schede orizzontali, inizialmente è costituito da due pannelli vuoti, denominati Item1 e Item2, per impostazione predefinita. Devi aggiungere manualmente i componenti del modulo a questi pannelli.

   ![Schede orizzontali](/help/forms/assets/insert-tabs-on-top.png)

1. Apri le proprietà del componente Schede orizzontali e specifica il nome del componente.
Ad esempio, in questo caso, aggiungiamo il nome del componente Schede orizzontali come Modulo di richiesta IT.

   ![Aggiungi nome per schede orizzontali](/help/forms/assets/change-name-of-horizontal-tabs.png)

1. Fai clic su **Fine**.

   ![Schede orizzontali](/help/forms/assets/tabs-on-top-rename-component.png)

Una volta aggiunto il componente layout nel modulo, modifica il numero di pannelli in base ai requisiti.

### &#x200B;2. Aggiungere pannelli al layout

Aggiungi un nuovo pannello al componente Schede orizzontali:

1. Apri le proprietà del componente Schede orizzontali e fai clic sulla scheda **Elementi**.

   ![Scheda elemento per schede orizzontali](/help/forms/assets/tabs-on-top-items-tab.png)

1. Fai clic sull&#39;icona **Aggiungi** per aggiungere un nuovo pannello.

   ![Aggiungi nuovo pannello](/help/forms/assets/tabs-on-top-add-panel.png)

   Quando si fa clic sull&#39;icona **Aggiungi**, viene visualizzata la finestra di dialogo **Inserisci nuovo componente**.

1. Seleziona il componente del pannello.

   ![Aggiungi nuovo pannello](/help/forms/assets/tabs-on-top-new-panel.png)

   Quando selezioni il componente pannello, il nuovo pannello viene aggiunto nel layout orizzontale.

   ![Aggiungi nuovo pannello](/help/forms/assets/tabs-on-top-add-new-panel.png)

   Assegna un nome al nuovo pannello. In caso contrario, non puoi salvare le proprietà del componente Schede orizzontali.

1. Specificate i nomi dei pannelli come mostrato nella figura riportata di seguito:

   ![Nomi pannello](/help/forms/assets/tabs-on-tops-panel-name.png)

1. Fai clic su **Fine**.

   Dopo aver fatto clic su **Fine**, i tre pannelli vengono visualizzati affiancati in una riga. I nomi dei pannelli vengono visualizzati come intestazioni per ciascun pannello e puoi aggiungere componenti modulo a ciascun pannello.

   ![Nomi pannello](/help/forms/assets/tabs-on-top-initial-view.png)

   Puoi configurare le proprietà del componente pannello. Ad esempio, il modulo di richiesta IT non include i titoli dei pannelli, ecco i passaggi per configurare le proprietà del componente pannello.

1. Apri le proprietà del primo pannello.

   ![Proprietà pannello 1](/help/forms/assets/tabs-on-tops-panel1-properties.png)

1. Selezionare la casella di controllo **Nascondi titolo** dalla scheda **Base**.

   ![Nascondi titolo](/help/forms/assets/tabs-on-top-hide-panel.png)

1. Fai clic su **Fine**.

Allo stesso modo, potete nascondere i titoli anche per gli altri due pannelli. Al termine, puoi procedere con l’aggiunta di componenti modulo a ciascun pannello.

### &#x200B;3. Aggiungere componenti modulo al pannello

<!-- You can employ one of the following method to add form components to the panel:
* [Add components to a layout's panel using the Add icon](#add-components-to-a-layouts-panel-using-the-add-icon)
* [Drag and drop components into a layout's panel](#drag-and-drop-components-into-a-layouts-panel) -->

1. Individua la sezione all’interno del pannello che consente di aggiungere componenti.
1. Fai clic sull&#39;icona **Aggiungi**. L’icona è un segno più (+) che indica l’opzione per aggiungere nuovi componenti.
   ![Inserisci layout](/help/forms/assets/tabs-on-top-add-component.png)

   Facendo clic sull&#39;icona **Aggiungi** viene visualizzata una finestra di dialogo **Inserisci nuovo componente** in cui sono visualizzati vari componenti da inserire.

   ![Finestra di dialogo Inserisci nuovo componente](/help/forms/assets/insert-new-component.png)

1. Sfoglia i componenti disponibili nella finestra di dialogo che viene visualizzata e seleziona il componente desiderato. Nel nostro caso, seleziona il componente Casella di testo.
1. Apri le proprietà del componente aggiunto e specifica il nome. Consente di modificare le proprietà del componente Casella di testo aggiunto e di specificarne il nome.
   ![Inserisci layout](/help/forms/assets/tabs-on-top-textbox-component.png)
1. Allo stesso modo, aggiungi altri due componenti Casella di testo e assegna ai componenti un nome ID e-mail e un Reparto.\
   ![Primo pannello](/help/forms/assets/tabs-on-tops-first-panel.png)

   Dopo aver aggiunto i componenti nel primo pannello, puoi procedere con l’aggiunta dei componenti al secondo pannello.

1. Per cambiare pannello, fare clic su **Seleziona pannello** nella barra degli strumenti.

   ![Pannello Switch](/help/forms/assets/tabs-on-top-select-panel.png)

   Quando fai clic su **Seleziona pannello**, viene visualizzato l&#39;elenco dei pannelli aggiunti nel componente Schede orizzontali.

   ![Pannello Switch](/help/forms/assets/tabs-on-tops-panel2.png)

1. Selezionare **2 pannello** dall&#39;elenco dei pannelli e la visualizzazione cambia dal primo pannello al secondo.

   ![Secondo pannello](/help/forms/assets/tabs-on-top-panel2-component.png)

1. Ripetete i passi descritti dal punto 2 al punto 4 per aggiungere i componenti desiderati nel pannello 2 come mostrato nella figura seguente:

   ![Componenti del secondo pannello](/help/forms/assets/panel-2-components.png)

1. Passare al pannello **3** seguendo i passaggi descritti nei passaggi 6 e 7.

1. Ripeti i passaggi descritti dal passaggio 2 al passaggio 4 per aggiungere il componente desiderato nel pannello 3:

   ![Componenti del terzo pannello](/help/forms/assets/panel-3-component.png)

1. Fai clic su **[!UICONTROL Anteprima]** nell&#39;angolo in alto a destra dell&#39;ambiente di authoring.
   ![Layout orizzontale](/help/forms/assets/horizontal-layout.gif)

Puoi anche [trascinare i componenti](#extra-bytes) per aggiungere i componenti del modulo a ciascun pannello.


<!-- #### Drag and drop components into a layout's panel 

1. Locate the section within the panel that allows you to add components. 
2. Navigate to the left panel within your authoring environment and click **Components**.

    ![Component Panel](/help/forms/assets/add-new-component.png){width="200" align="center"}

    When you click the **Components** option, the list of the available components appears.   

    ![Component Panel](/help/forms/assets/add-new-component2.png){width="200" align="center"}

3. Browse the available components and select the Text Box component.

4. Drag the component by clicking and holding the selected component, then drag it over to the panel area to place it.

5. Drop the component into the panel by releasing the mouse. 

6. Open the properties of the added Text Box component and specify its name as Name.
    ![Insert layout](/help/forms/assets/tabs-on-top-textbox-component.png){width="200" align="center"}
7. Similarly, add two more Text Box components and name added the components as Email ID and Department.   
    ![First Panel](/help/forms/assets/tabs-on-tops-first-panel.png){width="200" align="center"}

    Now that the components in the first panel have been added, you can proceed with adding the components to the second panel. 

8. To switch the panel, click **Select Panel** from the toolbar. 

    ![Switch Panel](/help/forms/assets/tabs-on-top-select-panel.png){width="200" align="center"}

    When you click the **Select Panel**, the list of the added panels in the Horizontal Tabs component appears.

    ![Switch Panel](/help/forms/assets/tabs-on-tops-panel2.png){width="200" align="center"}

9. Select **2 Panel** from the panel list and the view changes from the first panel to the second panel.

    ![Second Panel](/help/forms/assets/tabs-on-top-panel2-component.png){width="200" align="center"}

10. Repeat the steps outlined from Step 2 to Step 6 for adding the desired components in panel 2 as shown in the below figure:   

     ![Second Panel components](/help/forms/assets/panel-2-components.png){width="200" align="center"}

11. Switch to the **3 Panel** by following the steps outlined in Step 8 and Step 9.

12. Repeat the steps outlined from Step 2 to Step 6 for adding the desired component in panel 3:

    ![Third Panel components](/help/forms/assets/panel-3-component.png){width="200" align="center"} 

    -->



Puoi anche eliminare il componente modulo dal pannello utilizzando l&#39;icona ![Elimina](/help/forms/assets/Smock_Delete_18_N.svg).

![Eliminazione di un componente](/help/forms/assets/delete-component.png)

Puoi anche aggiungere le convalide richieste per i componenti, in base alle esigenze.

## Come si sostituisce un layout esistente con un nuovo layout?

È possibile sostituire un layout di un modulo con un nuovo layout, che comporta la modifica della disposizione e della visualizzazione dei componenti all’interno di un modulo.

Per sostituire il layout esistente di un modulo, effettuare le seguenti operazioni:

1. Fare clic sull&#39;icona Sostituisci nella barra degli strumenti del componente layout per visualizzare la finestra di dialogo **[!UICONTROL Sostituisci componente]**.

   ![Sostituisci layout](/help/forms/assets/replace-layout.png)

1. Selezionare il layout desiderato dalla finestra di dialogo **[!UICONTROL Sostituisci componente]**.

   ![Finestra di dialogo Sostituisci componente](/help/forms/assets/replace-component.png)

   Dopo aver selezionato il layout, la disposizione dei componenti all’interno del layout cambia di conseguenza. Ad esempio, seleziona il componente Schede verticali dalla finestra di dialogo **[!UICONTROL Sostituisci componente]**; la disposizione del pannello cambia in Schede a sinistra:

   ![Layout verticale](/help/forms/assets/vertical-tab.gif)

## Byte aggiuntivi

Per trascinare i componenti nel generatore di moduli, effettua le seguenti operazioni:

1. Individua la sezione che ti consente di aggiungere componenti.
1. Passa al pannello a sinistra nell&#39;ambiente di authoring e fai clic su **Componenti**.

   ![Pannello Componenti](/help/forms/assets/add-new-component.png)

   Quando si fa clic sull&#39;opzione **Componenti**, viene visualizzato l&#39;elenco dei componenti disponibili.

   ![Pannello Componenti](/help/forms/assets/add-new-component2.png)

1. Sfoglia i componenti disponibili e seleziona il componente desiderato.

1. Trascina il componente facendo clic e tenendo premuto il pulsante, quindi trascinalo sull’area del pannello per posizionarlo.

1. Rilascia il componente nel pannello rilasciando il mouse.

## Passaggi successivi

Una volta acquisite familiarità con le varie funzionalità di layout di un modulo adattivo basato su componenti core, puoi procedere con i passaggi successivi:

* [Creare il primo modulo adattivo basato su componenti core](/help/forms/creating-adaptive-form-core-components.md)
* [Creare e utilizzare i temi del modulo adattivo](/help/forms/using-themes-in-core-components.md)



## Consulta anche

{{see-also}}
