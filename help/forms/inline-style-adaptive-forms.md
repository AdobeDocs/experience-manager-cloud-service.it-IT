---
title: Come si applicano gli stili in linea ai componenti dei moduli adattivi?
description: Mentre puoi applicare stili personalizzati su un modulo adattivo, puoi anche applicare proprietà CSS in linea sui singoli componenti di un modulo adattivo. Scopri come applicare gli stili in linea ai componenti Modulo adattivo. Approfondisci con un esempio lo stile in linea applicato a un componente campo di testo.
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 25adabfb-ff19-4cb2-aef5-0a8086d2e552
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 2%

---

# Stile in linea dei componenti per moduli adattivi {#inline-styling-of-adaptive-form-components}

È possibile definire l’aspetto e lo stile generali di un modulo adattivo specificando gli stili utilizzando [editor a tema](themes.md). Inoltre, puoi applicare stili CSS in linea ai singoli componenti Modulo adattivo e visualizzare in anteprima le modifiche al volo. Gli stili in linea sostituiscono lo stile fornito nel tema .

## Applicare proprietà CSS in linea {#apply-inline-css-properties}

Per aggiungere stili in linea a un componente:

1. Aprire il modulo nell’editor moduli e modificare la modalità in modalità stile. Per passare alla modalità stile nella barra degli strumenti della pagina, tocca ![elenco a discesa canvas](assets/Smock_ChevronDown.svg) > **[!UICONTROL Stile]**.
1. Seleziona un componente nella pagina e tocca il pulsante di modifica ![pulsante di modifica](assets/edit.svg). Proprietà di stile aperte nella barra laterale.

   È inoltre possibile selezionare i componenti dalla struttura gerarchica del modulo nella barra laterale. La struttura gerarchica del modulo è disponibile come Oggetti modulo nella barra laterale.

   In [!UICONTROL Stile] In questa modalità è possibile visualizzare i componenti elencati in Oggetti modulo. Tuttavia, l’elenco Oggetti modulo nella barra laterale elenca i componenti, ad esempio campi e pannelli. I campi e i pannelli sono componenti generici che possono contenere componenti quali caselle di testo e pulsanti di scelta.

   Quando selezioni un componente dalla barra laterale, vengono visualizzati tutti i sottocomponenti elencati e le proprietà del componente selezionato. Puoi selezionare un sottocomponente specifico e formattarlo.

1. Fai clic su una scheda nella barra laterale per specificare le proprietà CSS. Puoi specificare proprietà quali:

   * [!UICONTROL Dimension e posizione] (Impostazione del display, imbottitura, altezza, larghezza, margine, posizione, indice z, float, trasparente, overflow)
   * [!UICONTROL Testo] (famiglia di font, peso, colore, dimensione, altezza riga e allineamento)
   * [!UICONTROL Sfondo] (Immagine e sfumatura, colore di sfondo)
   * [!UICONTROL Bordo] (Larghezza, stile, colore, raggio)
   * [!UICONTROL Effetti] (Ombra, Opacità)
   * [!UICONTROL Avanzate] (Consente di scrivere CSS personalizzati per il componente)

1. Allo stesso modo, puoi applicare gli stili ad altre parti di un componente, ad esempio [!UICONTROL Widget], [!UICONTROL Didascalia]e [!UICONTROL Aiuto].
1. Tocca **[!UICONTROL Fine]** per confermare le modifiche o **[!UICONTROL Annulla]** per eliminare le modifiche.

## Esempio: stili in linea per un componente campo {#example-inline-styles-for-a-field-component}

Le immagini seguenti rappresentano un campo di testo prima e dopo l’applicazione degli stili in linea.

![Componente casella di testo prima dell’applicazione dello stile in linea](assets/no-style.png)

Componente casella di testo prima di applicare proprietà di stile in linea

Osserva la modifica nello stile della casella di testo come mostrato nell’immagine seguente dopo aver applicato le seguenti proprietà CSS.

