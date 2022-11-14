---
title: Note sulla versione 2021.10.0 di Cloud Manager in AEM as a Cloud Service
description: Note sulla versione 2021.10.0 di Cloud Manager in AEM as a Cloud Service
feature: Release Information
exl-id: f8a87b00-52ce-42a6-a955-45cb14703b40
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 100%

---

# Note sulla versione 2021.10.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2021.10.0 di Cloud Manager in AEM as a Cloud Service.

>[!NOTE]
>Per visualizzare le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, fai clic [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=it).

## Data di pubblicazione {#release-date}

La data di pubblicazione di Cloud Manager in AEM as a Cloud Service 2021.10.0 è il 14 ottobre 2021.


### Novità {#what-is-new}

* Per prepararci ad alcune modifiche imminenti, ora le pipeline di distribuzione esistenti verranno indicate ed etichettate nell’interfaccia utente come pipeline **full stack**.

* Ora la scheda Pipeline è stata aggiornata per visualizzare una singola pagina integrata che mostra entrambe le pipeline di produzione e non di produzione. L’utente può selezionare Esegui/Pausa/Riprendi direttamente dal menu Azioni associato a ogni pipeline.

* Ora l’utente con il ruolo Responsabile dell’implementazione può eliminare la pipeline di produzione tramite l’interfaccia utente in modo autonomo.

* Le esperienze di aggiunta e modifica delle pipeline sono state aggiornate per poter utilizzare finestre modali moderne e intuitive.

* Ora gli utenti di Cloud Manager possono inviare feedback direttamente dall’interfaccia utente, tramite il pulsante **Feedback** posizionato nella parte in alto a destra della pagina di destinazione.

* Ora è possibile scaricare i grafici SLA annuali dall’interfaccia utente di Cloud Manager.

* Ora le esecuzioni delle pipeline di qualità del codice e non di produzione utilizzano un processo di clonazione superficiale durante la fase di build, garantendo tempi di generazione più brevi ai clienti con archivi Git di dimensioni particolarmente grandi.

* Ora la procedura guidata Aggiungi elenco IP consentiti informa l’utente se è stato raggiunto il numero massimo di elenchi IP consentiti.

* Ora la documentazione API di Cloud Manager include un ambiente playground interattivo che consente agli utenti connessi di sperimentare l’API dal browser in uso. Per ulteriori informazioni, consulta [Ambiente playground dell’API di Cloud Manager](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/).

* Il suggerimento della scheda Programma presenta una descrizione più dettagliata se è disattivata l’opzione di selezione sotto “Accedi a”. Ora viene visualizzato “Non esiste un ambiente di produzione”.

### Correzioni di bug {#bug-fixes}

* In rare situazioni, quando il personale Adobe ripristinava l’ambiente del cliente, il ripristino veniva considerato completo prima che l’ambiente fosse completamente operativo.

* Per alcune richieste interne effettuate durante la creazione dell’ambiente non veniva effettuato un secondo tentativo.

* In caso di errori della distribuzione rilevati successivamente alla verifica del nome di dominio, il messaggio di errore è stato corretto per suggerire all’utente di contattare il rappresentante Adobe.
