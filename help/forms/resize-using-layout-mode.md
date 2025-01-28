---
title: Come si utilizza la modalità layout per ridimensionare i componenti per i moduli adattivi?
description: Definisci la posizione dei componenti AEM Forms, scopri come accedere alla modalità di layout, ridimensionare i componenti, ridimensionare i pannelli e definire il layout a più colonne per un pannello.
role: User, Developer
level: Intermediate
feature: Adaptive Forms, Foundation Components
exl-id: 53896a8e-4568-460b-bca7-994baea0c8eb
source-git-commit: b5340c23f0a2496f0528530bdd072871f0d70d62
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 1%

---

# Utilizza la modalità Layout per ridimensionare i componenti per Adaptive Forms {#use-layout-mode-to-resize-components}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/creating-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base.

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/resize-using-layout-mode.html) |
| AEM as a Cloud Service | Questo articolo |

L’interfaccia di authoring di moduli adattivi consente di ridimensionare i componenti utilizzando la modalità Layout. Trascinate i punti blu all&#39;interno delle colonne per definire i punti iniziale e finale e posizionare i componenti. I punti blu vengono visualizzati dopo aver toccato il componente nella griglia reattiva. La griglia reattiva è costituita da 12 colonne uguali. L&#39;ombreggiatura dei colori bianco e blu nelle colonne alternative differenzia una colonna dall&#39;altra.

Puoi utilizzare la modalità Layout per ridimensionare i componenti per tutti i tipi di dispositivi, ad esempio desktop, tablet, telefono e altri dispositivi più piccoli. Il tablet deriva automaticamente la configurazione del layout dalla versione desktop e i dispositivi più piccoli derivano la configurazione del layout dal telefono. Tuttavia, puoi sovrascrivere le configurazioni derivate automaticamente per definire una configurazione diversa per ciascun tipo di dispositivo.

## Modalità Layout di accesso {#access-layout-mode}

Seleziona **[!UICONTROL Layout]** dall&#39;elenco a discesa visualizzato nella parte superiore dell&#39;interfaccia di creazione dei moduli adattivi accanto all&#39;opzione **[!UICONTROL Anteprima]**. Il modulo viene visualizzato in modalità Layout.

1. Accedi all&#39;istanza di authoring [!DNL Adobe Experience Manager] e passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Crea un nuovo modulo adattivo ](creating-adaptive-form.md) o apri un modulo adattivo [esistente.
1. Seleziona **[!UICONTROL Layout]** dall&#39;elenco a discesa visualizzato nella parte superiore accanto all&#39;opzione **[!UICONTROL Anteprima]**. Il modulo viene visualizzato in modalità Layout.

   ![Modalità layout](assets/layout_mode_ic_new.png)

## Ridimensionare i componenti {#resize-components}

1. In modalità Layout, seleziona il componente da ridimensionare. I punti blu vengono visualizzati all’inizio e alla fine della griglia reattiva.
1. Trascina i punti blu per definire la posizione del componente nella griglia reattiva.

   ![Ridimensionamento in modalità Layout](assets/layout_mode_resize_new_updated1.png)

   La barra degli strumenti visualizzata dopo aver toccato i componenti è costituita dalle seguenti opzioni:

   * **[!UICONTROL Elemento padre]**: selezionare il padre di un componente.
   * **[!UICONTROL Ripristina layout punto di interruzione]**: annulla tutte le modifiche di ridimensionamento e applica il layout predefinito al componente.
   * **[!UICONTROL Mobile in nuova riga]**: se nella stessa riga sono presenti più componenti, spostare il componente alla riga successiva.

   È inoltre possibile utilizzare l&#39;opzione **[!UICONTROL Ripristina layout punto di interruzione]** ( ![Ripristina punto di interruzione](assets/reverttopreviouslypublishedversion.png)) a livello di pannello per annullare tutte le modifiche di ridimensionamento.

   >[!NOTE]
   >
   >Non è possibile ridimensionare i componenti colonna tabella, barra degli strumenti, pulsante barra degli strumenti e area di destinazione utilizzando la modalità Layout. Utilizza la modalità Stile per ridimensionare questi componenti.

### Esempio {#example}

**Obiettivo:** inserire un componente tabella e un componente immagine e posizionarli in modo parallelo in un modulo adattivo.

1. Inserisci i componenti tabella e immagine utilizzando la modalità [!UICONTROL Modifica] nel modulo adattivo. Il componente immagine viene visualizzato dopo il componente tabella.
1. Passa alla modalità [!UICONTROL Layout] e seleziona il componente [!UICONTROL Tabella]. I punti blu per ridimensionare il componente vengono visualizzati nelle colonne 1 e 12.
1. Trascina il punto blu nella colonna 12 alla colonna 6 della griglia reattiva.

   ![Definire il punto finale della tabella](assets/layout_mode_end_point_table_new.png)

1. Allo stesso modo, seleziona il componente [!UICONTROL Immagine] e trascina il punto blu nella colonna 1 alla colonna 7 della griglia reattiva. I componenti tabella e immagine vengono visualizzati in parallelo.

   ![Tabella e immagine in parallelo in modalità Layout](assets/table_image_parallel_new.png)

   Puoi selezionare il componente Immagine e l&#39;opzione **[!UICONTROL Mobile in nuova riga]** disponibile nella barra degli strumenti per spostare il componente Immagine alla riga successiva.

