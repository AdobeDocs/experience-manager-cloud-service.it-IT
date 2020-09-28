---
title: Aggiornamenti AEM versione
description: 'Aggiornamenti AEM versione '
translation-type: tm+mt
source-git-commit: ca37f00926fc110b865e6db2e61ff1198519010b
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---


# Aggiornamenti AEM versione {#aem-version-updates}

## Introduzione {#introduction}

AEM come Cloud Service utilizza ora l&#39;integrazione continua e la fornitura continua (CI/CD) per garantire che i progetti siano nella versione AEM più recente. Ciò significa che tutte le operazioni di aggiornamento sono completamente automatizzate, pertanto non è necessaria alcuna interruzione del servizio per gli utenti.

>[!NOTE]
>Se l&#39;aggiornamento all&#39;ambiente di produzione non riesce, Cloud Manager ripristina automaticamente l&#39;ambiente dell&#39;area di visualizzazione. Questa operazione viene eseguita automaticamente per essere certi che, al termine di un aggiornamento, sia gli ambienti di fase che quelli di produzione siano sulla stessa versione AEM.

AEM aggiornamenti delle versioni sono di due tipi:

* **Aggiornamenti push**

   * Può essere rilasciato su base giornaliera.
   * La maggior parte delle attività di manutenzione, incluse le correzioni di bug più recenti e gli aggiornamenti della sicurezza.

   Poiché le modifiche vengono applicate regolarmente, l&#39;impatto è incrementale, riducendo l&#39;impatto sul servizio.

>[!NOTE]
>Per ulteriori informazioni AEM aggiornamenti push, consulta il white paper su [Adobe Experience Manager come modello di distribuzione continua Cloud Service](https://fieldreadiness-adobe.highspot.com/items/5ea322e1c714336c23b32599#2)

* **Aggiornamenti delle nuove funzioni**

   * Rilasciato tramite un programma mensile prevedibile.

AEM aggiornamenti passano attraverso un ciclo di convalida del prodotto intenso e completamente automatizzato, che prevede più passaggi per garantire l&#39;assenza di interruzioni del servizio per i sistemi in produzione. I controlli sanitari sono utilizzati per monitorare lo stato della domanda. Se questi controlli non vengono eseguiti durante un AEM come aggiornamento del Cloud Service, il rilascio non verrà completato e  Adobe verificherà perché l&#39;aggiornamento ha causato questo comportamento imprevisto.

[I test di prodotto e i test](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/understand-test-results.html#functional-testing) funzionali dei clienti che impediscono agli aggiornamenti di prodotto e ai suggerimenti sul codice cliente di interrompere la produzione vengono convalidati anche durante un aggiornamento AEM versione.

>[NOTA]
>Se il codice personalizzato è stato messo in staging e successivamente rifiutato dall&#39;utente, il successivo aggiornamento AEM rimuoverà tali modifiche per riflettere il tag git dell&#39;ultima release cliente riuscita alla produzione.

## Archivio nodi composito {#composite-node-store}

Come già detto, gli aggiornamenti nella maggior parte dei casi non generano tempi di inattività, anche per l&#39;autore, che è un cluster di nodi. Gli aggiornamenti Rolling sono possibili a causa della funzione *composito archivio* nodi in Oak.

Questa funzione consente AEM fare riferimento a più repository contemporaneamente. In una distribuzione continuativa, la nuova versione di AEM verde contiene il proprio `/libs` (il repository immutabile basato su TarMK), distinto dalla precedente versione di AEM blu, anche se entrambi fanno riferimento a un repository mutabile basato su DocumentMK condiviso che contiene aree come `/content` , `/conf` , `/etc` e altri. Poiché sia il blu che il verde hanno versioni proprie di `/libs`, possono essere entrambi attivi durante l&#39;aggiornamento continuo, assumendo entrambi il traffico fino a quando il blu non viene completamente sostituito dal verde.

