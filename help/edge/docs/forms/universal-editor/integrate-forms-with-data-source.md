---
title: Come integrare il modello dati modulo (FDM) per un modulo nell’editor universale?
description: Scopri come creare moduli basati su un modello dati modulo (FDM). Genera e modifica dati di esempio per gli oggetti del modello dati nel modello dati modulo (FDM).
feature: Edge Delivery Services, Form Data Model
role: Admin, User
exl-id: 9ce51223-57d0-47d8-8868-84b37d4e8e3e
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 33%

---


# Integrare Forms con Form Data Model (FDM)

Collegare i moduli alle origini dati back-end utilizzando FDM per abilitare l&#39;associazione dati, la convalida e i flussi di lavoro di invio.

## Prerequisiti

Completa questi passaggi prima di integrare FDM con i moduli:

1. **[Configurare Data Source](/help/forms/configure-data-sources.md)**: configurare le connessioni back-end
2. **[Crea modello dati modulo](/help/forms/create-form-data-models.md)**: definizione della struttura dati e dei servizi
3. **[Configura oggetti modello dati](/help/forms/work-with-form-data-model.md)**: mappa relazioni dati

## Considerazioni

Se nell’interfaccia dell’editor universale non viene visualizzata l’icona **Origini dati** o la proprietà **Riferimento bind** nel pannello delle proprietà a destra, abilita l’estensione **Origine dati** in **Extension Manager**.

