---
title: Separator component in Adaptive Forms
seo-title: Separator component in Adaptive Forms
description: You can use the separator component to visually segregate sections of a form.
seo-description: You can use the separator component to visually segregate sections of a form.
uuid: f8d2aed3-52aa-437f-bfe3-0c8779e7986c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: a8aa77fe-5880-4c4e-9e1b-3c5a8772c29d
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---


# Componente separatore in Forms adattivo{#separator-component-in-adaptive-forms}

È possibile utilizzare il componente separatore per separare visivamente i pannelli di un modulo. È possibile definire l’aspetto e lo stile generali di un componente separatore specificando le seguenti proprietà del componente separatore:

* **Nome elemento:** Specifica il nome del componente. Le espressioni SOM si rivolgono al componente con il valore specificato nel campo Nome elemento .
* **Spessore:** Specifica lo spessore in pixel del componente separatore.

* **Classe CSS:** Specifica la classe CSS personalizzata per il componente separatore

* **Stili in linea:** Con [!DNL AEM Forms], ora puoi applicare gli stili CSS in linea ai singoli componenti Modulo adattivo e visualizzare in anteprima le modifiche in tempo reale.

You can use the Layout mode to define the number of columns that the separator component spans to. Per ulteriori informazioni, consulta [Utilizzare la modalità Layout per ridimensionare i componenti](resize-using-layout-mode.md).

To specify properties of a separator component:

1. Seleziona un componente separatore e tocca ![cmppr](assets/cmppr.png). Le proprietà si aprono nella barra laterale.
1. Fai clic su una scheda nella sezione Proprietà CSS in linea per specificare le proprietà CSS. Ad esempio: a) Nella scheda Campo, fai clic su **Aggiungi elemento**. Viene aggiunta una riga con due campi.
1. Nel primo campo da sinistra, specifica una proprietà CSS3 da applicare. For example, **border**. You can also select a property by clicking the down-arrow button. L’elenco a discesa non è esaustivo e puoi specificare qualsiasi nome di proprietà CSS3 supportato in questo campo.
1. In the adjoining field, specify a valid value for the specified CSS3 property. Ad esempio: **Nero solido 3 px**.
1. Click **Add Item** to specify another property and its value.
1. Fai clic su **Anteprima** per visualizzare in anteprima le modifiche apportate al modulo.
1. Fai clic su **OK** per confermare le modifiche o **Annulla** per uscire dalla finestra di dialogo senza apportare alcuna modifica.

