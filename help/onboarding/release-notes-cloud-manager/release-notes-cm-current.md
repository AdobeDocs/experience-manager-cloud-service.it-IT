---
title: Note sulla versione per Cloud Manager in AEM come versione di Cloud Service 2021.2.0
description: Note sulla versione per Cloud Manager in AEM come versione di Cloud Service 2021.2.0
translation-type: tm+mt
source-git-commit: d20a729712c1dbd48150f813419b57c49074b492
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 2%

---


# Note sulla versione per Cloud Manager in Adobe Experience Manager come Cloud Service 2021.2.0 {#release-notes}

In questa pagina sono delineate le Note sulla versione di Marketing Cloud Manager in AEM come Cloud Service 2021.2.0.

## Data di rilascio {#release-date}

La data di rilascio per Cloud Manager in AEM come Cloud Service 2021.2.0 è l’11 febbraio 2021.

## Cloud Manager {#cloud-manager}

### Novità {#what-is-new}

* La pipeline di produzione di Cloud Manager ora include funzionalità di test dell&#39;interfaccia utente personalizzata.

* I clienti delle risorse potranno ora scegliere quando e dove distribuire l’istanza del Portale marchio in modo self-service tramite l’interfaccia utente di Cloud Manager. Per un normale programma (non sandbox) con soluzione Assets, ora è possibile effettuare il provisioning di Brand Portal nell&#39;ambiente Production. Il provisioning può essere eseguito solo una volta nell&#39;ambiente di produzione.

* Il tipo di archivio AEM progetto utilizzato nella creazione di progetti e sandbox è stato aggiornato alla versione 25.

* L&#39;elenco delle API obsolete identificate durante la scansione del codice è stato ridefinito in modo da includere classi e metodi aggiuntivi obsoleti nelle versioni SDK dell&#39;Cloud Service più recente.

* Profilo SonarQube per Cloud Manager aggiornato per rimuovere Sonar rule squid:S2142. Ciò non entrerà più in conflitto con i controlli di Interruzione del thread.

* L&#39;interfaccia utente di Cloud Manager informa l&#39;utente che potrebbe non essere temporaneamente in grado di aggiungere/aggiornare il nome di dominio perché nell&#39;ambiente associato è collegata una pipeline in esecuzione o al momento in attesa del passaggio di approvazione.

* Le proprietà impostate nei file `pom.xml` del cliente con il prefisso Sonar verranno ora rimosse in modo dinamico per evitare errori di creazione e scansione di qualità.

* L&#39;interfaccia utente di Cloud Manager informa l&#39;utente che potrebbe non essere temporaneamente in grado di selezionare un certificato SSL se è in uso da un nome di dominio attualmente distribuito.


### Correzioni di bug {#bug-fixes}

* La corrispondenza del certificato SSL rispetto a un nome di dominio non fa più distinzione tra maiuscole e minuscole.

* L&#39;interfaccia utente di Cloud Manager ora informa un utente se le chiavi private del certificato non soddisfano il limite di 2048 bit con un messaggio di errore appropriato.

* L&#39;interfaccia utente di Cloud Manager informa l&#39;utente che potrebbe non essere temporaneamente in grado di selezionare un certificato SSL se è in uso da un nome di dominio attualmente distribuito.

* In alcuni casi, un problema interno potrebbe causare il blocco dell&#39;eliminazione dell&#39;ambiente.

* Alcuni guasti della pipeline sono stati erroneamente riportati come errori della pipeline.
