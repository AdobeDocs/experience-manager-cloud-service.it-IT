---
title: Quali sono le funzionalità di layout di Adaptive Forms?
description: Il layout e l’aspetto di Adaptive Forms su vari dispositivi sono regolati dalle impostazioni di layout. Comprendere i vari layout e come applicarli.
exl-id: e30c6ff9-692b-4415-8f14-b4ef616b2d12
source-git-commit: 57e421a865b664c0adb7af93b33bd4b6b32049ab
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 3%

---

# Funzionalità di layout di Adaptive Forms {#layout-capabilities-of-adaptive-forms}

<span class="preview"> L’Adobe consiglia di utilizzare l’acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [creazione di un nuovo Forms adattivo](/help/forms/creating-adaptive-form-core-components.md) o [aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>


| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/layout-capabilities-adaptive-forms.html) |
| AEM as a Cloud Service | Questo articolo |

[!DNL Adobe Experience Manager] consente di creare Forms adattivo di facile utilizzo che offre esperienze dinamiche agli utenti finali. Il layout del modulo controlla il modo in cui gli elementi o i componenti vengono visualizzati in un modulo adattivo.

<!-- ## Prerequisite knowledge {#prerequisite-knowledge}

Before learning about the different layout capabilities of Adaptive Forms, read [Introduction to authoring forms](introduction-forms-authoring.md) to know more about Adaptive Forms. -->

## Tipi di layout {#types-of-layouts}

Un modulo adattivo offre i seguenti tipi di layout:

**[!UICONTROL Layout pannello]** Controlla il modo in cui gli elementi o i componenti all&#39;interno di un pannello vengono visualizzati su un dispositivo.

**[!UICONTROL Layout dispositivo mobile]** Controlla la navigazione di un modulo su un dispositivo mobile. Se la larghezza del dispositivo è di 768 pixel o più, il layout viene considerato un layout Mobile e ottimizzato per un dispositivo mobile.

**[!UICONTROL Layout barra degli strumenti]** Controlla il posizionamento dei pulsanti di azione nella barra degli strumenti o nel pannello di un modulo.

Tutti questi layout di pannello sono definiti nella `/libs/fd/af/layouts` posizione.

Per modificare il layout di un modulo adattivo, utilizza la modalità Creazione in [!DNL Experience Manager].

## [!UICONTROL Layout pannello] {#panel-layout}

Un autore di moduli può associare un layout a ciascun pannello di un modulo adattivo, incluso il pannello principale.

I layout del pannello sono disponibili all&#39;indirizzo `/libs/fd/af/layouts/panel` posizione. Tocca il pannello e seleziona ![cmppr1](assets/configure-icon.svg) per visualizzare le proprietà del pannello.

![Elenco dei layout del pannello per il pannello principale di un modulo adattivo](assets/layouts.png)

### [!UICONTROL Reattivo - tutto su una pagina senza navigazione] {#responsive-everything-on-one-page-without-navigation-br}

Utilizza questo layout di pannello per creare un layout reattivo che si adatta alle dimensioni dello schermo del dispositivo senza alcuna necessità di navigazione specializzata.

Utilizzando questo layout, è possibile inserire più **[!UICONTROL Modulo adattivo pannello]** componenti uno dopo l’altro all’interno del pannello.

![Un modulo che utilizza il layout dinamico come visualizzato su un piccolo schermo](assets/responsive-layout.png)

### [!UICONTROL Procedura guidata] {#wizard}

Utilizza questo layout di pannello per fornire una navigazione guidata all’interno di un modulo. Utilizzare ad esempio questo layout per acquisire informazioni obbligatorie in un modulo guidando gli utenti passo dopo passo.

Utilizza il **[!UICONTROL Modulo adattivo pannello]** per una navigazione dettagliata all’interno di un pannello. Quando utilizzi questo layout, un utente passa al passaggio successivo solo dopo aver completato il passaggio corrente

```javascript
window.guideBridge.validate([], this.panel.navigationContext.currentItem.somExpression)
```

![Un modulo che utilizza il layout della procedura guidata](assets/wizard-layout2.png)

### [!UICONTROL Pannello a soffietto] {#layout-for-accordion-design}

Utilizzando questo layout, è possibile inserire **[!UICONTROL Modulo adattivo pannello]** componente in un pannello con navigazione in stile Pannello a soffietto. Utilizzando questo layout, puoi anche creare pannelli ripetibili. I pannelli ripetibili consentono di aggiungere o rimuovere in modo dinamico i pannelli in base alle esigenze. Puoi definire il numero minimo e massimo di ripetizioni di un pannello. Inoltre, il titolo del pannello può essere determinato dinamicamente, in base alle informazioni fornite negli elementi del pannello.

L’espressione di riepilogo può essere utilizzata per mostrare i valori forniti dall’utente finale nel titolo del pannello ridotto a icona.

![Pannelli ripetibili con layout a soffietto in Forms adattivo](assets/accordion-layout.png)

