---
title: Come si aggiungono i collegamenti ai moduli nella pagina AEM Sites utilizzando il componente Collega Forms Portal?
description: Scopri come aggiungere collegamenti ai moduli alla pagina AEM Sites.
feature: Adaptive Forms, Core Components
role: User, Developer, Admin
exl-id: a55d0776-8827-46cc-9625-5d6f5f6bda3b
source-git-commit: 5b55a280c5b445d366c7bf189b54b51e961f6ec2
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 1%

---

# Aggiungi collegamenti modulo alla pagina Sites

Nello scenario del sito Web della banca, il componente **Link** Forms Portal migliora la navigazione guidando gli utenti verso moduli specifici in varie sezioni del sito. Fornisce riferimenti diretti a moduli come richieste di prestito, moduli per l’apertura di account o sondaggi di feedback, posizionati in modo strategico in tutto il sito web. Il componente **Collegamento** inserisce collegamenti che indirizzano gli utenti a specifici Forms adattivi nella pagina Sites. Ad esempio, sul sito web della banca, gli utenti anonimi possono accedere a un modulo di richiesta generale, mentre gli utenti connessi possono accedere direttamente a moduli più sicuri, come le richieste di prestito o i moduli di autorizzazione delle transazioni.

![Icona collegamento](/help/forms/assets/link-forms.png)


## Aggiungere il componente Collegamento alla pagina Sites

Per aggiungere il componente del portale **Collegamento** alla pagina Sites, effettuare le seguenti operazioni:

1. Apri la pagina AEM Sites in modalità **Modifica**.
1. Vai a **[!UICONTROL Informazioni pagina]** > **[!UICONTROL Modifica modello]**
   ![Modifica criterio modello](/help/forms/assets/save-form-as-draft-edit-template.png)

1. Fai clic sul **[!UICONTROL Criterio]** e seleziona la casella di controllo **[!UICONTROL Collegamento]** nel **[Nome progetto Archetipo AEM] - Forms and Communications Portal**.

   ![Selezione criteri](/help/forms/assets/add-link.png)

1. Fai clic su **[!UICONTROL Fine]**.
1. Ora riapri la pagina AEM Sites in modalità di authoring.
1. Nell’editor pagina, individua la sezione che consente di aggiungere il componente Forms Portal.

1. Fai clic sull&#39;icona **Aggiungi**. L’icona è un segno più (+) che indica l’opzione per aggiungere nuovi componenti.

   Facendo clic sull&#39;icona **Aggiungi** viene visualizzata una finestra di dialogo **Inserisci nuovo componente** in cui sono visualizzati vari componenti da inserire.

   >[!NOTE]
   >
   > In alternativa, puoi anche trascinare e rilasciare il componente.

1. Sfoglia i componenti disponibili nella finestra di dialogo e seleziona il componente desiderato dall’elenco. Selezionare ad esempio il componente **Link** dall&#39;elenco per aggiungere il componente **Link** di Forms Portal.

   ![Componente collegamento](/help/forms/assets/add-link-in-sites.png)

Ora configura le proprietà del componente **Link**.

## Comprendere le proprietà del componente Collegamento

Puoi personalizzare facilmente le proprietà del componente **Link** tramite la finestra di dialogo per configurazione per un&#39;esperienza utente ottimale. Per configurare, selezionare il componente, quindi selezionare l&#39;icona ![Configura](assets/configure_icon.png). Viene visualizzata la finestra di dialogo **[!UICONTROL Collegamento]**.

### Scheda Visualizzazione

![Scheda Visualizzazione](/help/forms/assets/link-asset-tab.png)

Nella scheda **[!UICONTROL Visualizzazione]**, fornisci la didascalia del collegamento e la descrizione comando per facilitare l&#39;identificazione dei moduli rappresentati dal collegamento.

### Scheda Informazioni risorsa

![Scheda Informazioni di Assets](/help/forms/assets/link-asset-info.png)

Nella scheda **[!UICONTROL Informazioni risorsa]**, specifica il percorso dell&#39;archivio in cui è memorizzata la risorsa.

### Scheda Parametri query

![Scheda Parametri query](/help/forms/assets/link-query-tab.png)

Nella scheda **[!UICONTROL Parametri query]**, specifica i parametri aggiuntivi nel formato della coppia chiave-valore. Quando fai clic sul collegamento, questi parametri aggiuntivi vengono trasmessi insieme al modulo.

## Visualizzare i collegamenti dei moduli nella pagina Sites utilizzando il componente Collegamento

Visualizzare l&#39;anteprima della pagina Sites per visualizzare il collegamento a un modulo adattivo specificato nella scheda delle proprietà **Assets Info** del componente **Link**. Facendo clic sul collegamento, il modulo viene visualizzato sullo schermo per gli utenti, che possono quindi accedervi in base alle autorizzazioni.

![Scheda Parametri query](/help/forms/assets/link-forms.png)

## Articoli correlati

{{forms-portal-see-also}}

## Consulta anche {#see-also}

{{see-also}}
