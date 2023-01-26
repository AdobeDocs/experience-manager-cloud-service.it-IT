---
title: Aggiornamenti della versione di AEM
description: Aggiornamenti della versione di AEM
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: c3e1559923699d300d78a71195bd5658c3323331
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 30%

---


# Aggiornamenti della versione di AEM {#aem-version-updates}

## Introduzione {#introduction}

AEM as a Cloud Service ora utilizza un approccio CI/CD (Continuous Integration/Continuous Delivery, integrazione continua e distribuzione continua), affinché tu possa lavorare sempre sui tuoi progetti con la versione più recente di AEM. Ciò significa che le istanze di produzione e di staging vengono aggiornate alla versione più recente AEM senza alcuna interruzione del servizio per gli utenti.

>[!NOTE]
>
>Se l’aggiornamento dell’ambiente di produzione non riesce, Cloud Manager ripristina automaticamente l’ambiente di staging. Questa operazione viene eseguita automaticamente per assicurarsi che al termine di un aggiornamento, entrambi gli ambienti di staging e di produzione utilizzino la stessa versione di AEM.

Esistono due tipi di aggiornamenti delle versioni di AEM:

* **Aggiornamenti di manutenzione di AEM**

   * Possono essere rilasciati su base giornaliera.
   * Vengono utilizzati principalmente a scopo di manutenzione, e possono contenere le correzioni di bug e gli aggiornamenti di sicurezza più recenti.
   * Dal momento che le modifiche vengono applicate su base regolare, hanno un impatto minimo.

* **Aggiornamenti con nuove funzioni**

   * Vengono rilasciati in base a una pianificazione mensile prevedibile.

Gli aggiornamenti AEM passano attraverso una pipeline di convalida del prodotto intensa e completamente automatizzata, che prevede più fasi, senza interrompere il servizio per tutti i sistemi in produzione. I controlli sanitari sono utilizzati per monitorare lo stato di salute della domanda. Se questi controlli non riescono durante un aggiornamento AEM as a Cloud Service, il rilascio non procederà e l’Adobe esaminerà il motivo per cui l’aggiornamento ha causato questo comportamento imprevisto.

[test dei prodotti e test funzionali dei clienti,](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) che impediscono l&#39;interruzione dei sistemi di produzione da parte degli aggiornamenti dei prodotti e del codice cliente, vengono convalidati anche durante un aggiornamento della versione AEM.

>[!NOTE]
>
>Se il codice personalizzato è stato inviato allo staging e non alla produzione, il successivo aggiornamento AEM rimuoverà tali modifiche per riflettere il tag git dell’ultima versione del cliente riuscita in produzione. Pertanto, il codice personalizzato disponibile solo in fase di staging dovrà essere nuovamente distribuito.

## Archiviazione dei nodi compositi {#composite-node-store}

Nella maggior parte dei casi, gli aggiornamenti non genereranno tempi di inattività, anche per l’istanza di authoring, che è un cluster di nodi. Aggiornamenti continui sono possibili a causa della funzionalità di archiviazione dei nodi compositi in Oak.

Questa funzione consente AEM fare riferimento contemporaneamente a più archivi. In una distribuzione continua, la nuova versione di AEM verde contiene la propria `/libs` (archivio immutabile basato su TarMK), diverso dalla vecchia versione di AEM blu, anche se entrambi fanno riferimento a un archivio mutabile basato su DocumentMK condiviso che contiene aree come `/content` , `/conf` , `/etc` e altri. Perché sia il blu che il verde hanno le loro versioni di `/libs`, possono essere entrambi attivi durante l’aggiornamento continuo, sia assumendo traffico fino a quando il blu non viene completamente sostituito dal verde.