### [!UICONTROL Layout a schede: le schede vengono visualizzate a sinistra]{#tabbed-layout-tabs-appear-on-the-left}

Utilizzando questo layout, è possibile inserire **[!UICONTROL Modulo adattivo pannello]** componente in un pannello con navigazione tramite schede. Le schede vengono posizionate a sinistra del contenuto del pannello.

![Nel layout con schede, le schede vengono visualizzate a sinistra](assets/tabs-on-left.png)

Schede visualizzate a sinistra di un pannello

### [!UICONTROL Layout a schede: le schede vengono visualizzate nella parte superiore] {#tabbed-layout-tabs-appear-on-the-top}

Utilizzando questo layout, è possibile inserire **[!UICONTROL Modulo adattivo pannello]** Componente in un pannello con navigazione tramite schede. Le schede vengono posizionate sopra il contenuto del pannello.

![Layout a schede in Forms adattivo con schede in alto](assets/tabs-on-top.png)

## Layout dispositivi mobili {#mobile-layouts}

I layout mobili consentono una navigazione semplice sui dispositivi mobili con schermi relativamente più piccoli. I layout mobili utilizzano gli stili a schede o della procedura guidata per la navigazione dei moduli. L’applicazione di un layout mobile fornisce un unico layout per l’intero modulo.

Questo layout controlla la navigazione tramite una barra di navigazione e un menu di navigazione. La barra di navigazione mostra **&lt;** e **>** icona per indicare **[!UICONTROL avanti]** e **[!UICONTROL precedente]** passaggi di navigazione nel modulo.

I layout per dispositivi mobili sono disponibili all’indirizzo `/libs/fd/af/layouts/mobile/` posizione. Per impostazione predefinita, in Adaptive Forms sono disponibili i seguenti layout per dispositivi mobili.

![Elenco dei layout mobili in Forms adattivo](assets/mobile-navigation.png)

Seleziona la **[!UICONTROL Aggiungi elementi navigabili del layout reattivo al menu per dispositivi mobili]** per visualizzare le opzioni navigabili disponibili per un pannello nel layout Mobile. Le opzioni navigabili sono visibili solo se si seleziona **[!UICONTROL Reattivo]** layout di un pannello.

Quando si utilizza un layout Mobile, per accedere ai vari pannelli del modulo tocca il menu del modulo ![aem6forms_form_menu](assets/rail-icon.svg) icona.

### [!UICONTROL Layout con titoli dei pannelli nell’intestazione del modulo] {#layout-with-panel-titles-in-the-form-header}

Questo layout, come suggerisce il nome, mostra i titoli dei pannelli insieme al menu di navigazione e alla barra di navigazione. Questo layout fornisce anche le icone Successivo e Precedente per la navigazione.

![Layout mobili con titoli dei pannelli nelle intestazioni dei moduli](assets/mobile-layout1.png)

### [!UICONTROL Layout senza titoli dei pannelli nell’intestazione del modulo]{#layout-without-panel-titles-in-the-form-header}

Come suggerisce il nome, questo layout mostra solo il menu di navigazione e la barra di navigazione senza i titoli dei pannelli. Questo layout fornisce anche le icone Successivo e Precedente per la navigazione.

![Layout mobili senza titoli dei pannelli nelle intestazioni dei moduli](assets/mobile-layout2.png)

## Consulta anche {#see-also}

{{see-also}}


<!-- ## Toolbar layouts {#toolbar-layouts}

A Toolbar Layout controls positioning and display of any action buttons that you add to your Adaptive Forms. The layout can be added at a form level or at a panel level.

![A list of Toolbar Layouts in Adaptive Forms to control layout of buttons](assets/toolbar-layouts.png)

A list of Toolbar Layouts in Adaptive Forms

Toolbar layouts are available at `/libs/fd/af/layouts/toolbar` location. Adaptive Forms provide the following Toolbar Layouts, by default.

### [!UICONTROL Default layout for toolbar] {#default-layout-for-toolbar}

This layout is selected as the default layout when you add any action buttons in an Adaptive Form. Selecting this layout displays the same layout for both, desktop and mobile devices.

Also, you can add multiple toolbars containing action buttons configured with this layout. An action button is associated with a form control. You can configure the toolbars to be before or after a panel.

![Default view for toolbar](assets/toolbar_layout_default.png)

Default view for toolbar

### [!UICONTROL Mobile fixed layout for toolbar] {#mobile-fixed-layout-for-toolbar}

Select this layout to provide alternate layouts for desktop and mobile devices.

For the desktop layout, you can add Action buttons using some specific labels. Only one toolbar can be configured with this layout. If more than one toolbar is configured with this layout, there is an overlap for mobile devices and only one toolbar is visible. For example, you can have a toolbar at the bottom or the top of the form, or, after or before panels in the form.

For the Mobile layout, you can add action buttons using icons.

![Mobile fixed layout for toolbar](assets/toolbar_layout_mobile_fixed.png)

Mobile fixed layout for toolbar-->


