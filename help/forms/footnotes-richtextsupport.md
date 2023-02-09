---
title: Supporto per note a piè di pagina
description: Supporto dell’editor Rich Text per le note a piè di pagina.
source-git-commit: 6f6cf5657bf745a2e392a8bfd02572aa864cc69c
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Componente nota a piè di pagina {#footnotecomponent}

**[!UICONTROL Nota]** è la parte aggiuntiva di informazioni o note che vengono visualizzate alla fine della pagina. [!UICONTROL Nota] comprende le note indicate nel testo con numeri come apice.

Le note a piè di pagina vengono numerate in sequenza nell’ordine in cui compaiono sulla pagina. Ogni nota a piè di pagina ha un numero univoco come apice che corrisponde al numero posizionato nella parte inferiore della pagina. Accanto al numero vengono visualizzate le informazioni supplementari sotto forma di nota a piè di pagina.

![Descrizione nota a piè di pagina](/help/forms/assets/footnote_description.png)


## Utilizzo della nota a piè di pagina {#usesoffootnotes}

* Aiuta a fornire citazioni.
* Fornisce informazioni aggiuntive che possono interrompere il normale flusso delle informazioni principali.
* Fornisce informazioni parentetiche o autorizzazioni di copyright.

In Forms adattivo, [!UICONTROL nota] viene utilizzato per visualizzare le informazioni su come compilare o utilizzare il modulo. Per informazioni su come creare un Forms adattivo, consulta [Creazione di un modulo adattivo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html).

## Nota a piè di pagina in Forms adattivo {#using-footnote-adaptiveforms}

Per aggiungere una nota a piè di pagina in Forms adattivo, esegui i seguenti passaggi:
1. Apri un modulo adattivo in **Modifica** modalità.
1. Dal browser Componenti, trascina la **[!UICONTROL Testo]** sul modulo adattivo.
1. Seleziona la **[!UICONTROL Testo]** componente aggiunto e tocca ![cmppr](assets/configure-icon.svg) per modificarne le proprietà.

   ![Nota a piè di pagina in Forms adattivo](/help/forms/assets/footnote_rte.png)

1. Selezionare il testo per il quale si desidera aggiungere una descrizione a piè di pagina e fare clic su  ![stella](/help/forms/assets/asterisk.svg) per assegnare uno stile al pulsante **[!UICONTROL Nota]** componente.

1. Fai clic su ![check](/help/forms/assets/save_icon.svg) per salvare le modifiche e gli stili.

   >[!NOTE]
   >
   >* Le note a piè di pagina vengono numerate automaticamente e visualizzate nel modo in cui vengono create nel Modulo adattivo.
   >* Se sono presenti note a piè di pagina duplicate, la numerazione è la stessa per tutte le note a piè di pagina duplicate.


1. Dal browser Componenti, trascina la **[!UICONTROL Segnaposto nota a piè di pagina]** sul modulo adattivo.
   >[!NOTE]
   >
   >* Nell’istanza di pubblicazione, le note a piè di pagina vengono visualizzate nella posizione in cui **[!UICONTROL Segnaposto nota a piè di pagina]** Il componente viene inserito nel Modulo adattivo.
   >* Quando vi spostate tra i diversi pannelli, vengono visualizzate solo le note a piè di pagina visibili **[!UICONTROL Segnaposto nota a piè di pagina]** presenti nel pannello navigato.


1. Salva le proprietà.

In fase di esecuzione, il numero viene visualizzato sul testo come apice e la relativa descrizione viene visualizzata nel **[!UICONTROL Nota]** nella posizione in cui [!UICONTROL Segnaposto nota a piè di pagina] viene posizionato sul modulo adattivo. Per passare direttamente alla descrizione della nota a piè di pagina, fai clic sul numero corrispondente nella [!UICONTROL Nota].