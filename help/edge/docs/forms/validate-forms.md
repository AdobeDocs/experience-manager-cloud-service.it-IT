---
title: 'Da fogli di calcolo a moduli: masterizzazione delle convalide dei campi del blocco moduli adattivi'
description: Crea moduli potenti più rapidamente utilizzando fogli di calcolo e campi blocco moduli adattivi. Questa guida consente di creare convalide personalizzate per i campi di blocco dei moduli EDS.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 16e1d42a-42d0-4335-ba81-feedea7ed7d7
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 100%

---

# Aggiungere convalide ai campi del modulo

Il blocco moduli adattivi dispone di funzioni di convalida incorporate. Queste convalide vengono applicate automaticamente nei browser moderni in base al tipo di campo scelto e alle proprietà aggiuntive fornite.

## Informazioni sui tipi di campo e sulla convalida

Il Blocco moduli adattivi supporta diversi [Tipi di ingresso HTML-5](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), inclusi testo, e-mail, numero, data e altro. Può anche ospitare [textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea), select e fieldset, oltre a funzioni complete di convalida degli input proprie di HTML-5.

Utilizza i tipi di campo HTML per definire il tipo di dati che un utente può immettere. Diversi tipi di campo dispongono di regole di convalida incorporate diverse:

E-mail: questo tipo di campo convalida automaticamente l’input dell’utente in base a un formato di indirizzo e-mail comune. Gli utenti che immettono un indirizzo e-mail non valido visualizzeranno un messaggio di errore.
Numero: questo tipo di campo consente solo l’input numerico. Gli utenti che immettono caratteri non numerici riceveranno un errore.
Data: questo tipo di campo convalida l’input dell’utente in base a un formato di data standard. Anche le date al di fuori di un intervallo ragionevole potrebbero essere segnalate come non valide.
URL: questo tipo di campo convalida l’input dell’utente in base a un formato URL valido. Gli utenti che immettono un URL non valido visualizzeranno un messaggio di errore.
Tel: questo tipo di campo è progettato specificamente per i numeri di telefono e potrebbe attivare la convalida in base a formati di paese specifici (non universalmente supportati).



