---
title: Come integrare un modello dati di modulo (FDM) in un modulo nell’editor universale?
description: Scopri come creare moduli per Edge Delivery Services basati su un modello dati modulo (FDM). Genera e modifica dati di esempio per gli oggetti del modello dati nel modello dati modulo (FDM).
feature: Edge Delivery Services, Form Data Model
role: Admin, User
exl-id: 9ce51223-57d0-47d8-8868-84b37d4e8e3e
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: ht
source-wordcount: '716'
ht-degree: 100%

---


# Integrare i moduli con un modello dati modulo (FDM)

Collega i moduli alle origini dati di back-end utilizzando FDM per abilitare l’associazione dati, la convalida e i flussi di lavoro di invio.

## Prerequisiti

Completa questi passaggi prima di integrare FDM con i moduli:

1. **[Configura l’origine dati](/help/forms/configure-data-sources.md)**: configura le connessioni back-end
2. **[Crea un modello dati modulo](/help/forms/create-form-data-models.md)**: definisci la struttura e i servizi dati
3. **[Configura oggetti modello dati](/help/forms/work-with-form-data-model.md)**: mappa le relazioni dei dati

## Considerazioni

Se nell’interfaccia dell’editor universale non viene visualizzata l’icona **Origini dati** o la proprietà **Riferimento bind** nel pannello delle proprietà a destra, abilita l’estensione **Origine dati** in **Extension Manager**.

![Schermata dell’interfaccia dell’editor universale di Extension Manager che mostra le estensioni disponibili, inclusa l’estensione Origini dati, che possono essere abilitate per l’integrazione del modulo](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

Per informazioni su come abilitare e disabilitare le estensioni nell’editor universale, consulta l’articolo [Caratteristiche principali delle funzioni di Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions).

## Scegliere il tipo di modulo

L’editor universale supporta due approcci per la creazione di moduli:

| Aspetto | Modulo basato su schema | Modulo non basato su schema |
|--------|-------------------|----------------------|
| **Complessità di configurazione** | Semplice (associazione automatica) | Manuale (associazione campo per campo) |
| **Caso d’uso** | Nuovi moduli con struttura dati definita | Moduli esistenti o requisiti flessibili |
| **Origine dati** | Obbligatoria durante la creazione | Può essere aggiunta in un secondo momento |
| **Associazione** | Associazione dei campi automatica | Associazione manuale per campo |

![Tipi di modulo nell’editor universale](/help/edge/docs/forms/universal-editor/assets/form-types.png){width="50%" align="center" height="50%"}

## Modulo basato su schema

I moduli basati su schema configurano automaticamente le origini dati e associano i campi modulo ai dati. Questo approccio è ideale per i nuovi moduli con strutture di dati ben definite.

### Creare un modulo basato su schema

1. **Accedere alla console Moduli**
   - Accedi all’istanza di authoring [!DNL Experience Manager Forms].
   - Passa a: **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e Documenti]**

2. **Iniziare la creazione del modulo**
   - Seleziona **[!UICONTROL Crea]** > **[!UICONTROL Moduli adattivi]**
   - Scegli un modello Edge Delivery Services
   - Fai clic su **[!UICONTROL Crea]** quando è abilitato

   ![Modello di Edge Delivery Services](/help/edge/assets/create-eds-forms.png)

3. **Configurare un modello dati**
   - Vai alla scheda **Dati**
   - Seleziona **Modello dati modulo (FDM)** per più origini dati o **Schema JSON** per un singolo sistema di back-end
   - Scegli il FDM creato (ad esempio, Modello dati modulo Animale domestico)

   ![Selezionare il modello dati modulo](/help/edge/docs/forms/universal-editor/assets/select-petstore-form-data-model.png)

4. **Completare la configurazione del modulo**
   - Immetti **Nome** e **Titolo**
   - Specifica **URL GitHub** (esempio: `https://github.com/wkndforms/edsforms`)
   - Fai clic su **[!UICONTROL Crea]**.

   ![Creare un modulo basato su schema](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form.png)

### Verificare un modulo basato su schema

Il modulo si apre nell’editor universale con associazione dati preconfigurata:

![Schermata dell’editor universale che mostra un modulo basato su schema con campi modulo precompilati e il browser dei contenuti con gli elementi dell’origine dati disponibili](/help/edge/docs/forms/universal-editor/assets/schema-based-form-in-ue.png)

