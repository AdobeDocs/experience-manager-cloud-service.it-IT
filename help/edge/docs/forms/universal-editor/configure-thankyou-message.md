---
title: Come configurare una pagina di reindirizzamento o un messaggio di ringraziamento?
description: Scopri come gli utenti possono visualizzare un messaggio di ringraziamento o essere reindirizzati a una pagina web che gli autori dei moduli possono configurare durante la creazione del modulo.
feature: Adaptive Forms, Edge Delivery Services
role: User
level: Intermediate
source-git-commit: 87650caea6eb907093f0f327f1dbc19641098e4a
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Configurare il reindirizzamento o il messaggio di ringraziamento

Nei moduli creati mediante l’Editor universale, gli autori dei moduli possono configurare ciò che accade dopo l’invio di un modulo da parte dell’utente. Puoi visualizzare un messaggio di ringraziamento o reindirizzare l’utente a una pagina web specifica utilizzando la scheda Invio nell’estensione Modifica proprietà modulo.

Puoi configurare il messaggio di ringraziamento o gli URL di reindirizzamento per i moduli creati nell&#39;editor universale utilizzando la scheda **Invio** dell&#39;estensione **Proprietà modulo di AEM**.

## Prerequisiti

È possibile configurare l&#39;azione di invio per i moduli creati nell&#39;Editor universale utilizzando la scheda **Invio** dell&#39;estensione **Modifica proprietà modulo**.

![Icona proprietà modulo](/help/forms/assets/ue-form-properties-icon.png)

![Proprietà modulo editor universale](/help/forms/assets/ue-form-properties.png)

>[!NOTE]
>
> * Se l&#39;icona **Proprietà modulo** non è visibile nell&#39;interfaccia di Universal Editor, abilitare l&#39;estensione **Modifica proprietà modulo** in Extension Manager.
> * Per informazioni su come abilitare o disabilitare le estensioni nell&#39;editor universale, consulta l&#39;articolo [Caratteristiche principali di Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions).

## Come configurare il reindirizzamento o il messaggio di ringraziamento?

Quando si invia un modulo, è possibile reindirizzare l&#39;utente a un&#39;altra pagina Web o visualizzare un messaggio.

Per configurare la pagina di reindirizzamento o il messaggio di ringraziamento:

1. Apri il modulo adattivo per la modifica.
2. Aprire la Struttura contenuto e selezionare il **[!UICONTROL Contenitore guida]**.
3. Fai clic sull&#39;icona Proprietà contenitore modulo adattivo ![Proprietà contenitore modulo adattivo](/help/forms/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo per configurare i modelli dati.
4. Apri la scheda **[!UICONTROL Invio]**. Vengono visualizzate le opzioni per configurare una pagina di reindirizzamento o un messaggio:

   ![Finestra di dialogo per l&#39;invio del Contenitore guida per configurare una pagina di reindirizzamento o un messaggio](/help/forms/assets/adaptive-forms-core-components-redirect-page-or-thank-you-message.png)

**Configura URL di reindirizzamento**

* Per configurare un URL di reindirizzamento, per l&#39;opzione Invia selezionare l&#39;opzione **[!UICONTROL Reindirizza all&#39;URL]** e fornire un indirizzo assoluto o un URL di reindirizzamento o un percorso relativo di una pagina AEM Sites.

![reindirizzamento](/help/edge/docs/forms/universal-editor/assets/redirect-ue.png)

**Configura messaggio di ringraziamento**

* Per configurare un messaggio personalizzato o di ringraziamento, selezionare l&#39;opzione **[!UICONTROL Mostra messaggio]** e immettere un messaggio nella casella Contenuto messaggio. Si tratta di una casella di testo RTF, è possibile utilizzare l&#39;opzione a schermo intero per visualizzare tutti gli elementi RTF disponibili.

![grazie](/help/edge/docs/forms/universal-editor/assets/thankyou-ue.png)

Gli autori dei moduli possono configurare una pagina per ogni modulo, alla quale gli utenti vengono reindirizzati dopo l&#39;invio di un modulo.
