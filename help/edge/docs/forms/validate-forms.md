---
title: 'Da fogli di calcolo a Forms: masterizzazione delle convalide dei campi blocco modulo'
description: Crea moduli potenti più rapidamente utilizzando fogli di calcolo e campi blocco modulo. Questa guida consente di creare convalide personalizzate per i campi blocco EDS Forms.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 78d40574e6fea8dde22414e43fd77215b9e7d2a1
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# Aggiungere convalide ai campi modulo

Il blocco di modulo dispone di funzioni di convalida integrate. Queste convalide vengono applicate automaticamente nei browser moderni in base al tipo di campo scelto e alle proprietà aggiuntive fornite.

## Informazioni sui tipi di campo e sulla convalida

Il blocco Form supporta diversi [Tipi di ingresso HTML-5](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), inclusi testo, e-mail, numero, data e altro. Può anche ospitare [textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea), select e fieldset, oltre a funzioni complete di convalida degli input proprie di HTML-5.

utilizza i tipi di campo HTML per definire il tipo di dati che un utente può immettere. Diversi tipi di campo dispongono di regole di convalida incorporate diverse:

E-mail: questo tipo di campo convalida automaticamente l’input dell’utente in base a un formato di indirizzo e-mail comune. Gli utenti che immettono un messaggio e-mail non valido visualizzeranno un messaggio di errore.
Numero: questo tipo di campo consente solo l’input numerico. Gli utenti che immettono caratteri non numerici riceveranno un errore.
Data: questo tipo di campo convalida l’input dell’utente in base a un formato di data standard. Anche le date al di fuori di un intervallo ragionevole potrebbero essere segnalate come non valide.
URL: questo tipo di campo convalida l’input dell’utente in base a un formato URL valido. Gli utenti che immettono un URL non valido visualizzeranno un messaggio di errore.
Tel: questo tipo di campo è progettato specificamente per i numeri di telefono e potrebbe attivare la convalida in base a formati di paese specifici (non universalmente supportati).


## Vedi altro

* [Creare e visualizzare in anteprima un modulo](/help/edge/docs/forms/create-forms.md)
* [Abilita modulo per l’invio di dati](/help/edge/docs/forms/submit-forms.md)
* [Pubblicare un modulo nella pagina Sites](/help/edge/docs/forms/publish-eds-forms.md)
* [Aggiungere convalide ai campi modulo](/help/edge/docs/forms/validate-forms.md)
* [Modificare i temi e lo stile del modulo](/help/edge/docs/forms/style-theme-forms.md)