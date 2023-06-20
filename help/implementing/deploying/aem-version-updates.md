---
title: Aggiornamenti della versione di AEM
description: Scopri in che modo AEM as a Cloud Service utilizza Continuous Integration and Delivery (CI/CD) per mantenere i progetti sull’ultima versione.
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: bceec9ea6858b1c4c042ecd96f13ae5cac1bbee5
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 23%

---


# Aggiornamenti della versione di AEM {#aem-version-updates}

Scopri in che modo AEM as a Cloud Service utilizza Continuous Integration and Delivery (CI/CD) per mantenere i progetti sull’ultima versione.

## CI/CD {#ci-cd}

AEM as a Cloud Service utilizza l’integrazione continua e la distribuzione continua (CI/CD) per garantire che i tuoi progetti siano nella versione dell’AEM più recente. Ciò significa che le istanze di produzione e staging vengono aggiornate alla versione più recente di AEM senza alcuna interruzione del servizio per gli utenti.

Gli aggiornamenti delle versioni vengono applicati automaticamente solo alle istanze di produzione e staging. [Gli aggiornamenti AEM devono essere applicati manualmente a tutte le altre istanze.](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)

## Tipo di aggiornamenti {#update-types}

Esistono due tipi di aggiornamenti delle versioni di AEM:

* **Aggiornamenti di manutenzione di AEM**

   * Possono essere rilasciati su base giornaliera.
   * Vengono utilizzati principalmente a scopo di manutenzione, e possono contenere le correzioni di bug e gli aggiornamenti di sicurezza più recenti.
   * Dal momento che le modifiche vengono applicate su base regolare, hanno un impatto minimo.

* **Aggiornamenti con nuove funzioni**

   * Sono rilasciati su [programma mensile prevedibile.](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it)

## Errore di aggiornamento {#update-failure}

Gli aggiornamenti AEM passano attraverso una pipeline di convalida del prodotto intensa e completamente automatizzata che coinvolge più fasi, garantendo l&#39;assenza di interruzioni del servizio per tutti i sistemi in produzione. I controlli di integrità vengono utilizzati per monitorare lo stato dell&#39;applicazione. Se questi controlli non vanno a buon fine durante un aggiornamento as a Cloud Service dell’AEM, la versione non procede e l’Adobe indaga il motivo per cui l’aggiornamento ha causato questo comportamento imprevisto.

[test di prodotto e test funzionali del cliente,](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) che impediscono gli aggiornamenti del prodotto e gli push del codice del cliente da interrompere i sistemi di produzione, vengono convalidati anche durante un aggiornamento della versione AEM.

Se l’aggiornamento dell’ambiente di produzione non riesce, Cloud Manager ripristina automaticamente l’ambiente di staging. Questa operazione viene eseguita automaticamente per assicurarsi che al termine di un aggiornamento, entrambi gli ambienti di staging e di produzione utilizzino la stessa versione di AEM.

>[!NOTE]
>
>Se il codice personalizzato è stato inviato alla gestione temporanea e non alla produzione, il prossimo aggiornamento AEM rimuoverà tali modifiche per riflettere il tag Git dell’ultima versione del cliente alla produzione con esito positivo. Pertanto, il codice personalizzato disponibile solo nell’area di gestione temporanea dovrà essere nuovamente distribuito.

## Archivio nodi compositi {#composite-node-store}

Nella maggior parte dei casi, gli aggiornamenti non comportano tempi di inattività, incluso per l’istanza di authoring, che è un cluster di nodi. Gli aggiornamenti continui sono possibili a causa di [la funzione archivio nodi compositi in Oak.](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)

Questa funzione consente all’AEM di fare riferimento simultaneamente a più archivi. In un [distribuzione continua,](/help/implementing/deploying/overview.md#how-rolling-deployments-work) la nuova versione dell’AEM contiene `/libs` (l’archivio immutabile basato su TarMK), distinto dalla versione precedente dell’AEM, anche se entrambi fanno riferimento a un archivio mutabile basato su DocumentMK condiviso che contiene aree come `/content` , `/conf` , `/etc` e altri.

Poiché sia la vecchia che la nuova versione hanno la propria versione di `/libs`, possono essere entrambi attivi durante l’aggiornamento continuo e possono assumere il traffico fino a quando il vecchio non viene completamente sostituito dal nuovo.
