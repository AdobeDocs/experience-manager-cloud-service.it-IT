---
title: Esperienza unificata per gli strumenti di refactoring del codice
description: Esperienza unificata per gli strumenti di refactoring del codice
translation-type: tm+mt
source-git-commit: 03434343829e1a1fb95256a607619b55626c6afc
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 1%

---


# Esperienza unificata per gli strumenti di refactoring del codice {#unified-experience}

Abbiamo sviluppato strumenti per automatizzare alcune delle attività di refactoring del codice necessarie per essere compatibili con AEM come Cloud Service. Per ridurre la complessità associata all&#39;installazione e alla configurazione di diversi strumenti di refactoring del codice, abbiamo sviluppato un plugin per unificare gli strumenti che operano su codice e repository.

## Benefits {#benefits}

Il plug-in Esperienza unificata offre i seguenti vantaggi:

* Unisce gli strumenti che lavorano sul codice sorgente in un&#39; `node.js` applicazione esposta come `aio-cli ` plug-in per fornire all&#39;utente un&#39;esperienza utente coerente.

* Consente di eseguire tutti gli strumenti tramite un singolo comando, fornendo al contempo la flessibilità necessaria per eseguire strumenti specifici.

* Offre estensibilità per semplificare l&#39;aggiunta di nuovi strumenti, mantenendo al tempo stesso un&#39;esperienza coerente.

## Informazioni sul plug-in {#understanding-plugin}

Il `aio-cli-plugin-aem-cloud-service-migration` plugin è costituito da due parti principali:

* **Interfaccia utente**

   * `aio-cli` comandi per eseguire uno o più strumenti di refactoring del codice (concatenando gli strumenti da eseguire in sequenza)
   * `config.yaml` che accetta i parametri di input richiesti

* **Suite di strumenti per il refactoring del codice sottostante**

   Gli strumenti di refactoring del codice eseguono le loro funzionalità tramite:

   * Scansione della rispettiva sezione del codice del cliente e manipolazione del codice (in base all&#39;implementazione del codice per le best practice) per produrre l&#39;output che può essere convalidato e distribuito.

   * Generazione di un rapporto di riepilogo per registrare le operazioni eseguite durante l&#39;esecuzione.

## Disponibilità {#availability}

Fare riferimento a Risorse [Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) per saperne di più sull&#39;utilizzo e come puoi contribuire a questo codice plug-in open source in GitHub.

>[!NOTE]
>Attualmente solo Dispatcher Converter è integrato con il plug-in.
