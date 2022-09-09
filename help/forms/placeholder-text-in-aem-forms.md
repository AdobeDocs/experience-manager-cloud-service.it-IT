---
title: Testo segnaposto in [!DNL AEM Forms]
description: Il testo segnaposto ha lo scopo di aiutare l’utente a inserire dati quando il controllo non ha alcun valore. Può trattarsi di un valore di esempio o di una breve descrizione del formato previsto.
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Testo segnaposto in [!DNL AEM Forms] {#placeholder-text-in-aem-forms}

Il testo segnaposto rappresenta una parola o una frase breve. Ha lo scopo di aiutare l’utente a inserire dati quando il controllo non ha alcun valore. Un testo segnaposto può essere un valore di esempio o una breve descrizione del formato previsto. Il testo segnaposto viene visualizzato prima che l’utente immetta un valore e viene rimosso quando l’utente immette o seleziona un valore.

>[!NOTE]
>
>Il testo segnaposto, se specificato, deve avere un valore che non contenga nuovi caratteri di riga.

![Componente data con e senza testo segnaposto](assets/dat-picker-place-holder-text.png)

**A.** Componente data con testo segnaposto **B.** Componente data senza testo segnaposto

[!DNL AEM Forms] supporto del testo segnaposto per i campi Casella password, Selezione data, Casella numerica e Casella di testo.\
I testi segnaposto non sono supportati per il widget di data nativo di HTML5. Per specificare un testo segnaposto:

1. Fai clic con il pulsante destro del mouse su un componente che supporta il testo segnaposto e fai clic su **Modifica**. Viene visualizzata la finestra di dialogo Modifica componente.

1. Apri **Titolo e testo** scheda .
1. Specifica una parola o una frase breve nel **Casella di testo segnaposto**. Fai clic su **OK**.

>[!NOTE]
>
>Testo segnaposto non supportato su [!DNL Microsoft Internet Explorer 9].

