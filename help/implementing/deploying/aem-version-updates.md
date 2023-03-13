---
title: Aggiornamenti della versione di AEM
description: Aggiornamenti della versione di AEM
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: f977c6d8fa3ebd4b082e48da8b248178f9a2f34b
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 30%

---


# Aggiornamenti della versione di AEM {#aem-version-updates}

## Introduzione {#introduction}

AEM as a Cloud Service ora utilizza un approccio CI/CD (Continuous Integration/Continuous Delivery, integrazione continua e distribuzione continua), affinché tu possa lavorare sempre sui tuoi progetti con la versione più recente di AEM. Ciò significa che le istanze di produzione e staging vengono aggiornate alla versione più recente dell’AEM senza alcuna interruzione del servizio per gli utenti.

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

Gli aggiornamenti AEM passano attraverso una pipeline di convalida del prodotto intensa e completamente automatizzata che coinvolge più fasi, garantendo l&#39;assenza di interruzioni del servizio per tutti i sistemi in produzione. I controlli di integrità vengono utilizzati per monitorare lo stato dell&#39;applicazione. Se questi controlli non vanno a buon fine durante un aggiornamento as a Cloud Service dell’AEM, la versione non procede e l’Adobe indaga il motivo per cui l’aggiornamento ha causato questo comportamento imprevisto.

[test di prodotto e test funzionali del cliente,](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) che impediscono gli aggiornamenti del prodotto e gli push del codice del cliente da interrompere i sistemi di produzione, vengono convalidati anche durante un aggiornamento della versione AEM.

>[!NOTE]
>
>Se il codice personalizzato è stato inviato alla gestione temporanea e non alla produzione, il prossimo aggiornamento AEM rimuoverà tali modifiche per riflettere il tag Git dell’ultima versione del cliente alla produzione con esito positivo. Pertanto, il codice personalizzato disponibile solo nell’area di gestione temporanea dovrà essere nuovamente distribuito.

## Archivio nodi compositi {#composite-node-store}

Nella maggior parte dei casi, gli aggiornamenti non comportano tempi di inattività, incluso per l’istanza di authoring, che è un cluster di nodi. Gli aggiornamenti continui sono possibili a causa della funzione di archivio nodi composito in Oak.

Questa funzione consente all’AEM di fare riferimento simultaneamente a più archivi. In una distribuzione continua, la nuova versione verde dell’AEM contiene la propria `/libs` (l’archivio immutabile basato su TarMK), diverso dalla versione blu precedente dell’AEM, anche se entrambi fanno riferimento a un archivio mutabile basato su DocumentMK condiviso che contiene aree come `/content` , `/conf` , `/etc` e altri. Perché sia il blu che il verde hanno le loro versioni di `/libs`, possono essere entrambi attivi durante l’aggiornamento continuo, entrambi assumono il traffico fino a quando il blu non viene completamente sostituito dal verde.
