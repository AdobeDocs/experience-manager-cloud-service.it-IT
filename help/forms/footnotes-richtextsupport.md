---
title: Supporto note a piè di pagina
description: Supporto dell’editor Rich Text per le note a piè di pagina.
exl-id: f04dae84-daab-42f8-876f-02fe426f62be
source-git-commit: 9cff6e94b38016f008fd8177be2e071a530d80b6
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Componente nota a piè di pagina {#footnotecomponent}

**[!UICONTROL Nota a piè di pagina]** è la parte aggiuntiva di informazioni o note visualizzate alla fine della pagina. [!UICONTROL Nota a piè di pagina] comprende le note indicate nel testo con i numeri in apice.

Le note a piè di pagina sono numerate in sequenza nell’ordine in cui appaiono sulla pagina. Ogni nota a piè di pagina ha un numero univoco come apice che corrisponde al numero posizionato nella parte inferiore della pagina. Accanto al numero vengono visualizzate le informazioni supplementari come descrizione della nota a piè di pagina.

![Descrizione nota a piè di pagina](/help/forms/assets/footnote_description.png)


## Utilizzo della nota a piè di pagina {#usesoffootnotes}

* Aiuta a fornire le citazioni.
* Fornisce informazioni aggiuntive che possono interrompere il normale flusso delle informazioni principali.
* Fornisce informazioni parentetiche o autorizzazioni di copyright.

In Adaptive Forms, [!UICONTROL nota a piè pagina] viene utilizzato per visualizzare le informazioni su come completare o utilizzare il modulo. Per informazioni su come creare un Forms adattivo, consulta [Creazione di un modulo adattivo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html).

## Nota a piè di pagina in Forms adattivo {#using-footnote-adaptiveforms}

Per aggiungere una nota a piè di pagina in Adaptive Forms, effettuate le seguenti operazioni:
1. Aprire un modulo adattivo in **Modifica** modalità.
1. Dal browser Componenti, trascina **[!UICONTROL Testo]** nel modulo adattivo.
1. Seleziona la **[!UICONTROL Testo]** componente aggiunto e tocca ![cmppr](assets/configure-icon.svg) per modificarne le proprietà.

   ![Nota a piè di pagina in Forms adattivo](/help/forms/assets/footnote_rte.png)

1. Selezionare il testo per il quale si desidera aggiungere una descrizione della nota a piè di pagina e fare clic su  ![stella](/help/forms/assets/asterisk.svg) per assegnare uno stile al **[!UICONTROL Nota a piè di pagina]** componente.

1. Clic ![spunta](/help/forms/assets/save_icon.svg) per salvare modifiche e stili.

   >[!NOTE]
   >
   >* Le note a piè di pagina vengono numerate automaticamente e visualizzate in modo da essere create nel modulo adattivo.
   >* Se sono presenti note a piè di pagina duplicate, la numerazione è uguale per tutte le note a piè di pagina duplicate.


1. Dal browser Componenti, trascina **[!UICONTROL Segnaposto nota a piè di pagina]** nel modulo adattivo.
   >[!NOTE]
   >
   >* Nell&#39;istanza di pubblicazione, le note a piè di pagina vengono visualizzate nella posizione in cui **[!UICONTROL Segnaposto nota a piè di pagina]** viene inserito nel modulo adattivo.
   >* Quando ci si sposta tra pannelli diversi, nella sezione vengono visualizzate solo le note a piè di pagina visibili **[!UICONTROL Segnaposto nota a piè di pagina]** che sono presenti all’interno del pannello navigato.


1. Salva le proprietà.

In fase di runtime, il numero viene visualizzato sul testo come apice e la descrizione corrispondente viene visualizzata nel **[!UICONTROL Nota a piè di pagina]** componente nella posizione in cui [!UICONTROL Segnaposto nota a piè di pagina] viene inserito nel modulo adattivo. È possibile passare direttamente alla descrizione della nota a piè di pagina facendo clic sul numero corrispondente nella [!UICONTROL Nota a piè di pagina].
