---
title: Aggiornamenti AEM versione
description: 'Aggiornamenti AEM versione '
translation-type: tm+mt
source-git-commit: 78c0802a0703e81941013347a3f4b57cb106c927
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# AEM aggiornamenti della versione {#aem-version-updates}

## Introduzione {#introduction}

AEM come Cloud Service utilizza ora l&#39;integrazione continua e la fornitura continua (CI/CD) per garantire che i progetti siano nella versione AEM più recente. Ciò significa che le istanze Produzione e Stage vengono aggiornate alla versione più recente AEM senza alcuna interruzione del servizio per gli utenti.

>[!NOTE]
>Se l&#39;aggiornamento all&#39;ambiente di produzione non riesce, Cloud Manager ripristina automaticamente l&#39;ambiente dell&#39;area di visualizzazione. Questa operazione viene eseguita automaticamente per essere certi che, al termine di un aggiornamento, sia gli ambienti di fase che quelli di produzione siano sulla stessa versione AEM.

AEM aggiornamenti delle versioni sono di due tipi:

* **Aggiornamenti AEM push**

   * Può essere rilasciato su base giornaliera.

   * La maggior parte delle attività di manutenzione, incluse le correzioni di bug più recenti e gli aggiornamenti della sicurezza.

      Poiché le modifiche vengono applicate regolarmente, l&#39;impatto è incrementale, riducendo l&#39;impatto sul servizio.

* **Aggiornamenti delle nuove funzioni**

   * Rilasciato tramite un programma mensile prevedibile.

AEM aggiornamenti passano attraverso un ciclo di convalida del prodotto intenso e completamente automatizzato, che prevede più passaggi per garantire l&#39;assenza di interruzioni del servizio per i sistemi in produzione. I controlli sanitari sono utilizzati per monitorare lo stato della domanda. Se questi controlli non vengono eseguiti durante un AEM come aggiornamento del Cloud Service, il rilascio non verrà completato e  Adobe verificherà perché l&#39;aggiornamento ha causato questo comportamento imprevisto.

[I test di prodotto e ](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/understand-test-results.html#functional-testing) i test funzionali dei clienti che impediscono agli aggiornamenti dei prodotti e ai suggerimenti sul codice cliente di interrompere la produzione vengono convalidati anche durante un aggiornamento AEM versione.

>[!NOTE]
>
>Se il codice personalizzato è stato messo in staging e successivamente rifiutato dall&#39;utente, il successivo aggiornamento AEM rimuoverà tali modifiche per riflettere il tag git dell&#39;ultima release cliente riuscita alla produzione.

## Archivio nodi compositi {#composite-node-store}

Come già detto, gli aggiornamenti nella maggior parte dei casi non generano tempi di inattività, anche per l&#39;autore, che è un cluster di nodi. Gli aggiornamenti a rotolamento sono possibili grazie alla funzionalità *composito node store* in Oak.

Questa funzione consente AEM fare riferimento a più repository contemporaneamente. In una distribuzione continua, la nuova versione di AEM verde contiene il proprio `/libs` (repository immutabile basato su TarMK), distinto dalla versione precedente di AEM blu, anche se entrambi fanno riferimento a un repository mutabile basato su DocumentMK condiviso che contiene aree come `/content`, `/conf`, `/etc` e altre. Poiché sia il blu che il verde hanno versioni proprie di `/libs`, entrambi possono essere attivi durante l&#39;aggiornamento continuo, assumendo entrambi il traffico fino a quando il blu non viene completamente sostituito dal verde.

