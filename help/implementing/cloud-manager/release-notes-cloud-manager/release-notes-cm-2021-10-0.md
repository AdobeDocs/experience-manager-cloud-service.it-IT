---
title: Note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2021.10.0
description: Note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2021.10.0
feature: Release Information
source-git-commit: 14042b45b14f2c5575fc96979579bb0aaffc9a17
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 3%

---

# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2021.10.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.10.0.

>[!NOTE]
>Per visualizzare le note sulla versione corrente per Adobe Experience Manager as a Cloud Service, fai clic su [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=it).

## Data di pubblicazione {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.10.0 è il 14 ottobre 2021.


### Novità {#what-is-new}

* In preparazione di alcune modifiche imminenti, nell’interfaccia utente verrà fatto riferimento alle pipeline di distribuzione esistenti ed etichettarle come **Stack completo** gasdotti.

* La scheda della pipeline è stata aggiornata per visualizzare una singola faccia integrata che mostra sia le pipeline di produzione che quelle non di produzione e l’utente può selezionare Esegui/Pausa/Riprendi direttamente dal menu delle azioni associato a ciascuna pipeline.

* Un utente con il ruolo di Deployment Manager può ora eliminare la pipeline di produzione in modo self-service tramite l’interfaccia utente.

* Le esperienze di aggiunta e modifica delle pipeline sono state aggiornate per poter utilizzare modelli moderni e familiari.

* Gli utenti di Cloud Manager ora possono inviare un feedback direttamente dall’interfaccia utente tramite l’ **Feedback** in alto a destra della pagina di destinazione.

* I grafici SLA annuali possono ora essere scaricati dall’interfaccia utente di Cloud Manager.

* Le esecuzioni della pipeline di qualità del codice e non di produzione ora utilizzeranno un processo di duplicazione poco profondo più efficiente durante il passaggio di creazione, consentendo ai clienti con archivi Git di dimensioni particolarmente grandi di ottenere tempi di creazione più rapidi.

* La procedura guidata Aggiungi Elenco consentiti IP informa l’utente se è stato raggiunto il numero massimo consentito di Elenchi consentiti IP.

* La documentazione API di Cloud Manager ora include un parco giochi interattivo che consente agli utenti connessi di sperimentare l’API dal proprio browser. Vedi [Playground API di Cloud Manager](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) per ulteriori dettagli.

* La descrizione comandi nella scheda Programma sarà più descrittiva se un’opzione di selezione in &quot;Passa a&quot; è disabilitata. Ora viene visualizzato &quot;Un ambiente di produzione non esiste&quot;.

### Correzioni di bug {#bug-fixes}

* In rare situazioni, quando uno staff Adobe ripristina l&#39;ambiente del cliente, il ripristino è stato considerato completo prima che l&#39;ambiente fosse completamente operativo.

* Alcune richieste interne effettuate durante la creazione dell’ambiente non sono state ritentate.

* Se si verifica un errore di distribuzione in seguito alla verifica del nome di dominio, il messaggio di errore è stato corretto per richiedere al cliente di contattare il proprio rappresentante Adobe.

