---
title: Come si aggiunge una nota a piè di pagina a un modulo adattivo?
description: Utilizza l’editor Rich Text per le note a piè di pagina in un modulo adattivo.
feature: Adaptive Forms, Foundation Components
exl-id: f04dae84-daab-42f8-876f-02fe426f62be
role: User, Developer
source-git-commit: a7265b4f8df34efc09076c03d1433f9aae542e76
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Componente nota a piè di pagina {#footnotecomponent}

Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/creating-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base.

**[!UICONTROL Nota a piè di pagina]** è la parte aggiuntiva di informazioni o note visualizzate alla fine della pagina. [!UICONTROL La nota a piè di pagina] comprende le note indicate nel testo con i numeri in apice.

Le note a piè di pagina sono numerate in sequenza in base all&#39;ordine di visualizzazione nella pagina. Ogni nota a piè di pagina ha un numero univoco come apice che corrisponde al numero posizionato nella parte inferiore della pagina. Accanto al numero vengono visualizzate le informazioni supplementari come descrizione della nota a piè di pagina.

![Descrizione nota](/help/forms/assets/footnote_description.png)


## Utilizzo della nota a piè di pagina {#usesoffootnotes}

* Aiuta a fornire le citazioni.
* Fornisce informazioni aggiuntive che possono interrompere il normale flusso delle informazioni principali.
* Fornisce informazioni parentetiche o autorizzazioni di copyright.

In Forms adattivo, viene utilizzata la [!UICONTROL nota a piè di pagina] per visualizzare le informazioni su come completare o utilizzare il modulo. Per informazioni sulla creazione di un Forms adattivo, vedere [Creazione di un modulo adattivo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html?lang=it).

## Nota a piè di pagina in Forms adattivo {#using-footnote-adaptiveforms}

Per aggiungere una nota a piè di pagina in Adaptive Forms, effettuate le seguenti operazioni:

1. Apri un modulo adattivo in modalità **Modifica**.
1. Dal browser componenti, trascina il componente **[!UICONTROL Testo]** nel modulo adattivo.
1. Seleziona il componente **[!UICONTROL Testo]** aggiunto e seleziona ![cmppr](assets/configure-icon.svg) per modificarne le proprietà.

   ![Nota a piè di pagina in Forms adattivo](/help/forms/assets/footnote_rte.png)

1. Seleziona il testo per il quale desideri aggiungere una descrizione della nota a piè di pagina e fai clic sul pulsante ![stella](/help/forms/assets/asterisk.svg) per assegnare uno stile al componente **[!UICONTROL Nota a piè di pagina]**.

1. Fai clic su ![check](/help/forms/assets/save_icon.svg) per salvare le modifiche e gli stili.

   >[!NOTE]
   >
   >* Le note a piè di pagina vengono numerate automaticamente e visualizzate in modo da essere create nel modulo adattivo.
   >* Se sono presenti note a piè di pagina duplicate, la numerazione è uguale per tutte le note a piè di pagina duplicate.

1. Dal browser componenti, trascina il componente **[!UICONTROL Segnaposto nota a piè di pagina]** nel modulo adattivo.

1. Salva le proprietà.

In fase di esecuzione, il numero viene visualizzato nel testo come apice e la descrizione corrispondente viene visualizzata nel componente **[!UICONTROL Nota a piè di pagina]** nella posizione in cui [!UICONTROL Segnaposto nota a piè di pagina] viene inserito nel modulo adattivo. Puoi passare direttamente alla descrizione della nota a piè di pagina facendo clic sul numero corrispondente nella [!UICONTROL Nota a piè di pagina].

## Comportamento del segnaposto della nota a piè di pagina in Forms adattivo

* Nell&#39;istanza di pubblicazione, le note a piè di pagina vengono visualizzate nella posizione in cui il componente **[!UICONTROL Segnaposto nota a piè di pagina]** viene inserito nel modulo adattivo.
* Le note a piè di pagina supportano le interruzioni di riga, consentendo agli autori dei moduli di formattare il contenuto su più righe all&#39;interno del componente **[!UICONTROL Segnaposto nota a piè di pagina]**.
* Le note a piè di pagina rimangono sempre visibili nel **[!UICONTROL Segnaposto nota a piè di pagina]**, indipendentemente dalla visibilità dei pannelli associati.


## Consulta anche {#see-also}

{{see-also}}