![Binding automatico dei dati](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

## Modulo non basato su schema

I moduli non basati su schema richiedono la configurazione manuale dell’origine dati e dell’associazione dei campi. Questo approccio offre flessibilità per i moduli esistenti o per i requisiti complessi.

### Creare un modulo non basato su schema

1. **Accedere alle proprietà di un modulo**
   - Accedi all’istanza di authoring di [!DNL Experience Manager Forms].
   - Passa a: **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**
   - Seleziona il modulo e fai clic su **[!UICONTROL Proprietà]**

   ![Aprire le proprietà del modulo](/help/edge/docs/forms/universal-editor/assets/non-schema-based-edit-properties.png)

2. **Configurare un modello modulo**
   - Apri la scheda **Modello modulo**
   - Seleziona **Modello dati modulo (FDM)** dal menu a discesa **Seleziona da**
   - Scegli il tuo FDM dall’elenco

   ![Selezionare la scheda Modello del modulo](/help/edge/docs/forms/universal-editor/assets/select-form-model.png)

   ![Selezionare Modello dati modulo](/help/edge/docs/forms/universal-editor/assets/select-fdm.png)

3. **Configurazione di conferma**
   - Nella finestra di avviso fai clic su **OK**.
   - Fai clic su **[!UICONTROL Salva e chiudi]**

   ![Procedura guidata per modello del modulo](/help/edge/docs/forms/universal-editor/assets/form-model-wizard.png)

### Aggiungi elementi dei dati

1. **Aprire il modulo per la modifica**
   - Il modulo si apre nell’editor universale

   ![Authoring di moduli non basato su schema](/help/edge/docs/forms/universal-editor/assets/non-schema-form-authoring.png)

2. **Accedere a elementi dell’origine dati**
   - Vai alla scheda **[!UICONTROL Origine dati]** nel **[!UICONTROL Browser contenuti]**
   - Visualizza gli elementi dei dati disponibili dal tuo FDM

   ![Origine dei dati del modulo](/help/edge/docs/forms/universal-editor/assets/non-schema-data-source.png)

3. **Aggiungere elementi al modulo**
   - Seleziona gli elementi dei dati e fai clic su **[!UICONTROL Aggiungi]**
   - Oppure trascina gli elementi per creare il modulo

   ![Aggiungere elementi dei dati](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-element.png)

   ![Schermata che mostra l’editor universale con un modulo non basato su schema generato trascinando elementi di dati dalla scheda Origine dati nella struttura del modulo](/help/edge/docs/forms/universal-editor/assets/non-schema-form.png)

### Aggiungere l’associazione manuale dei dati

Per i campi modulo esistenti, aggiungi l’associazione dei dati tramite la proprietà **Riferimento associazione**:

1. **Aprire le proprietà del campo**
   - Seleziona il campo modulo per l’associazione
   - Apri il suo pannello delle proprietà

2. **Configurare un riferimento di associazione**
   - Vai alla proprietà **Riferimento associazione**
   - Fai clic sull’icona **Sfoglia**

   ![Aggiungere manualmente l&#39;associazione dei dati per un campo modulo](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-binding.png)

3. **Seleziona elemento di dati**
   - Scegli dalla struttura dell’origine dati nella procedura guidata **Seleziona un riferimento di associazione**.
   - Seleziona l’elemento di dati desiderato e fai clic su **Seleziona**

   ![seleziona riferimento binding dei dati](/help/edge/docs/forms/universal-editor/assets/select-bind-reference.png)

   ![seleziona elemento di dati](/help/edge/docs/forms/universal-editor/assets/select-data-element.png)

4. **Verificare il binding**
   - Il campo modulo ora si associa all’elemento di dati
   - L’associazione viene visualizzata nella proprietà **Riferimento di associazione**

   ![Binding automatico dei dati](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

## Verifica integrazione

Dopo aver completato l’integrazione:

1. **Testa l’associazione di dati**: verifica che i campi modulo mostrino i dati corretti
2. **Convalida gli invii**: assicurati che i dati vengano salvati nelle origini configurate
3. **Verifica la gestione degli errori**: testa scenari di dati non validi

## Passaggi successivi

Configura [azioni di invio](/help/edge/docs/forms/universal-editor/submit-action.md) per completare il flusso di lavoro del modulo.
