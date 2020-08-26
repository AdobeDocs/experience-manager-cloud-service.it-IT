---
title: Esperienza unificata per gli strumenti di refactoring del codice
description: Esperienza unificata per gli strumenti di refactoring del codice
translation-type: tm+mt
source-git-commit: df41244712e1792e5265e4e6c8104962899c9b26
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---


# Esperienza unificata per gli strumenti di refactoring del codice {#unified-experience}

Gli strumenti Unified Experience for Code Refactoring (Esperienza unificata per il ripristino del codice) uniscono l&#39;esperienza per l&#39;esecuzione di AEM come strumenti di refactoring del codice di Cloud Service che operano su file dispatcher, codice e repository.

Questo strumento riduce la complessità dell’utilizzo di strumenti di refactoring del codice, con ogni esigenza di esecuzione diversa in termini di installazione, configurazione ed esecuzione.

![immagine](/help/move-to-cloud-service/assets/unified-1.png)

## Benefits {#benefits}

Gli strumenti Unified Experience for Code Refactoring richiamano ed eseguono tutti gli strumenti di refactoring del codice che funzionano sul codice sorgente dalla stessa posizione.

Questi strumenti, insieme ai repository di corredo, consentono:

* L&#39;unificazione di tutti gli strumenti per la migrazione del codice sorgente in un&#39; `node.js` applicazione è stata esposta `aio-cli plugin` per fornire all&#39;utente un&#39;esperienza utente coerente.

* Provisioning per eseguire la migrazione globale tramite un singolo comando, fornendo al contempo la flessibilità di eseguire un particolare strumento in base alle esigenze.

* Per semplificare l&#39;aggiunta futura di nuovi strumenti come l&#39;aggiunta di nuovo strumento al plugin, è sufficiente aggiungere un nuovo comando per lo sviluppatore e un semplice aggiornamento del plugin per l&#39;utente, in modo che l&#39;esperienza rimanga coerente con l&#39;aggiunta di più valore.

## Informazioni sul plug-in {#understanding-plugin}

Consente di `aio-cli-plugin-aem-cloud-service-migration` ridefinire il codice del cliente, la struttura del repository o le configurazioni nel computer locale del cliente. Questa pagina acquisisce i requisiti dettagliati e le decisioni di progettazione per l&#39;esperienza unificata.
È disponibile come origine aperta per la community di utenti che può essere estesa per casi di utilizzo personalizzati.

Questi strumenti unificano tutti gli strumenti di refactoring del codice in un&#39;unica applicazione node.js esposta come `aio-cli plugin` per fornire all&#39;utente un&#39;esperienza utente coerente. Il plug-in scansiona la base di codice locale del cliente e produce AEM come codice, configurazioni e pacchetti compatibili con il Cloud Service che possono essere poi distribuiti in ambienti Cloud Service.

Il plugin è costituito da due parti principali:

* **Interfaccia utente**

   `aio-cli` comandi per eseguire uno o più strumenti di migrazione (tramite il concatenamento degli strumenti da eseguire sequenzialmente)`config.yaml` che incorpora i parametri di input richiesti

* **Suite di strumenti sottostanti per la migrazione**

   Gli strumenti di migrazione eseguono le proprie funzionalità tramite:

   * Scansione della rispettiva sezione del codice del cliente ed esecuzione della migrazione (basata sull&#39;implementazione del codice per le best practice) per produrre l&#39;output che può essere convalidato e distribuito.

   * Registrazione delle operazioni eseguite durante la migrazione, in modo coerente, per produrre un rapporto di riepilogo.

## Disponibilità {#availability}

È possibile installare e utilizzare il `aio-cli-plugin-aem-cloud-service-migration` tramite `aio-cli`.

>[!NOTE]
>Attualmente questo strumento è integrato solo con Dispatcher Converter.

Fare riferimento a Risorse [Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) per saperne di più sull&#39;utilizzo e come puoi contribuire a questo codice plug-in open source in GitHub.

