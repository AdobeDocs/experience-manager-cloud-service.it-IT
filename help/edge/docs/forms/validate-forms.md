---
title: 'Da fogli di calcolo a Forms: masterizzazione delle convalide dei campi di blocco adattivi di Forms'
description: Crea moduli potenti più rapidamente utilizzando fogli di calcolo e campi Forms Block Adaptive. Questa guida consente di creare convalide personalizzate per i campi blocco EDS Forms.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 16e1d42a-42d0-4335-ba81-feedea7ed7d7
source-git-commit: 2aa70e78764616f41fe64e324c017873cfba1d5b
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Aggiungere convalide ai campi modulo

Il blocco Forms adattivo dispone di funzioni di convalida integrate. Queste convalide vengono applicate automaticamente nei browser moderni in base al tipo di campo scelto e alle proprietà aggiuntive fornite.

## Informazioni sui tipi di campo e sulla convalida

Il blocco Forms adattivo supporta diversi [Tipi di ingresso HTML-5](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), inclusi testo, e-mail, numero, data e altro. Può anche ospitare [textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea), select e fieldset, oltre a funzioni complete di convalida degli input proprie di HTML-5.

utilizza i tipi di campo HTML per definire il tipo di dati che un utente può immettere. Diversi tipi di campo dispongono di regole di convalida incorporate diverse:

E-mail: questo tipo di campo convalida automaticamente l’input dell’utente in base a un formato di indirizzo e-mail comune. Gli utenti che immettono un messaggio e-mail non valido visualizzeranno un messaggio di errore.
Numero: questo tipo di campo consente solo l’input numerico. Gli utenti che immettono caratteri non numerici riceveranno un errore.
Data: questo tipo di campo convalida l’input dell’utente in base a un formato di data standard. Anche le date al di fuori di un intervallo ragionevole potrebbero essere segnalate come non valide.
URL: questo tipo di campo convalida l’input dell’utente in base a un formato URL valido. Gli utenti che immettono un URL non valido visualizzeranno un messaggio di errore.
Tel: questo tipo di campo è progettato specificamente per i numeri di telefono e potrebbe attivare la convalida in base a formati di paese specifici (non universalmente supportati).



