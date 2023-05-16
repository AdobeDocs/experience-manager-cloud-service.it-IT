---
title: Aggiornamenti della versione di AEM
description: Scopri come AEM as a Cloud Service utilizza l’integrazione continua e la consegna (CI/CD) per mantenere i progetti sulla versione più recente.
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 59bc2b5af22ef23775195f098517cec40d98d66b
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 23%

---


# Aggiornamenti della versione di AEM {#aem-version-updates}

Scopri come AEM as a Cloud Service utilizza l’integrazione continua e la consegna (CI/CD) per mantenere i progetti sulla versione più recente.

## CI/CD {#ci-cd}

AEM as a Cloud Service utilizza l’integrazione continua e la distribuzione continua (CI/CD) per garantire che i progetti siano nella versione di AEM più recente. Ciò significa che le istanze di produzione e staging vengono aggiornate alla versione più recente di AEM senza alcuna interruzione del servizio per gli utenti.

Gli aggiornamenti di versione vengono applicati automaticamente solo alle istanze di produzione e di staging. [AEM aggiornamenti devono essere applicati manualmente a tutte le altre istanze.](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)

## Tipo di aggiornamenti {#update-types}

Esistono due tipi di aggiornamenti delle versioni di AEM:

* **Aggiornamenti di manutenzione di AEM**

   * Possono essere rilasciati su base giornaliera.
   * Vengono utilizzati principalmente a scopo di manutenzione, e possono contenere le correzioni di bug e gli aggiornamenti di sicurezza più recenti.
   * Dal momento che le modifiche vengono applicate su base regolare, hanno un impatto minimo.

* **Aggiornamenti con nuove funzioni**

   * Sono rilasciate su un [programma mensile prevedibile.](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it)

## Errore di aggiornamento {#update-failure}

Gli aggiornamenti AEM passano attraverso una pipeline di convalida del prodotto intensa e completamente automatizzata, che prevede più fasi, senza interrompere il servizio per tutti i sistemi in produzione. I controlli sanitari sono utilizzati per monitorare lo stato di salute della domanda. Se questi controlli non riescono durante un aggiornamento AEM as a Cloud Service, il rilascio non procederà e l’Adobe esaminerà il motivo per cui l’aggiornamento ha causato questo comportamento imprevisto.

[test dei prodotti e test funzionali dei clienti,](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) che impediscono l&#39;interruzione dei sistemi di produzione da parte degli aggiornamenti dei prodotti e del codice cliente, vengono convalidati anche durante un aggiornamento della versione AEM.

Se l’aggiornamento dell’ambiente di produzione non riesce, Cloud Manager ripristina automaticamente l’ambiente di staging. Questa operazione viene eseguita automaticamente per assicurarsi che al termine di un aggiornamento, entrambi gli ambienti di staging e di produzione utilizzino la stessa versione di AEM.

>[!NOTE]
>
>Se il codice personalizzato è stato inviato allo staging e non alla produzione, il successivo aggiornamento AEM rimuoverà tali modifiche per riflettere il tag git dell’ultima versione del cliente riuscita in produzione. Pertanto, il codice personalizzato disponibile solo in fase di staging dovrà essere nuovamente distribuito.

## Archiviazione dei nodi compositi {#composite-node-store}

Nella maggior parte dei casi, gli aggiornamenti non genereranno tempi di inattività, anche per l’istanza di authoring, che è un cluster di nodi. Gli aggiornamenti continui sono possibili a causa di [la funzione di archiviazione dei nodi compositi in Oak.](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)

Questa funzione consente AEM fare riferimento contemporaneamente a più archivi. In caso di rotolamento [distribuzione blu-verde,](/help/implementing/deploying/overview.md#index-management-using-blue-green-deployments) la nuova versione AEM verde contiene la propria `/libs` (archivio immutabile basato su TarMK), diverso dalla vecchia versione di AEM blu, anche se entrambi fanno riferimento a un archivio mutabile basato su DocumentMK condiviso che contiene aree come `/content` , `/conf` , `/etc` e altri.

Perché sia il blu che il verde hanno le loro versioni di `/libs`, possono essere entrambi attivi durante l’aggiornamento continuo, sia assumendo traffico fino a quando il blu non viene completamente sostituito dal verde.
