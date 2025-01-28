---
title: Modelli e-mail HTML in Forms adattivo su Forms as a Cloud Service
description: Scopri come utilizzare i modelli e-mail con moduli adattivi.
feature: Adaptive Forms, Core Components
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: b5340c23f0a2496f0528530bdd072871f0d70d62
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---

# Modelli e-mail in Forms adattivo

Forms adattivo consente di utilizzare modelli e-mail HTML e di testo normale. I modelli e-mail di HTML consentono di inviare e-mail avanzate, personalizzate e visivamente accattivanti quando viene inviato un modulo. Queste e-mail possono essere personalizzate con i dati del modulo e migliorate utilizzando vari tag e-mail, come immagini e collegamenti. Con Adaptive Forms, puoi caricare un file contenente un modello di HTML o utilizzare un editor di testo normale per creare questi modelli.

![Modelli e-mail HTML](/help/forms/assets/html-email.png)

Questo articolo consente di configurare e utilizzare i modelli e-mail in Adaptive Forms. Entro la fine, potrai:

* [Configurare un modello di HTML per un modulo adattivo](#configure-an-html-template-for-an-adaptive-form)
* [Configurare un modello e-mail in testo normale per un modulo adattivo](#configure-a-plain-text-template-for-an-adaptive-form)
* [Utilizzare i dati dei moduli nei modelli e-mail](#use-form-data-in-your-email-templates)


Ecco una breve panoramica dei passaggi necessari:

1. Apri il modulo adattivo per la modifica.
1. Configura l&#39;azione di invio [Invia e-mail](/help/forms/configure-submit-action-send-email.md).
1. Seleziona o carica un modello di HTML oppure immetti manualmente il modello di e-mail.
1. Verifica la configurazione e-mail.

## Configurare un modello di HTML per un modulo adattivo

Puoi impostare un modulo adattivo per inviare un&#39;e-mail al momento dell&#39;invio utilizzando l&#39;[**Invia e-mail** azione di invio](/help/forms/configure-submit-action-send-email.md). L’azione fornisce due metodi per configurare un modello di HTML:

### Opzione 1: selezionare un file contenente il modello di HTML

Prima di procedere, assicurati di aver caricato il modello di HTML nell’ambiente AEM Forms.

1. Apri il modulo adattivo per la modifica.
1. Vai a **Browser contenuti**, seleziona il **Contenitore guida**, quindi tocca l&#39;icona delle proprietà. Verrà visualizzata una finestra di dialogo con il titolo `Adaptive Form Container`.
1. Vai alla scheda **Invio** e seleziona l&#39;azione di invio **Invia e-mail**.

   ![Invia azione di invio e-mail](/help/forms/assets/send-email-action.png)

1. Abilita l&#39;opzione **Usa modello esterno**.
1. Abilita l&#39;opzione **Usa modello HTML**.
1. Fai clic sull’icona della cartella per l’opzione Percorso modello esterno e sfoglia per selezionare il modello di HTML.
1. Fai clic su **Fine** per salvare la configurazione.

Il modello di HTML è ora configurato per il modulo adattivo.

### Opzione 2: inserire o incollare manualmente un modello di HTML

1. Apri il modulo adattivo per la modifica.
1. Vai a **Browser contenuti**, seleziona il **Contenitore guida**, quindi tocca l&#39;icona delle proprietà. Verrà visualizzata una finestra di dialogo con il titolo `Adaptive Form Container`.
1. Vai alla scheda **Invio** e seleziona l&#39;azione di invio **Invia e-mail**.
1. Abilita l&#39;opzione **Usa modello HTML**.
1. Digita o incolla il codice HTML direttamente nella casella **Modello e-mail** fornita.


## Configurare un modello di testo normale per un modulo adattivo

Puoi impostare un modulo adattivo per inviare un&#39;e-mail al momento dell&#39;invio utilizzando l&#39;[**Invia e-mail** azione di invio](/help/forms/configure-submit-action-send-email.md). L’azione fornisce due metodi per configurare un modello di testo normale:

### Opzione 1: selezionare un file contenente il modello

Prima di procedere, assicurati di aver caricato il modello di HTML nell’ambiente AEM Forms.

1. Apri il modulo adattivo per la modifica.
1. Vai a **Browser contenuti**, seleziona il **Contenitore guida**, quindi tocca l&#39;icona delle proprietà. Verrà visualizzata una finestra di dialogo con il titolo `Adaptive Form Container`.
1. Vai alla scheda **Invio** e seleziona l&#39;azione di invio **Invia e-mail**.
1. Abilita l&#39;opzione **Usa modello esterno**.
1. Fai clic sull&#39;icona della cartella per l&#39;opzione **Percorso modello esterno** e sfoglia per selezionare il modello di testo normale.
1. Fai clic su Fine per salvare la configurazione.

Il modello è ora configurato per il modulo adattivo.

### Opzione 2: inserire o incollare manualmente un modello di HTML

1. Apri il modulo adattivo per la modifica.
1. Vai a **Browser contenuti**, seleziona il **Contenitore guida**, quindi tocca l&#39;icona delle proprietà. Verrà visualizzata una finestra di dialogo con il titolo `Adaptive Form Container`.
1. Vai alla scheda **Invio** e seleziona l&#39;azione di invio **Invia e-mail**.
1. Digita o incolla il codice del modello di testo normale direttamente nella casella **Modello e-mail** fornita.

## Utilizzare i dati del modulo nei modelli e-mail

È possibile includere i dati del modulo nei modelli e-mail utilizzando i segnaposto. Questi segnaposto vengono sostituiti in modo dinamico con i valori effettivi dei campi del modulo al momento dell’invio dell’e-mail. Ad esempio:

* ${name}: valore del campo denominato &quot;name&quot;.
* ${email}: valore del campo denominato &quot;email&quot;.
* ${message}: valore del campo denominato &quot;message&quot;.

### Modello e-mail HTML di esempio

Di seguito è riportato un esempio di modello e-mail di HTML che utilizza segnaposto per i dati del modulo:

```HTML
    <!DOCTYPE html>
    <html>
    <head>
        <title>Form Submission</title>
        <style>
            body {
                font-family: Arial, sans-serif;
                line-height: 1.6;
                color: #333;
            }
            h2 {
                color: #0056b3;
            }
        </style>
    </head>
    <body>
        <h2>Thank You for Your Submission</h2>
        <p>Dear ${name},</p>
        <p>We have received your submission with the following details:</p>
        <ul>
            <li><strong>Email:</strong> ${email}</li>
            <li><strong>Phone Number:</strong> ${phone_number}</li>
            <li><strong>Message:</strong> ${message}</li>
        </ul>
        <p>We will get back to you soon!</p>
        <p>Best regards,</p>
        <p>Your Team</p>
    </body>
    </html>
```

### Esempio di modello di e-mail in testo normale

Di seguito è riportato un esempio di modello di e-mail di testo normale:

```TXT
    
    Subject: Thank You for Your Submission
    
    Dear ${name},
    
    We have received your submission with the following details:
    
    - Email: ${email}
    - Phone Number: ${phone_number}
    - Message: ${message}
    
    We will get back to you soon!
    
    Best regards,
    Your Team
```

## Best practice per i modelli e-mail per HTML

* Assicurati che gli stili siano inline per una migliore compatibilità con i client e-mail.
* Rendi il tuo modello dinamico per un’esperienza migliore sui dispositivi mobili.
* Utilizza strumenti come Litmus o E-mail su Acid per visualizzare in anteprima il messaggio e-mail tra vari client e-mail.
* Assicurati che i nomi dei segnaposto corrispondano esattamente ai nomi dei campi modulo.
* Verifica la presenza di tag mancanti o errati nel modello di HTML.
* Verificare che l&#39;azione di invio [Invia e-mail](/help/forms/configure-submit-action-send-email.md) sia configurata correttamente.
