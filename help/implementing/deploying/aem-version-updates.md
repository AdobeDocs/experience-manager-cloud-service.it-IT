---
title: Aggiornamenti della versione di AEM
description: 'Aggiornamenti della versione di AEM '
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 36%

---

# Aggiornamenti della versione di AEM {#aem-version-updates}

## Introduzione {#introduction}

AEM as a Cloud Service ora utilizza l’integrazione continua e la distribuzione continua (CI/CD) per garantire che i progetti siano nella versione di AEM più recente. Ciò significa che le istanze Production e Stage vengono aggiornate alla versione più recente di AEM senza alcuna interruzione del servizio per gli utenti.

>[!NOTE]
>Se l’aggiornamento dell’ambiente di produzione non riesce, Cloud Manager ripristina automaticamente l’ambiente di stage. Questa operazione viene eseguita automaticamente per assicurarsi che al termine di un aggiornamento, sia gli ambienti di stage che di produzione si trovino nella stessa versione AEM.

Gli aggiornamenti delle versioni di AEM sono di due tipi:

* **Aggiornamenti push di AEM**

   * Possono essere rilasciati su base giornaliera.

   * Prevalentemente manutenzione, incluse le ultime correzioni di bug e gli aggiornamenti di sicurezza.

      Con l’applicazione regolare delle modifiche, l’impatto è incrementale e influisce meno sul servizio.

* **Nuovi aggiornamenti delle funzioni**

   * Rilasciati tramite un programma mensile prevedibile.

Gli aggiornamenti AEM passano attraverso una pipeline di convalida del prodotto intensa e completamente automatizzata, che prevede più passaggi per garantire l&#39;assenza di interruzioni del servizio per tutti i sistemi in produzione. I controlli sanitari sono utilizzati per monitorare lo stato di salute della domanda. Se questi controlli non riescono durante un aggiornamento AEM as a Cloud Service, il rilascio non procederà e l’Adobe esaminerà il motivo per cui l’aggiornamento ha causato questo comportamento imprevisto.

[Test del prodotto e test funzionali del cliente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/understand-test-results.html#functional-testing) che impediscono l’interruzione della produzione da parte degli aggiornamenti dei prodotti e del codice cliente, vengono convalidati anche durante un aggiornamento della versione AEM.

>[!NOTE]
>
>Se il codice personalizzato è stato inviato alla gestione temporanea e successivamente rifiutato da te, il successivo aggiornamento AEM rimuoverà tali modifiche per riflettere il tag git dell’ultima versione del cliente riuscita in produzione.

## Archiviazione dei nodi compositi {#composite-node-store}

Come accennato in precedenza, gli aggiornamenti nella maggior parte dei casi non genereranno tempi di inattività, incluso per l’autore, che è un cluster di nodi. Gli aggiornamenti continui sono possibili a causa *archivio a nodi compositi* in Oak.

Questa funzione consente AEM fare riferimento contemporaneamente a più archivi. In una distribuzione continua, la nuova versione di Green AEM contiene la propria `/libs` (archivio immutabile basato su TarMK), diverso dalla vecchia versione Blue AEM, anche se entrambi fanno riferimento a un archivio mutabile basato su DocumentMK condiviso che contiene aree come `/content` , `/conf` , `/etc` e altri. Perché sia il blu che il verde hanno le loro versioni di `/libs`, possono essere entrambi attivi durante l’aggiornamento continuo, sia assumendo traffico fino a quando il blu non viene completamente sostituito dal verde.
