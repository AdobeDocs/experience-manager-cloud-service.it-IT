---
title: Aggiornamenti della versione di AEM
description: Aggiornamenti della versione di AEM
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 575be022704e998e63162f19c37ece877efef627
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 4%

---


# Aggiornamenti della versione di AEM {#aem-version-updates}

## Introduzione {#introduction}

AEM as a Cloud Service ora utilizza l’integrazione continua e la distribuzione continua (CI/CD) per garantire che i progetti siano nella versione di AEM più recente. Ciò significa che le istanze di produzione e staging vengono aggiornate alla versione più recente AEM senza alcuna interruzione del servizio per gli utenti.

>[!NOTE]
>
>Se l’aggiornamento all’ambiente di produzione non riesce, Cloud Manager ripristina automaticamente l’ambiente di staging. Questa operazione viene eseguita automaticamente per assicurarsi che al termine di un aggiornamento, sia gli ambienti di staging che quelli di produzione si trovino nella stessa versione AEM.

Esistono due tipi di aggiornamenti delle versioni AEM:

* **Aggiornamenti alla manutenzione AEM**

   * Possono essere rilasciati su base giornaliera.
   * Sono principalmente a scopo di manutenzione, incluse le ultime correzioni di bug e gli aggiornamenti di sicurezza.
   * Hanno un impatto minimo poiché le modifiche vengono applicate regolarmente.

* **Nuovi aggiornamenti delle funzioni**

   * Vengono rilasciati tramite un programma mensile prevedibile.

Gli aggiornamenti AEM passano attraverso una pipeline di convalida del prodotto intensa e completamente automatizzata, che prevede più fasi, senza interrompere il servizio per tutti i sistemi in produzione. I controlli sanitari sono utilizzati per monitorare lo stato di salute della domanda. Se questi controlli non riescono durante un aggiornamento AEM as a Cloud Service, il rilascio non procederà e l’Adobe esaminerà il motivo per cui l’aggiornamento ha causato questo comportamento imprevisto.

[test dei prodotti e test funzionali dei clienti,](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) che impediscono l&#39;interruzione dei sistemi di produzione da parte degli aggiornamenti dei prodotti e del codice cliente, vengono convalidati anche durante un aggiornamento della versione AEM.

>[!NOTE]
>
>Se il codice personalizzato è stato inviato alla gestione temporanea e successivamente rifiutato da te, il successivo aggiornamento AEM rimuoverà tali modifiche per riflettere il tag git dell’ultima versione del cliente riuscita in produzione.

## Archiviazione dei nodi compositi {#composite-node-store}

Nella maggior parte dei casi, gli aggiornamenti non genereranno tempi di inattività, anche per l’istanza di authoring, che è un cluster di nodi. Aggiornamenti continui sono possibili a causa della funzionalità di archiviazione dei nodi compositi in Oak.

Questa funzione consente AEM fare riferimento contemporaneamente a più archivi. In una distribuzione continua, la nuova versione di AEM verde contiene la propria `/libs` (archivio immutabile basato su TarMK), diverso dalla vecchia versione di AEM blu, anche se entrambi fanno riferimento a un archivio mutabile basato su DocumentMK condiviso che contiene aree come `/content` , `/conf` , `/etc` e altri. Perché sia il blu che il verde hanno le loro versioni di `/libs`, possono essere entrambi attivi durante l’aggiornamento continuo, sia assumendo traffico fino a quando il blu non viene completamente sostituito dal verde.