![Schermata dell’interfaccia dell’editor universale di Extension Manager che mostra le estensioni disponibili, inclusa l’estensione Origini dati, che possono essere abilitate per l’integrazione del modulo](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

Per informazioni su come abilitare e disabilitare le estensioni nell’editor universale, consulta l’articolo [Caratteristiche principali delle funzioni di Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions).

## Scegli il tipo di modulo

Universal Editor supporta due approcci per la creazione di moduli:

| Aspetto | Modulo basato su schema | Modulo non basato su schema |
|--------|-------------------|----------------------|
| **Complessità installazione** | Semplice (binding automatico) | Manuale (associazione campo per campo) |
| **Caso d’uso** | Nuovi moduli con struttura dati definita | Moduli esistenti o requisiti flessibili |
| **Origine dati** | Richiesto durante la creazione | Può essere aggiunto in un secondo momento |
| **Associazione** | Associazione automatica dei campi | Associazione manuale per campo |

![Tipi di modulo nell’editor universale](/help/edge/docs/forms/universal-editor/assets/form-types.png){width="50%" align="center" height="50%"}

## Modulo basato su schema

I moduli basati su schema configurano automaticamente le origini dati e associano i campi modulo ai dati. Questo approccio è ideale per i nuovi moduli con strutture di dati ben definite.

### Creare un modulo basato su schema

1. **Accedi alla console Forms**
   - Accedi all&#39;istanza Autore [!DNL Experience Manager Forms]
   - Passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**

2. **Avvia creazione modulo**
   - Seleziona **[!UICONTROL Crea]** > **[!UICONTROL Forms adattivo]**
   - Scegli un modello Edge Delivery Services
   - Fare clic su **[!UICONTROL Crea]** quando abilitato

   ![Modello di Edge Delivery Services](/help/edge/assets/create-eds-forms.png)

3. **Configura modello dati**
   - Vai alla scheda **Dati**
   - Seleziona **Modello dati modulo (FDM)** per più origini dati o **Schema JSON** per un singolo sistema back-end
   - Scegli il modello di dati FDM creato (ad esempio, Modello dati modulo Pet)

   ![Seleziona modello dati modulo](/help/edge/docs/forms/universal-editor/assets/select-petstore-form-data-model.png)

4. **Completare la configurazione del modulo**
   - Immetti **Nome** e **Titolo**
   - Specifica **URL GitHub** (esempio: `https://github.com/wkndforms/edsforms`)
   - Fai clic su **[!UICONTROL Crea]**.

   ![Crea modulo basato su schema](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form.png)

### Verifica modulo basato su schema

Il modulo si apre in Universal Editor con associazione dati preconfigurata:

![Schermata dell’editor universale che mostra un modulo basato su schema con campi modulo precompilati e il browser dei contenuti con gli elementi dell’origine dati disponibili](/help/edge/docs/forms/universal-editor/assets/schema-based-form-in-ue.png)

![Binding automatico dei dati](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

## Modulo non basato su schema

I moduli non basati su schema richiedono la configurazione manuale dell’origine dati e l’associazione dei campi. Questo approccio offre flessibilità per i moduli esistenti o per i requisiti complessi.

### Crea modulo non basato su schema

1. **Proprietà modulo di accesso**
   - Accedi all&#39;istanza Autore [!DNL Experience Manager Forms]
   - Passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**
   - Seleziona il modulo e fai clic su **[!UICONTROL Proprietà]**

   ![Apri proprietà modulo](/help/edge/docs/forms/universal-editor/assets/non-schema-based-edit-properties.png)

2. **Configura modello modulo**
   - Apri la scheda **Modello modulo**
   - Seleziona **Modello dati modulo (FDM)** dal menu a discesa **Seleziona da**
   - Scegli il tuo FDM dall’elenco

   ![Seleziona scheda Modello del modulo](/help/edge/docs/forms/universal-editor/assets/select-form-model.png)

   ![Seleziona Modello dati modulo](/help/edge/docs/forms/universal-editor/assets/select-fdm.png)

3. **Conferma configurazione**
   - Fare clic su **OK** nella finestra di avviso
   - Fai clic su **[!UICONTROL Salva e chiudi]**

   ![Procedura guidata modello del modulo](/help/edge/docs/forms/universal-editor/assets/form-model-wizard.png)

### Aggiungi elementi dati

1. **Apri modulo per la modifica**
   - Il modulo si apre in Universal Editor

   ![Authoring di moduli non basato su schema](/help/edge/docs/forms/universal-editor/assets/non-schema-form-authoring.png)

2. **Accedere a elementi di Data Source**
   - Vai alla scheda **[!UICONTROL Origine dati]** nel **[!UICONTROL Browser contenuti]**
   - Visualizza gli elementi dati disponibili dal tuo FDM

   ![Origine dati modulo](/help/edge/docs/forms/universal-editor/assets/non-schema-data-source.png)

3. **Aggiungi elementi al modulo**
   - Seleziona gli elementi dati e fai clic su **[!UICONTROL Aggiungi]**
   - Oppure trascina gli elementi per creare il modulo

   ![Aggiungi elementi dei dati](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-element.png)

   ![Schermata che mostra l’editor universale con un modulo non basato su schema generato trascinando elementi di dati dalla scheda Origine dati nella struttura del modulo](/help/edge/docs/forms/universal-editor/assets/non-schema-form.png)

### Aggiungi associazione dati manuale

Per i campi modulo esistenti, aggiungi l&#39;associazione dati tramite la proprietà **Bind Reference**:

1. **Apri proprietà campo**
   - Seleziona il campo modulo per l’associazione
   - Apri il pannello delle proprietà

2. **Configura riferimento associazione**
   - Vai alla proprietà **Riferimento binding**
   - Fai clic sull&#39;icona **Sfoglia**

   ![Aggiungere manualmente il binding dei dati per un campo modulo](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-binding.png)

3. **Seleziona elemento dati**
   - Scegliere dalla struttura dell&#39;origine dati nella procedura guidata **Seleziona un riferimento associazione**
   - Seleziona l&#39;elemento dati desiderato e fai clic su **Seleziona**

   ![seleziona riferimento binding dei dati](/help/edge/docs/forms/universal-editor/assets/select-bind-reference.png)

   ![seleziona elemento di dati](/help/edge/docs/forms/universal-editor/assets/select-data-element.png)

4. **Verifica binding**
   - Il campo modulo ora si lega all’elemento dati
   - L&#39;associazione viene visualizzata nella proprietà **Riferimento associazione**

   ![Binding automatico dei dati](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

## Verifica integrazione

Dopo aver completato l’integrazione:

1. **Associazione dati di prova**: verificare che i campi modulo visualizzino dati corretti
2. **Convalida invii**: assicurati che i dati vengano salvati nelle origini configurate
3. **Verifica gestione errori**: verifica con scenari di dati non validi

## Passaggi successivi

Configura [azioni di invio](/help/edge/docs/forms/universal-editor/submit-action.md) per completare il flusso di lavoro del modulo.
