---
title: Cos’è un componente separatore in Adaptive Forms?
description: Il componente Separatore in Forms adattivo consente di segregare visivamente le sezioni di un modulo.
uuid: f8d2aed3-52aa-437f-bfe3-0c8779e7986c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
source-git-commit: 7e3eb3426002408a90e08bee9c2a8b7a7bfebb61
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 1%

---


# Componente separatore in Adaptive Forms{#separator-component-in-adaptive-forms}

È possibile utilizzare il componente Separatore per separare visivamente i pannelli di un modulo. È possibile definire l&#39;aspetto e lo stile generali di un componente separatore specificando le seguenti proprietà del componente separatore:

* **Nome elemento:** Specifica il nome del componente. Le espressioni SOM indirizzano il componente con un valore specificato nel campo Nome elemento.
* **Spessore:** Specifica lo spessore in pixel del componente separatore.

* **Classe CSS:** Specifica la classe CSS personalizzata per il componente separatore

* **Stili in linea:** Con [!DNL AEM Forms]Ora puoi applicare stili CSS in linea ai singoli componenti del modulo adattivo e visualizzare in anteprima le modifiche in tempo reale.

Puoi utilizzare la modalità Layout per definire il numero di colonne su cui si estende il componente Separatore. Per ulteriori informazioni, consulta [Utilizzare la modalità Layout per ridimensionare i componenti](resize-using-layout-mode.md).

Per specificare le proprietà di un componente separatore:

1. Seleziona un componente separatore e tocca ![cmppr](assets/cmppr.png). Le proprietà si aprono nella barra laterale.
1. Fai clic su una scheda nella sezione Proprietà CSS in linea per specificare le proprietà CSS. Ad esempio, un. Nella scheda Campo fare clic su **Aggiungi elemento**. Viene aggiunta una riga con due campi.
1. Nel primo campo da sinistra, specifica una proprietà CSS3 da applicare. Ad esempio: **bordo**. Puoi anche selezionare una proprietà facendo clic sul pulsante freccia giù. L’elenco a discesa non è esaustivo ed è possibile specificare qualsiasi nome di proprietà CSS3 supportato in questo campo.
1. Nel campo adiacente, specifica un valore valido per la proprietà CSS3 specificata. Ad esempio: **3 pixel in nero uniforme**.
1. Clic **Aggiungi elemento** per specificare un&#39;altra proprietà e il relativo valore.
1. Clic **Anteprima** in modo da visualizzare le modifiche nel modulo.
1. Effettua una delle operazioni seguenti:
   * Conferma le modifiche facendo clic su **OK**
   * Per uscire dalla finestra di dialogo senza apportare alcuna modifica, fare clic su **Annulla**.

