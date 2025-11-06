---
title: Aggiungere sezioni ripetibili a un modulo
description: Aggiungere sezioni ripetibili a un modulo EDS
feature: Edge Delivery Services
exl-id: 062d5a88-48ca-421f-bf0d-1483e3cfee28
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 100%

---

# Aggiungere sezioni ripetibili a un modulo

I blocchi di moduli adattivi consentono di aggiungere o rendere ripetibile una sezione o un componente di un modulo. Questo consente agli utenti di immettere più volte informazioni per lo stesso tipo di dati, semplificando così la raccolta di informazioni quali esperienze lavorative o formazione.

Si consideri, ad esempio, un modulo utilizzato per raccogliere informazioni sull’esperienza lavorativa di una persona. È possibile che sia disponibile una sezione ripetibile per l’acquisizione dei dettagli di ogni processo precedente. In genere, la sezione ripetibile contiene campi quali il nome dell’azienda, la qualifica, le date di assunzione e le responsabilità lavorative. L’utente può aggiungere più istanze della sezione ripetibile per immettere informazioni su ogni lavoro svolto.

Alla fine di questo articolo imparerai a:

- [creare una sezione ripetibile in un modulo](#add-repeatable-sections-to-a-form)
- [impostare il numero minimo o massimo di ripetizioni in un modulo](#set-minimum-or-maximum-number-of-repetitions-for-a-repeatable-section)

## creare una sezione ripetibile

La creazione di una sezione ripetibile in un modulo consente agli utenti di immettere più istanze dello stesso insieme di dati, consentendo una raccolta efficiente di informazioni ripetitive. Per creare una sezione ripetibile in un modulo:

1. Vai alla cartella del progetto Edge Deliver in Microsoft SharePoint o Google Workspace e apri il foglio di calcolo.

1. Aggiungere un campo modulo con la proprietà `type` impostata su `fieldset`
1. Specifica il `Name` di campo. La proprietà nome viene utilizzata per creare una sezione ripetibile.
1. Abilita ripetibilità impostando `repeatable` su `true`.
1. Specifica un `label` descrittivo per il campo. Funge da intestazione per la sezione ripetibile.

   Fare riferimento all’immagine seguente per un’illustrazione di una sezione della cronologia lavorativa all’interno di un modulo di candidatura.

   ![](/help/edge/assets/repeatable-section-example-job-application-form.png)

1. Per ogni campo che desideri includere nella sezione, impostane la proprietà `Fieldset` allo stesso nome scelto al passaggio 3.

   Ad esempio, designa `experience` nella proprietà Fieldset di tutti i campi rilevanti da includere nella sezione `employment history`.

   ![esempio di campo sezione ripetibile e relative proprietà](/help/edge/assets/repeatable-section--mention-fieldset-name-example-job-application-form.png)

1. Utilizza la [barra laterale di AEM](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) per visualizzare in anteprima e pubblicare il foglio. La sezione ripetibile viene aggiunta al modulo.

   Sotto la sezione ripetibile, è possibile trovare un pulsante **Aggiungi** che semplifica l’aggiunta di più sezioni.

   ![sezione ripetibile, pulsante Aggiungi, per aggiungere più sezioni ](/help/edge/assets/repeatable-section-example.png)


## Impostazione delle ripetizioni minime e massime

Nella progettazione dei moduli è utile impostare ripetizioni minime e massime per le sezioni ripetibili. In questo modo, puoi stabilire controllo e coerenza guidando al contempo gli utenti in modo efficace. Per impostare un numero minimo o massimo di ripetizioni:

1. Vai alla cartella del progetto Edge Deliver in Microsoft SharePoint o Google Workspace e apri il foglio di calcolo.

1. Per un campo di proprietà `type` `fieldset` e `repeatable` impostata su `true`:

   - imposta la proprietà `min` per specificare il numero minimo di ripetizioni della sezione.

   - imposta la proprietà `max` per specificare il numero massimo di ripetizioni della sezione.

   ![Impostare le proprietà min e max per specificare il numero di ripetizioni della sezione](/help/edge/assets/repeatable-section-set-min-max.png)

1. Utilizza la [barra laterale di AEM](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) per visualizzare in anteprima e pubblicare il foglio.

   Durante l’aggiunta di una sezione ripetibile, gli utenti trovare un’icona **Elimina** che semplifica la rimozione delle sezioni ripetibili. Una volta aggiunte, queste sezioni non possono essere ridotte a un numero di istanze inferiore a quello specificato dalla proprietà `min`. In questo modo si garantisce il rispetto dei requisiti minimi stabiliti per la compilazione del modulo.


