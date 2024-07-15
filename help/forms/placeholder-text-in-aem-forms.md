---
title: Come si aggiunge il testo segnaposto ai campi modulo?
description: Il testo segnaposto ha lo scopo di aiutare l'utente a immettere dati quando il controllo non contiene alcun valore. Potrebbe essere un valore di esempio o una breve descrizione del formato previsto.
source-git-commit: d33c7278d16a8cce76c87b606ca09aa91f1c3563
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# Testo segnaposto in [!DNL AEM Forms] {#placeholder-text-in-aem-forms}

Il testo segnaposto rappresenta una parola o una breve frase. Lo scopo è quello di aiutare l&#39;utente a inserire dati quando il controllo non ha valore. Un testo segnaposto può essere un valore di esempio o una breve descrizione del formato previsto. Il testo segnaposto viene visualizzato prima che l’utente immetta un valore, viene rimosso quando l’utente immette o seleziona un valore.

>[!NOTE]
>
>Il testo segnaposto, se specificato, deve avere un valore che non contenga caratteri di riga nuovi.

![Componente data con e senza testo segnaposto](assets/dat-picker-place-holder-text.png)

**A.** Componente data con testo segnaposto **B.** Componente data senza testo segnaposto

[!DNL AEM Forms] supporta il testo segnaposto per i campi casella password, selettore data, casella numerica e casella di testo.\
I testi segnaposto non sono supportati per il widget data nativo di HTML5. Per specificare un testo segnaposto:

1. Fare clic con il pulsante destro del mouse su un componente che supporta il testo segnaposto e scegliere **Modifica**. Viene visualizzata la finestra di dialogo Modifica componente.

1. Apri la scheda **Titolo e testo**.
1. Specificare una parola o una breve frase nella **casella di testo Segnaposto**. Fai clic su **OK**.

>[!NOTE]
>
>Testo segnaposto non supportato in [!DNL Microsoft Internet Explorer 9].