## Ridimensiona pannelli {#resize-panels-layout-mode}

Per ridimensionare l’intero pannello al posto dei singoli componenti, effettua le seguenti operazioni:

1. Selezionare uno dei componenti del pannello che si desidera ridimensionare, selezionare ![Seleziona elemento padre](assets/select_parent_icon.svg) e selezionare la prima opzione nell&#39;elenco a discesa, se il pannello è l&#39;elemento padre immediato del componente.

   I punti blu vengono visualizzati all’inizio e alla fine della griglia reattiva.

1. Trascina i punti blu per definire la posizione del pannello nella griglia reattiva.
È possibile ripetere i passaggi 1 e 2 e selezionare ![Seleziona elemento padre](assets/float_to_new_line_icon.svg) per spostare il pannello ridimensionato alla riga successiva.

## Definire il layout a più colonne per un pannello

Per definire il numero di colonne di un pannello, esegui i seguenti passaggi:

1. In modalità **[!UICONTROL Modifica]**, seleziona il pannello, seleziona ![Configura](assets/configure-icon.svg), quindi seleziona **[!UICONTROL Reattivo - tutto nella pagina senza navigazione]** dall&#39;elenco a discesa **[!UICONTROL Layout pannello]**.

1. Seleziona ![Salva](assets/save_icon.svg) per salvare le proprietà.

1. Nella modalità **[!UICONTROL Layout]**, seleziona uno dei componenti del pannello, seleziona ![Seleziona elemento padre](assets/select_parent_icon.svg) e seleziona il pannello.

1. Selezionare ![più colonne](assets/multi-column.svg) e selezionare il numero di colonne dall&#39;elenco a discesa. Il numero di colonne può essere compreso tra 1 e 12. Il pannello viene diviso in un layout a più colonne.

![più colonne in modalità layout](assets/multi-column-layout.png)

## Abilita la nuova griglia reattiva per i layout reattivi precedenti {#enableresponsivegrid}

Abilitare la nuova griglia reattiva per i moduli creati con [!DNL Adobe Experience Manager] Forms 6.4 o versione precedente per ridimensionare i componenti.

>[!NOTE]
>
>Passando alla nuova griglia responsive, vengono ignorate le proprietà di layout già definite per i componenti utilizzati nel modulo.

Per abilitare la nuova griglia reattiva, effettua le seguenti operazioni:

1. Seleziona **[!UICONTROL Layout]** dall&#39;elenco a discesa visualizzato nella parte superiore accanto all&#39;opzione **[!UICONTROL Anteprima]**. Viene visualizzata una conferma per abilitare la modalità Layout.
1. Seleziona **[!UICONTROL Sì]** per abilitare la modalità **[!UICONTROL Layout]** per il modulo.

### Incorporare un vecchio frammento in un modulo adattivo con un nuovo layout reattivo {#embed-an-old-fragment-in-an-adaptive-form-with-new-responsive-layout}

Il nuovo layout reattivo per modulo adattivo consente di aggiungere al modulo un frammento di modulo adattivo con il vecchio layout reattivo. Tuttavia, il nuovo layout elimina le proprietà di layout già definite per i componenti utilizzati nel frammento. Puoi passare alla modalità Layout per definire le proprietà di layout dei componenti utilizzati nel frammento.

### Incorporare un frammento con un nuovo layout reattivo in un modulo adattivo precedente {#embed-a-fragment-with-new-responsive-layout-in-an-old-adaptive-form}

Se incorpori un frammento con il nuovo layout reattivo in un modulo adattivo con un vecchio layout reattivo, il sistema richiede di abilitare la modalità Layout per il modulo e di reincorporare il frammento.

Per attivare la modalità Layout, seleziona **[!UICONTROL Layout]** dall&#39;elenco a discesa visualizzato nella parte superiore accanto all&#39;opzione **[!UICONTROL Anteprima]** e seleziona **[!UICONTROL Sì]** per confermare. Seleziona la modalità **[!UICONTROL Modifica]** per reincorporare il frammento.

## Disattiva la modalità Layout per i moduli con layout reattivo precedente {#disable-layout-mode-for-forms-with-old-responsive-layout}

È possibile disattivare la modalità Layout per i moduli con layout reattivo precedente modificando le proprietà del modello utilizzato nel modulo.

Per disattivare la modalità Layout, effettua le seguenti operazioni:

1. Seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Modelli]** e apri il modello utilizzato nel modulo in modalità **[!UICONTROL Modifica]**.
1. Selezionare il Contenitore modulo nel riquadro di sinistra e selezionare **[!UICONTROL Criterio.]**

   ![Disattiva modalità layout](assets/policy_disable_layout_mode.png)

1. Selezionare la scheda **[!UICONTROL Impostazioni layout]** e selezionare **[!UICONTROL Disattiva modalità layout]**.
1. Seleziona ![Salva modifiche](assets/save_icon.svg) per salvare le proprietà del modello.

## Consulta anche {#see-also}

{{see-also}}