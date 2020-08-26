---
title: Esperienza unificata per gli strumenti di refactoring del codice
description: Esperienza unificata per gli strumenti di refactoring del codice
translation-type: tm+mt
source-git-commit: c00b10b4d564e05099740b9ff991624db4f37a3d
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---


# Esperienza unificata per gli strumenti di refactoring del codice {#unified-experience}

Strumenti multipli con diversi punti di interazione per i clienti creano un&#39;esperienza disgiunta e aumentano la complessità nell&#39;utilizzo degli strumenti, con ogni esigenza di esecuzione diversa in termini di installazione, configurazione ed esecuzione.

## Benefits {#benefits}

L’esperienza unificata per gli strumenti di refactoring del codice richiama ed esegue tutti gli strumenti di refactoring del codice che funzionano sul codice sorgente dalla stessa posizione.

L’esperienza unificata per gli strumenti di refactoring dei codici insieme ai repository dei partner consente di:

* Unificate tutti gli strumenti per la migrazione del codice sorgente in un’ `node.js` applicazione esposta `aio-cli plugin` per fornire all’utente un’esperienza utente coerente.

* Disposizione per eseguire la migrazione globale tramite un singolo comando, fornendo al contempo la flessibilità di eseguire un particolare strumento come da requisito.

* Per semplificare l&#39;aggiunta futura di nuovi strumenti come l&#39;aggiunta di nuovo strumento al plugin, è sufficiente aggiungere un nuovo comando per lo sviluppatore e un semplice aggiornamento del plugin per l&#39;utente, in modo che l&#39;esperienza rimanga coerente con l&#39;aggiunta di più valore.

### Nozioni di base sulla progettazione dell’applicazione

Questi strumenti unificano tutti gli strumenti di refactoring del codice in un&#39;unica applicazione node.js esposta come `aio-cli plugin` per fornire all&#39;utente un&#39;esperienza utente coerente.

Il plugin è costituito da due parti principali:

* **Interfaccia utente**

   `aio-cli` comandi per eseguire uno o più strumenti di migrazione (tramite il concatenamento degli strumenti da eseguire sequenzialmente)`config.yaml` che incorpora i parametri di input richiesti

* **Suite di strumenti sottostanti per la migrazione**

   Gli strumenti di migrazione eseguono le proprie funzionalità tramite:

   * Scansione della rispettiva sezione del codice del cliente ed esecuzione della migrazione (basata sull&#39;implementazione del codice per le best practice) per produrre l&#39;output che può essere convalidato e distribuito.

   * Registrazione delle operazioni eseguite durante la migrazione, in modo coerente, per produrre un rapporto di riepilogo.

## Utilizzo del plug-in {#using-plugin}

Consente di `aio-cli-plugin-aem-cloud-service-migration` ridefinire il codice del cliente, la struttura del repository o le configurazioni nel computer locale del cliente. Questa pagina acquisisce i requisiti dettagliati e le decisioni di progettazione per l&#39;esperienza unificata.
È disponibile come origine aperta per la community di utenti che può essere estesa per casi di utilizzo personalizzati.

## Disponibilità {#availability}

È possibile installare e utilizzare `aio-cli-plugin-aem-cloud-service-migration` tramite `aio-cli` (attualmente integrato solo con il dispatcher converter).

Fare riferimento a Risorse [Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) per saperne di più sull&#39;utilizzo e come potete contribuire a questo strumento.

Il codice plug-in è stato aperto in origine in Github.

