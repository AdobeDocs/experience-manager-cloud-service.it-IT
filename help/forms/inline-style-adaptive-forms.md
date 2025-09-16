---
title: Come si applicano gli stili in linea ai componenti di moduli adattivi?
description: Scopri come applicare stili personalizzati a un modulo adattivo, e come applicare le proprietà CSS in linea ai singoli componenti di un modulo adattivo.
feature: Adaptive Forms, Foundation Components
role: User, Developer
level: Intermediate
exl-id: 25adabfb-ff19-4cb2-aef5-0a8086d2e552
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 3%

---

# Stile in linea dei componenti del modulo adattivo {#inline-styling-of-adaptive-form-components}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/creating-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base.

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/inline-style-adaptive-forms.html) |
| AEM as a Cloud Service | Questo articolo |

Puoi definire l&#39;aspetto e lo stile generali di un modulo adattivo specificando gli stili tramite [editor temi](themes.md). Inoltre, puoi applicare stili CSS in linea ai singoli componenti del modulo adattivo e visualizzare all’istante le modifiche in anteprima. Gli stili in linea sostituiscono gli stili forniti nel tema.

## Applicare le proprietà CSS in linea {#apply-inline-css-properties}

Per aggiungere stili in linea a un componente:

1. Aprire il modulo nel generatore di moduli e impostare la modalità stile. Per cambiare la modalità in stile, nella barra degli strumenti della pagina, seleziona ![elenco a discesa dell&#39;area di lavoro](assets/Smock_ChevronDown.svg) > **[!UICONTROL Stile]**.
1. Selezionare un componente nella pagina, quindi selezionare il pulsante di modifica ![edit-button](assets/edit.svg). Le proprietà di stile si aprono nella barra laterale.

   Puoi anche selezionare i componenti dalla struttura gerarchica del modulo nella barra laterale. La struttura della gerarchia dei moduli è disponibile come Oggetti modulo nella barra laterale.

   Nella modalità [!UICONTROL Stile], puoi visualizzare i componenti elencati in Oggetti modulo. Tuttavia, l’elenco Oggetti modulo nella barra laterale elenca componenti quali campi e pannelli. I campi e i pannelli sono componenti generici che possono contenere componenti quali caselle di testo e pulsanti di scelta.

   Quando selezioni un componente dalla barra laterale, vengono visualizzati tutti i sottocomponenti elencati e le proprietà del componente selezionato. Puoi selezionare un sottocomponente specifico e assegnargli uno stile.

1. Fai clic su una scheda nella barra laterale per specificare le proprietà CSS. Puoi specificare proprietà quali:

   * [!UICONTROL Dimensioni e posizione] (impostazione di visualizzazione, spaziatura interna, altezza, larghezza, margine, posizione, indice z, virgola mobile, cancellazione, riversamento)
   * [!UICONTROL Testo] (famiglia di caratteri, peso, colore, dimensione, altezza della riga e allineamento)
   * [!UICONTROL Sfondo] (immagine e sfumatura, colore di sfondo)
   * [!UICONTROL Bordo] (larghezza, stile, colore, raggio)
   * [!UICONTROL Effetti] (Ombreggiatura, Opacità)
   * [!UICONTROL Avanzate] (consente di scrivere CSS personalizzati per il componente)

1. Analogamente, è possibile applicare stili per altre parti di un componente, ad esempio [!UICONTROL Widget], [!UICONTROL Didascalia] e [!UICONTROL Guida].
1. Seleziona **[!UICONTROL Fine]** per confermare le modifiche o **[!UICONTROL Annulla]** per ignorarle.

## Esempio: stili in linea per un componente campo {#example-inline-styles-for-a-field-component}

Le immagini seguenti rappresentano un campo di testo prima e dopo l’applicazione di stili in linea.

![Componente casella di testo prima dell&#39;applicazione dello stile in linea](assets/no-style.png)

Componente casella di testo prima di applicare proprietà di stile in linea

Osserva la modifica dello stile della casella di testo come mostrato nell’immagine seguente dopo l’applicazione delle seguenti proprietà CSS.

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
   <td><p>bordo</p> </td>
   <td><p>Larghezza bordo = 2 px</p> <p>Stile bordo=solido</p> <p>Colore bordo=#1111</p> </td>
   <td><p>Crea un bordo nero largo 2 pixel attorno al campo</p> </td>
  </tr>
  <tr>
   <td><p>Casella di testo</p> </td>
   <td><p>background-color</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>Cambia il colore di sfondo in blu fioreCornice (#6495ED)</p> <p>Nota: è possibile specificare un nome di colore o il relativo codice esadecimale nel campo valore.</p> </td>
  </tr>
  <tr>
   <td><p>Etichetta</p> </td>
   <td><p>Dimensioni e posizione &gt; larghezza</p> </td>
   <td><p>100 px</p> </td>
   <td><p>Imposta la larghezza come 100 px per l'etichetta</p> </td>
  </tr>
  <tr>
   <td>Icona guida campo</td>
   <td>Testo &gt; Colore carattere</td>
   <td>#2ECC40</td>
   <td>Cambia il colore della faccia dell'icona della guida.</td>
  </tr>
  <tr>
   <td><p>Descrizione lunga</p> </td>
   <td><p>text-align</p> </td>
   <td><p>centro</p> </td>
   <td><p>Allinea al centro la descrizione lunga della guida</p> </td>
  </tr>
 </tbody>
</table>

![Stile casella di testo dopo l&#39;applicazione dello stile in linea](assets/applied-style.png)

Componente casella di testo dopo l’applicazione delle proprietà di stile in linea

Seguendo i passaggi precedenti, è possibile selezionare e assegnare uno stile ad altri componenti, ad esempio pannelli, pulsanti di invio e pulsanti di scelta.

>[!NOTE]
>
>Le proprietà di stile variano in base al componente selezionato.

## Copiare e incollare gli stili {#copy-paste-styles}

È inoltre possibile copiare e incollare uno stile da un componente a un altro in un modulo adattivo. In modalità **[!UICONTROL Stile]**, seleziona il componente e l&#39;icona Copia ![Copia](assets/property-copy-icon.svg).

Selezionare l&#39;altro componente dello stesso tipo e l&#39;icona Incolla ![Copia](assets/Smock_Paste_18_N.svg) per incollare lo stile copiato. Puoi anche selezionare l&#39;icona Cancella stile ![Copia](assets/clear-style-icon.svg) per cancellare lo stile applicato.

## Impostare stili per diversi stati di un componente {#set-styles-for-states}

È possibile impostare stili per diversi stati di un tipo di componente. I diversi stati includono: [!UICONTROL Stato attivo], [!UICONTROL Disabilitato], [!UICONTROL Passaggio del mouse], [!UICONTROL Errore], [!UICONTROL Operazione riuscita] e [!UICONTROL Obbligatorio].

Per definire lo stile per uno stato di un componente:

1. Nella modalità **[!UICONTROL Stile]**, seleziona il componente e l&#39;icona Modifica ![Modifica](assets/Smock_Edit_18_N.svg).

1. Selezionare lo stato del componente utilizzando l&#39;elenco a discesa **[!UICONTROL Stato]**.

   ![Seleziona stato](assets/select-state.png)

1. Definisci lo stile per lo stato selezionato del componente e seleziona ![Salva](assets/save_icon.svg) per salvare le proprietà.

È inoltre possibile simulare gli stati di esito positivo e di errore. Seleziona l&#39;icona Espandi per visualizzare le opzioni **[!UICONTROL Simula esito positivo]** e **[!UICONTROL Simula errore]**.

![Simula stati](assets/simulate-states.png)


## Consulta anche {#see-also}

{{see-also}}


<!--

>[!MORELIKETHIS]
>
>* [Use themes in Adaptive Form Core Components ](/help/forms/using-themes-in-core-components.md)

-->