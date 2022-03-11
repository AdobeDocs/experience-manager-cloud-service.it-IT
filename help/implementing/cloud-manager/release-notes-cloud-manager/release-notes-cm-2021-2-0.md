---
title: Note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2021.2.0
description: Note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2021.2.0
exl-id: 281f9523-dec2-44f1-9459-5a45d48489d9
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 2%

---

# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2021.2.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.2.0.

## Data di pubblicazione {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.2.0 è l’11 febbraio 2021.

## Cloud Manager {#cloud-manager}

### Novità {#what-is-new}

* I clienti di Assets ora potranno scegliere quando e dove implementare la propria istanza Brand Portal in modalità self-service tramite l’interfaccia utente di Cloud Manager. Per un programma normale (non sandbox) con soluzione Assets, ora è possibile eseguire il provisioning di Brand Portal nell’ambiente Produzione. Il provisioning può essere eseguito una sola volta nell’ambiente di produzione.

* L’Archetipo di progetto AEM utilizzato nella creazione di progetti e sandbox è stato aggiornato alla versione 25.

* L’elenco delle API obsolete identificate durante la scansione del codice è stato perfezionato per includere classi e metodi aggiuntivi obsoleti nelle ultime versioni dell’SDK di Cloud Service.

* Profilo SonarQube per Cloud Manager aggiornato per rimuovere Sonar rule squid:S2142. Questo non entrerà più in conflitto con i controlli di interruzione del thread.

* L’interfaccia utente di Cloud Manager informa l’utente che potrebbe non essere temporaneamente in grado di aggiungere/aggiornare il nome di dominio perché all’ambiente associato è collegata una pipeline in esecuzione o attualmente in attesa del passaggio di approvazione.

* Proprietà impostate nel cliente `pom.xml` i file con prefisso sonar vengono ora rimossi dinamicamente per evitare errori di creazione e di scansione della qualità.

* L’interfaccia utente di Cloud Manager informa l’utente che potrebbe non essere temporaneamente in grado di selezionare un certificato SSL se è utilizzato da un nome di dominio attualmente distribuito.

* Sono state aggiunte regole aggiuntive per la qualità del codice per risolvere i problemi relativi alla compatibilità dei Cloud Service.

### Correzioni di bug  {#bug-fixes}

* La corrispondenza del certificato SSL rispetto a un nome di dominio non fa più distinzione tra maiuscole e minuscole.

* L’interfaccia utente di Cloud Manager ora informa un utente se le chiavi private del certificato non soddisfano il limite di 2048 bit con un messaggio di errore appropriato.

* L’interfaccia utente di Cloud Manager informa l’utente che potrebbe non essere temporaneamente in grado di selezionare un certificato SSL se è utilizzato da un nome di dominio attualmente distribuito.

* In alcuni casi, un problema interno può causare il blocco dell’eliminazione dell’ambiente.

* Alcuni errori di pipeline non sono stati segnalati correttamente come errori di pipeline.
