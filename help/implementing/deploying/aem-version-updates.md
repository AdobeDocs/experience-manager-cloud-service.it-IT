---
title: Aggiornamenti della versione di AEM
description: Scopri in che modo AEM as a Cloud Service utilizza Continuous Integration and Delivery (CI/CD) per mantenere i progetti sull’ultima versione.
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: dd567c484d71e25de1808f784c455cfb9b124fbf
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 11%

---


# Aggiornamenti della versione di AEM {#aem-version-updates}

Scopri in che modo AEM as a Cloud Service utilizza Continuous Integration and Delivery (CI/CD) per mantenere i progetti sull’ultima versione.

## CI/CD {#ci-cd}

AEM as a Cloud Service utilizza l’integrazione continua e la distribuzione continua (CI/CD) per garantire che i tuoi progetti siano nella versione dell’AEM più recente. Questo processo aggiorna facilmente le istanze di produzione, staging e sviluppo senza causare interruzioni agli utenti.

Prima che le istanze vengano aggiornate automaticamente, viene pubblicata una nuova versione di manutenzione dell’AEM con 3-5 giorni di anticipo. Durante questo periodo, puoi scegliere di:
[attivare gli aggiornamenti manuali per le istanze di sviluppo](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment).
Trascorso questo periodo di tempo, gli aggiornamenti delle versioni vengono applicati automaticamente agli ambienti di sviluppo. Se l’aggiornamento ha esito positivo, il processo di aggiornamento procede alle istanze di staging e produzione. Le istanze di sviluppo e staging fungono da gate di qualità automatizzato, in cui i test scritti personalizzati vengono eseguiti prima dell’applicazione dell’aggiornamento all’ambiente di produzione.

>[!NOTE]
>
> Nota: gli aggiornamenti automatici per gli ambienti di sviluppo verranno progressivamente abilitati nel 2023 per tutti i clienti. Se gli ambienti di sviluppo non vengono aggiornati automaticamente, puoi utilizzare gli aggiornamenti manuali per mantenerli sincronizzati con gli ambienti di staging e produzione.


## Tipo di aggiornamenti {#update-types}

Esistono due tipi di aggiornamenti delle versioni di AEM:

* **Aggiornamenti di manutenzione di AEM**

   * Possono essere rilasciati su base giornaliera.
   * Vengono utilizzati principalmente a scopo di manutenzione, e possono contenere le correzioni di bug e gli aggiornamenti di sicurezza più recenti.
   * Dal momento che le modifiche vengono applicate su base regolare, hanno un impatto minimo.

* **Aggiornamenti con nuove funzioni**

   * Sono rilasciati su [programma mensile prevedibile.](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it)

## Errore di aggiornamento {#update-failure}

Gli aggiornamenti AEM passano attraverso una pipeline di convalida del prodotto intensa e completamente automatizzata che coinvolge più fasi, garantendo l&#39;assenza di interruzioni del servizio per tutti i sistemi in produzione.
I controlli di integrità vengono utilizzati per monitorare lo stato dell&#39;applicazione.
Se questi controlli non vanno a buon fine durante un aggiornamento as a Cloud Service dell’AEM, la versione non procede e Adobe indaga il motivo per cui l’aggiornamento ha causato questo comportamento imprevisto.

Quando distribuisci una nuova versione di un codice personalizzato di nei tuoi ambienti,
[Test funzionali del prodotto e personalizzati](/help/implementing/cloud-manager/overview-test-results.md#functional-testing)
svolgere un ruolo cruciale nel garantire che i sistemi di produzione rimangano stabili e funzionanti anche dopo l&#39;applicazione di un cambiamento. Questi test vengono utilizzati anche nel processo di aggiornamento della versione AEM.

Se l’aggiornamento dell’ambiente di produzione non riesce, Cloud Manager ripristina automaticamente l’ambiente di staging. Questa operazione viene eseguita automaticamente per assicurarsi che al termine di un aggiornamento, entrambi gli ambienti di staging e produzione utilizzino la stessa versione dell’AEM.
Analogamente, se un aggiornamento automatico di un ambiente di sviluppo non riesce, gli ambienti di staging e produzione non verranno aggiornati.

>[!NOTE]
>
>Se il codice personalizzato è stato inviato alla gestione temporanea e non alla produzione, il prossimo aggiornamento AEM rimuoverà tali modifiche per riflettere il tag Git dell’ultima versione del cliente alla produzione con esito positivo. Pertanto, il codice personalizzato disponibile solo nell’area di gestione temporanea dovrà essere nuovamente distribuito.

## Archivio nodi compositi {#composite-node-store}

Nella maggior parte dei casi, gli aggiornamenti non comportano tempi di inattività, incluso per l’istanza di authoring, che è un cluster di nodi. Gli aggiornamenti continui sono possibili a causa di [la funzione archivio nodi compositi in Oak.](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)

Questa funzione consente all’AEM di fare riferimento simultaneamente a più archivi. In un [distribuzione continua,](/help/implementing/deploying/overview.md#how-rolling-deployments-work) la nuova versione dell’AEM contiene `/libs` (l’archivio immutabile basato su TarMK), distinto dalla versione precedente dell’AEM, anche se entrambi fanno riferimento a un archivio mutabile basato su DocumentMK condiviso che contiene aree come `/content` , `/conf` , `/etc` e altri.

Poiché sia la vecchia che la nuova versione hanno la propria versione di `/libs`, possono essere entrambi attivi durante l’aggiornamento continuo e possono assumere il traffico fino a quando il vecchio non viene completamente sostituito dal nuovo.