<table>
 <tbody>
  <tr>
   <td><p>Selettore</p> </td>
   <td><p>Proprietà CSS</p> </td>
   <td><p>Valore</p> </td>
   <td><p>Effetto</p> </td>
  </tr>
  <tr>
   <td><p>Campo</p> </td>
   <td><p>border</p> </td>
   <td><p>Larghezza bordo =2 px</p> <p>Stile bordo=Uniforme</p> <p>Colore bordo=#1111</p> </td>
   <td><p>Crea un bordo largo 2 px nero intorno al campo</p> </td>
  </tr>
  <tr>
   <td><p>Casella di testo</p> </td>
   <td><p>background-color</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>Cambia il colore di sfondo in CornflowerBlue (#6495ED)</p> <p>Nota: Nel campo del valore è possibile specificare un nome di colore o il relativo codice esadecimale.</p> </td>
  </tr>
  <tr>
   <td><p>Etichetta</p> </td>
   <td><p>Dimension e posizione &gt; larghezza</p> </td>
   <td><p>100 px</p> </td>
   <td><p>Corregge la larghezza di 100 px per l’etichetta</p> </td>
  </tr>
  <tr>
   <td>Icona guida campo</td>
   <td>Testo &gt; Colore font</td>
   <td>#2ECC40</td>
   <td>Cambia il colore della faccia dell'icona della guida.</td>
  </tr>
  <tr>
   <td><p>Descrizione lunga</p> </td>
   <td><p>text-align</p> </td>
   <td><p>center</p> </td>
   <td><p>Allinea al centro la descrizione lunga dell’aiuto.</p> </td>
  </tr>
 </tbody>
</table>

![Stile della casella di testo dopo l’applicazione dello stile in linea](assets/applied-style.png)

Componente casella di testo dopo l’applicazione delle proprietà di stile in linea

Seguendo i passaggi descritti in precedenza, puoi selezionare e assegnare uno stile ad altri componenti, ad esempio pannelli, pulsanti di invio e pulsanti di scelta.

>[!NOTE]
>
>Le proprietà dello stile variano a seconda del componente selezionato.

## Copiare e incollare gli stili {#copy-paste-styles}

È inoltre possibile copiare e incollare uno stile da un componente a un altro in un modulo adattivo. In **[!UICONTROL Stile]** , tocca il componente e tocca l’icona Copia ![Copia](assets/property-copy-icon.svg).

Tocca l’altro componente dello stesso tipo e tocca l’icona Incolla ![Copia](assets/Smock_Paste_18_N.svg) per incollare lo stile copiato. Puoi anche toccare l’icona Cancella stile ![Copia](assets/clear-style-icon.svg) per cancellare lo stile applicato.

## Impostare stili per diversi stati di un componente {#set-styles-for-states}

Puoi impostare gli stili per diversi stati di un tipo di componente. I diversi stati includono: [!UICONTROL Focus], [!UICONTROL Disabilitato], [!UICONTROL Hover], [!UICONTROL Errore], [!UICONTROL Completato]e [!UICONTROL Obbligatorio].

Per definire lo stile per uno stato di un componente:

1. In **[!UICONTROL Stile]** , tocca il componente e tocca l’icona Modifica ![Modifica](assets/Smock_Edit_18_N.svg).

1. Seleziona lo stato del componente utilizzando **[!UICONTROL Stato]** elenco a discesa.

   ![Seleziona stato](assets/select-state.png)

1. Definisci lo stile per lo stato selezionato del componente e tocca ![Salva](assets/save_icon.svg) per salvare le proprietà.

Puoi anche simulare gli stati di successo e di errore. Tocca l’icona Espandi per visualizzare l’icona **[!UICONTROL Simulazione riuscita]** e **[!UICONTROL Errore Simulazione]** opzioni.

![Simulazione degli stati](assets/simulate-states.png)
