---
title: Attiva l’interruttore delle funzioni per integrare le funzioni di adozione anticipata e prerelease
description: L’attivazione delle funzioni è una funzionalità di AEM che consente agli amministratori di abilitare le nuove funzioni in un ambiente di runtime.
feature: Adaptive Forms, Foundation Components, Core Components
role: User, Developer
exl-id: 3ad1370a-a399-4fbe-8168-c3a1cee06336
source-git-commit: c1d62f0dd5a25da7fbeef537e1c28fa8421f42cd
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 5%

---

# Abilitare attivazione/disattivazione funzioni in Adobe Experience Software Development Kit (AEM SDK)

In AEM, l’attivazione delle funzioni consente agli amministratori di abilitare o disabilitare le funzioni in fase di esecuzione, ideale per la gestione delle funzioni di adozione anticipata e prerelease senza modifiche al codice. Supporta i rollout graduali, il test A/B e la rapida disattivazione delle funzioni instabili.

In questo articolo viene illustrato come abilitare l’attivazione delle funzioni di attivazione/disattivazione nella configurazione SDK locale di AEM, che simula AEM as a Cloud Service utilizzando SDK e Dispatcher. Questa configurazione consente ai team di eseguire i test in un ambiente di produzione prima di distribuirli nel cloud.

## Perché utilizzare gli interruttori delle funzioni in una configurazione di AEM SDK?

Quando si lavora in una configurazione di AEM SDK, la funzione attiva la guida in:

* Verifica sicura delle caratteristiche sperimentali.

* Rollout di nuovi componenti in fasi.

* Mantenimento di un&#39;unica base di codice in più ambienti.

* Riduzione dei rischi durante le installazioni e gli aggiornamenti.

## Prerequisiti

Prima di abilitare l’attivazione delle funzioni nella configurazione di AEM SDK, assicurati di quanto segue:

* Utente membro del gruppo `forms-users`.

* Passa a `http://<author-instance-url>:portnumber/system/console/bundles` e controlla se il bundle **(com.adobe.granite.toggle.impl.dev-1.1.2.jar)** è presente o meno. Se non è presente, [scarica il bundle dal collegamento](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]s/cq650/hotfix/com.adobe.granite.toggle.impl.dev-1.1.8.jar).

  ![Attiva/Disattiva funzionalità](/help/forms/assets/aem-web-console-bundle.png)

### Abilitare il pulsante di attivazione/disattivazione della funzione

Per abilitare le opzioni nella tua istanza di AEM SDK, segui la procedura riportata di seguito:

1. Accedi all’istanza di AEM Forms.

1. Accedi a `http://author-instance-url:portnumber/system/console/configMgr`.

1. Cerca Adobe Granite Dynamic Toggle Provider in Configuration Manager.

   ![Attiva/Disattiva funzionalità](/help/forms/assets/aem-web-console-confi.png)

1. Fare clic sull&#39;icona ✏️.
1. Nella sezione Attivazione/disattivazione fare clic su➕.
1. Aggiungi l’ID di attivazione/disattivazione della funzione, come illustrato nell’immagine seguente.
   ![Attiva/Disattiva funzionalità](/help/forms/assets/feature-toggle.png)

1. Fai clic su Salva

>[!NOTE]
>
> L’ID di attivazione/disattivazione della funzione è disponibile nel documento specifico per le funzioni utilizzate in precedenza.


### Disabilita attivazione funzionalità

Per disattivare l&#39;attivazione/disattivazione delle funzionalità per le funzionalità attivate, procedere come segue:

1. Accedi all’istanza di AEM Forms.
1. Accedi a `http://author-instance-url:portnumber/system/console/configMgr`.
1. Cerca Adobe Granite Dynamic Toggle Provider in Configuration Manager.
1. Fare clic sull&#39;icona ✏️.
1. Nella sezione Attivazione/disattivazione fare clic su ➕.
1. Aggiungi il numero di attivazione/disattivazione della funzione.

   ![Attiva/Disattiva funzionalità](/help/forms/assets/disable-toggle-feature.png)

### Considerazioni tecniche

Gli interruttori delle funzioni sono gestiti in fase di esecuzione e sono più adatti per le impostazioni di sviluppo o test. In una configurazione di AEM SDK, accertati che gli interruttori siano controllati in base alla versione e sincronizzati con CI/CD. Affinché le modifiche vengano applicate, potrebbe essere necessario aggiornare la pagina o cancellare la cache.

>[!NOTE]
>
> Per abilitare l’attivazione/disattivazione della funzione per l’ambiente di produzione, contatta il team di supporto Adobe.
