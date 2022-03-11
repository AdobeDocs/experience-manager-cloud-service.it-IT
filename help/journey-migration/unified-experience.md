---
title: Esperienza unificata per gli strumenti di refactoring del codice
description: Esperienza unificata per gli strumenti di refactoring del codice
exl-id: daee0e2d-1e2b-41a3-acab-fc59142d0e05
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---

# Esperienza unificata per gli strumenti di refactoring del codice {#unified-experience}

Abbiamo sviluppato strumenti per automatizzare alcune delle attività di refactoring del codice necessarie per essere compatibili con AEM as a Cloud Service. Per ridurre la complessità associata all&#39;installazione e alla configurazione di diversi strumenti di refactoring del codice, abbiamo sviluppato un plug-in per unificare gli strumenti che operano su codice e archivi.

## Vantaggi {#benefits}

Il plug-in Esperienza unificata offre i seguenti vantaggi:

* Unisce gli strumenti che funzionano sul codice sorgente in un unico `node.js` applicazione esposta come `aio-cli ` per fornire all’utente un’esperienza utente coerente.

* Offre la possibilità di eseguire tutti gli strumenti tramite un singolo comando, fornendo al contempo la flessibilità di eseguire strumenti specifici in base alle esigenze.

* Offre estensibilità per semplificare l’aggiunta di nuovi strumenti, mantenendo al tempo stesso coerente l’esperienza.

## Informazioni sul plug-in {#understanding-plugin}

La `aio-cli-plugin-aem-cloud-service-migration` il plugin è costituito da due parti principali:

* **Interfaccia utente**

   * `aio-cli` comandi per eseguire uno o più strumenti di refactoring del codice (tramite il concatenamento degli strumenti da eseguire in sequenza).
   * `config.yaml` che acquisisce i parametri di input richiesti.

* **Suite di strumenti di refactoring del codice sottostante**

   Gli strumenti di refactoring del codice eseguono le loro funzionalità tramite:

   * Analisi della rispettiva sezione del codice del cliente e manipolazione del codice (basata sull’implementazione del codice per le best practice) per produrre l’output che può essere convalidato e distribuito.

   * Generazione di un report di riepilogo per registrare le operazioni eseguite durante l&#39;esecuzione.

## Disponibilità {#availability}

Fai riferimento a [Risorsa Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) per informazioni sull’utilizzo e su come contribuire a questo codice plug-in open source in GitHub.

>[!NOTE]
>Attualmente il plug-in è integrato con AEM Dispatcher Converter e Repository Modernizer.
