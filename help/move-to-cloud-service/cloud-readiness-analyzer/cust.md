---
title: Personalizzazione rilevata
description: Personalizzazione rilevata
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 3%

---


# Personalizzazione rilevata {#cust-pattern}

Questa pagina descrive il codice del pattern rilevato dalla personalizzazione.

## Sfondo {#background}

Questo codice del pattern viene utilizzato per identificare le personalizzazioni effettuate nell’istanza di AEM. Poiché la personalizzazione di AEM è comune, questo pattern non indica necessariamente che si è verificato un problema. Identifica un record di personalizzazioni in modo che possano essere valutate in relazione al loro impatto sui piani di aggiornamento.

Le personalizzazioni rilevate includono:

* Codice cliente (pacchetti e configurazioni)
* Pacchetti di terze parti
* Integrazioni con i servizi di terze parti
* Indici Oak non standard

## Dati pattern {#pattern-data}

Nella rappresentazione JSON del pattern sono inclusi gli oggetti seguenti:

* **item.message**: si riferisce al messaggio del pattern.
* **item.context**: fa riferimento a informazioni aggiuntive sulle informazioni della panoramica:
   * *type*: customization.found.
   * *data*: Un oggetto JSON contenente i dati che descrivono la personalizzazione

### Possibili implicazioni e rischi {#possible-implications}

Non applicabile.

### Soluzioni possibili  {#possible-solutions}

Non applicabile.
