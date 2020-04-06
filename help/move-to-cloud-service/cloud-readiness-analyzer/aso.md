---
title: Panoramica di AEM System
description: Panoramica di AEM System
translation-type: tm+mt
source-git-commit: aa6bb878ea4c58ba1e2fbf82d53effaa1a72d668

---


# Panoramica di AEM System {#aem-system}

Questa pagina descrive la panoramica di sistema di Adobe Experience Manager (AEM).

## Sfondo {#background}

Questo pattern viene utilizzato per identificare informazioni generali che forniscono una panoramica del sistema AEM. Le informazioni possono includere elementi quali:

Versione AEM: prodotti AEM utilizzati (Siti, Risorse, Moduli e così via) Conteggio dei nodi (pagine, risorse e così via)

## Dati pattern {#pattern-data}

Nella rappresentazione JSON del pattern sono inclusi gli oggetti seguenti:

* **item.message**: si riferisce al messaggio del pattern.
* **item.context**: fa riferimento a informazioni aggiuntive sulle informazioni della panoramica:
   * *type*: Il tipo di dati contestuali, &quot;aem.version&quot;, &quot;aem.product&quot; o &quot;node.count&quot;.
   * *data*: Un oggetto JSON contenente i dati corrispondenti al tipo: &quot;version&quot; (stringa), &quot;product&quot; (stringa) o &quot;count&quot; (numero intero).

### Possibili implicazioni e rischi {#possible-implications}

Non applicabile.

### Soluzioni possibili {#possible-solutions}

Non applicabile.
