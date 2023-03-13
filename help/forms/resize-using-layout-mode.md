---
title: Come si utilizza la modalità Layout per ridimensionare i componenti per Forms adattivo?
description: Definisci la posizione dei componenti utilizzando la griglia reattiva disponibile in modalità Layout. Scopri come accedere alla modalità Layout, ridimensionare i componenti e i pannelli, definire il layout a più colonne per un pannello, abilitare la nuova griglia reattiva per i layout reattivi precedenti e disabilitare la modalità Layout per i moduli con layout reattivo precedente.
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 53896a8e-4568-460b-bca7-994baea0c8eb
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 0%

---

# Utilizzare la modalità Layout per ridimensionare i componenti {#use-layout-mode-to-resize-components}

L’interfaccia di authoring di moduli adattivi consente di ridimensionare i componenti utilizzando la modalità Layout. Trascinate i punti blu all&#39;interno delle colonne per definire i punti iniziale e finale e posizionare i componenti. I punti blu vengono visualizzati dopo aver toccato il componente nella griglia reattiva. La griglia reattiva è costituita da 12 colonne uguali. L&#39;ombreggiatura dei colori bianco e blu nelle colonne alternative differenzia una colonna dall&#39;altra.

Puoi utilizzare la modalità Layout per ridimensionare i componenti per tutti i tipi di dispositivi, ad esempio desktop, tablet, telefono e altri dispositivi più piccoli. Il tablet deriva automaticamente la configurazione del layout dalla versione desktop e i dispositivi più piccoli derivano la configurazione del layout dal telefono. Tuttavia, puoi sovrascrivere le configurazioni derivate automaticamente per definire una configurazione diversa per ciascun tipo di dispositivo.

## Modalità Layout di accesso {#access-layout-mode}

Seleziona **[!UICONTROL Layout]** dall’elenco a discesa visualizzato nella parte superiore dell’interfaccia di authoring di Moduli adattivi accanto a **[!UICONTROL Anteprima]** opzione. Il modulo viene visualizzato in modalità Layout.

1. Accedi a [!DNL Adobe Experience Manager] istanza di authoring e passare a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Crea un nuovo elemento o apri un elemento esistente [Modulo adattivo](creating-adaptive-form.md).
1. Seleziona **[!UICONTROL Layout]** dall&#39;elenco a discesa visualizzato nella parte superiore accanto al **[!UICONTROL Anteprima]** opzione. Il modulo viene visualizzato in modalità Layout.

   ![Modalità Layout](assets/layout_mode_ic_new.png)

## Ridimensiona i componenti {#resize-components}

1. In modalità Layout, tocca il componente per ridimensionarlo. I punti blu vengono visualizzati all’inizio e alla fine della griglia reattiva.
1. Trascina i punti blu per definire la posizione del componente nella griglia reattiva.

   ![Ridimensionamento utilizzando la modalità Layout](assets/layout_mode_resize_new_updated1.png)

   La barra degli strumenti visualizzata dopo aver toccato i componenti è costituita dalle seguenti opzioni:

   * **[!UICONTROL Elemento padre]**: seleziona l’elemento padre di un componente.
   * **[!UICONTROL Ripristina layout punto di interruzione]**: annulla tutte le modifiche di ridimensionamento e applica il layout predefinito al componente.
   * **[!UICONTROL Mobile in nuova riga]**: sposta il componente alla riga successiva se all’interno della stessa riga sono presenti più componenti.

   È inoltre possibile utilizzare **[!UICONTROL Ripristina layout punto di interruzione]** ( ![Ripristina punto di interruzione](assets/reverttopreviouslypublishedversion.png)) a livello di pannello per annullare tutte le modifiche di ridimensionamento.

   >[!NOTE]
   >
   >Non è possibile ridimensionare i componenti colonna tabella, barra degli strumenti, pulsante barra degli strumenti e area di destinazione utilizzando la modalità Layout. Utilizza la modalità Stile per ridimensionare questi componenti.

### Esempio {#example}

**Obiettivo:** Desideri inserire un componente tabella e un componente immagine e posizionarli paralleli tra loro in un modulo adattivo.

1. Inserire i componenti tabella e immagine utilizzando [!UICONTROL Modifica] nel modulo adattivo. Il componente immagine viene visualizzato dopo il componente tabella.
1. Passa a [!UICONTROL Layout] e tocca il pulsante [!UICONTROL Tabella] componente. I punti blu per ridimensionare il componente vengono visualizzati nelle colonne 1 e 12.
1. Trascina il punto blu nella colonna 12 alla colonna 6 della griglia reattiva.

   ![Definire il punto finale della tabella](assets/layout_mode_end_point_table_new.png)

1. Allo stesso modo, seleziona la [!UICONTROL Immagine] e trascina il punto blu nella colonna 1 alla colonna 7 della griglia reattiva. I componenti tabella e immagine vengono visualizzati in parallelo.

   ![Tabella e immagine in parallelo in modalità Layout](assets/table_image_parallel_new.png)

   Puoi selezionare il componente Immagine e toccare **[!UICONTROL Mobile in nuova riga]** nella barra degli strumenti per spostare il componente Immagine alla riga successiva.

