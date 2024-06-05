---
title: Esperienza unificata per gli strumenti di refactoring del codice
description: Scopri Unified Experience for Code Refactoring Tools.
exl-id: daee0e2d-1e2b-41a3-acab-fc59142d0e05
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 1%

---

# Esperienza unificata per gli strumenti di refactoring del codice {#unified-experience}

Adobe ha sviluppato strumenti per automatizzare alcune delle attività di refactoring del codice necessarie per la compatibilità con Adobe Experience Manager (AEM) as a Cloud Service. Per ridurre la complessità associata all’installazione e alla configurazione di diversi strumenti di refactoring del codice, Adobe ha sviluppato un plug-in per unificare gli strumenti che operano sul codice e sugli archivi.

## Vantaggi {#benefits}

Il plug-in Unified Experience offre i seguenti vantaggi:

* Unisce in un unico strumento gli strumenti che lavorano sul codice sorgente `node.js` applicazione esposta come `aio-cli ` plug-in per fornire all’utente un’esperienza utente coerente.

* Esegue tutti gli strumenti tramite un singolo comando, fornendo al contempo la flessibilità necessaria per eseguire strumenti specifici in base alle esigenze.

* Semplifica l’aggiunta di nuovi strumenti, mantenendo coerente l’esperienza.

## Informazioni sul plug-in {#understanding-plugin}

Il `aio-cli-plugin-aem-cloud-service-migration` Il plug-in è costituito da due parti principali:

* **Interfaccia utente**

   * `aio-cli` comandi per eseguire uno o più strumenti di refactoring del codice (concatenando gli strumenti da eseguire in sequenza).
   * `config.yaml` che accetta i parametri di input richiesti.

* **Suite di strumenti di refactoring del codice sottostante**

  Gli strumenti di refactoring del codice eseguono le loro funzionalità tramite:

   * Analizzare la rispettiva sezione del codice del cliente e manipolare il codice (in base all’implementazione del codice per le best practice) per produrre l’output che può quindi essere convalidato e distribuito.

   * Produzione di un rapporto di riepilogo per registrare le operazioni eseguite durante l&#39;esecuzione.

## Disponibilità {#availability}

Consulta [Risorsa Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) dove puoi scoprire l’utilizzo e come contribuire a questo codice plug-in open source in GitHub.

>[!NOTE]
>Attualmente il plug-in è integrato con AEM Dispatcher Converter e Repository Modernizer.