## Ridimensiona pannelli {#resize-panels-layout-mode}

Per ridimensionare l’intero pannello al posto dei singoli componenti, effettua le seguenti operazioni:

1. Tocca uno dei componenti del pannello che desideri ridimensionare, quindi seleziona ![Seleziona elemento padre](assets/select_parent_icon.svg)e seleziona la prima opzione nell’elenco a discesa, se il pannello è l’elemento padre immediato del componente.

   I punti blu vengono visualizzati all’inizio e alla fine della griglia reattiva.

1. Trascina i punti blu per definire la posizione del pannello nella griglia reattiva.
È possibile ripetere i passaggi 1 e 2 e selezionare ![Seleziona elemento padre](assets/float_to_new_line_icon.svg) per spostare il pannello ridimensionato alla riga successiva.

## Definire il layout a più colonne per un pannello

Per definire il numero di colonne di un pannello, esegui i seguenti passaggi:

1. In entrata **[!UICONTROL Modifica]** , tocca il pannello, seleziona ![Configura](assets/configure-icon.svg), e seleziona **[!UICONTROL Reattivo: tutto ciò che si trova sulla pagina senza navigazione]** opzione dalla **[!UICONTROL Layout pannello]** elenco a discesa.

1. Tocca ![Salva](assets/save_icon.svg) per salvare le proprietà.

1. In **[!UICONTROL Layout]** , tocca uno dei componenti nel pannello, seleziona ![Seleziona elemento padre](assets/select_parent_icon.svg)e seleziona il pannello.

1. Tocca ![a più colonne](assets/multi-column.svg) e seleziona il numero di colonne dall’elenco a discesa. Il numero di colonne può essere compreso tra 1 e 12. Il pannello viene diviso in un layout a più colonne.

![più colonne in modalità layout](assets/multi-column-layout.png)

## Abilita la nuova griglia reattiva per i layout reattivi precedenti {#enableresponsivegrid}

Abilita la nuova griglia reattiva per i moduli creati con [!DNL Adobe Experience Manager] Forms 6.4 o versione precedente per ridimensionare i componenti.

>[!NOTE]
>
>Passando alla nuova griglia responsive, vengono ignorate le proprietà di layout già definite per i componenti utilizzati nel modulo.

Per abilitare la nuova griglia reattiva, effettua le seguenti operazioni:

1. Seleziona **[!UICONTROL Layout]** dall&#39;elenco a discesa visualizzato nella parte superiore accanto al **[!UICONTROL Anteprima]** opzione. Viene visualizzata una conferma per abilitare la modalità Layout.
1. Tocca **[!UICONTROL Sì]** per attivare **[!UICONTROL Layout]** per il modulo.

### Incorporare un vecchio frammento in un modulo adattivo con un nuovo layout reattivo {#embed-an-old-fragment-in-an-adaptive-form-with-new-responsive-layout}

Il nuovo layout dinamico per modulo adattivo consente di aggiungere al modulo un frammento di modulo adattivo con il vecchio layout responsivo. Tuttavia, il nuovo layout elimina le proprietà di layout già definite per i componenti utilizzati nel frammento. Puoi passare alla modalità Layout per definire le proprietà di layout dei componenti utilizzati nel frammento.

### Incorporare un frammento con un nuovo layout reattivo in un modulo adattivo precedente {#embed-a-fragment-with-new-responsive-layout-in-an-old-adaptive-form}

Se incorpori un frammento con il nuovo layout reattivo in un modulo adattivo con un vecchio layout reattivo, il sistema richiede di abilitare la modalità Layout per il modulo e di reincorporare il frammento.

Per attivare la modalità Layout, seleziona **[!UICONTROL Layout]** dall&#39;elenco a discesa visualizzato nella parte superiore accanto al **[!UICONTROL Anteprima]** opzione e tocca **[!UICONTROL Sì]** per confermare. Seleziona **[!UICONTROL Modifica]** per reincorporare il frammento.

## Disattiva la modalità Layout per i moduli con layout reattivo precedente {#disable-layout-mode-for-forms-with-old-responsive-layout}

È possibile disattivare la modalità Layout per i moduli con layout reattivo precedente modificando le proprietà del modello utilizzato nel modulo.

Per disattivare la modalità Layout, effettua le seguenti operazioni:

1. Seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Modelli]** e aprire il modello utilizzato nel modulo in **[!UICONTROL Modifica]** modalità.
1. Seleziona il Contenitore modulo nel riquadro a sinistra e tocca **[!UICONTROL Politica.]**

   ![Disattiva modalità Layout](assets/policy_disable_layout_mode.png)

1. Tocca il **[!UICONTROL Impostazioni di layout]** e seleziona **[!UICONTROL Disattiva modalità layout]**.
1. Tocca ![Salva modifiche](assets/save_icon.svg) per salvare le proprietà del modello.
