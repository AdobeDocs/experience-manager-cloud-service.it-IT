---
title: Aggiornamenti AEM versione
description: 'Aggiornamenti AEM versione '
feature: Deploying
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# Aggiornamenti AEM versione {#aem-version-updates}

## Introduzione {#introduction}

AEM come Cloud Service ora utilizza l’integrazione continua e la distribuzione continua (CI/CD) per garantire che i progetti siano nella versione di AEM più recente. Ciò significa che le istanze Production e Stage vengono aggiornate alla versione più recente AEM senza alcuna interruzione del servizio per gli utenti.

>[!NOTE]
>Se l’aggiornamento dell’ambiente di produzione non riesce, Cloud Manager ripristina automaticamente l’ambiente di stage. Questa operazione viene eseguita automaticamente per assicurarsi che al termine di un aggiornamento, sia gli ambienti di stage che di produzione si trovino nella stessa versione AEM.

Gli aggiornamenti delle versioni AEM sono di due tipi:

* **Aggiornamenti push AEM**

   * Può essere rilasciato su base giornaliera.

   * La maggior parte della manutenzione, incluse le ultime correzioni di bug e gli aggiornamenti di sicurezza.

      Con l’applicazione regolare delle modifiche, l’impatto è incrementale, riducendo l’impatto sul servizio.

* **Nuovi aggiornamenti delle funzioni**

   * Rilasciato tramite un programma mensile prevedibile.

Gli aggiornamenti AEM passano attraverso una pipeline di convalida del prodotto intensa e completamente automatizzata, che prevede più passaggi per garantire l&#39;assenza di interruzioni del servizio per tutti i sistemi in produzione. I controlli sanitari sono utilizzati per monitorare lo stato di salute della domanda. Se questi controlli non riescono durante un AEM come aggiornamento del Cloud Service, il rilascio non procederà e l’Adobe esaminerà il motivo per cui l’aggiornamento ha causato questo comportamento imprevisto.

[I test dei prodotti e ](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/understand-test-results.html#functional-testing) i test funzionali dei clienti che impediscono l’interruzione della produzione da parte degli aggiornamenti dei prodotti e del codice cliente vengono convalidati anche durante un aggiornamento della versione AEM.

>[!NOTE]
>
>Se il codice personalizzato è stato inviato alla gestione temporanea e successivamente rifiutato da te, il successivo aggiornamento AEM rimuoverà tali modifiche per riflettere il tag git dell’ultima versione del cliente riuscita in produzione.

## Archivio dei nodi compositi {#composite-node-store}

Come accennato in precedenza, gli aggiornamenti nella maggior parte dei casi non genereranno tempi di inattività, incluso per l’autore, che è un cluster di nodi. Aggiornamenti continui sono possibili a causa della funzione *composita node store* in Oak.

Questa funzione consente AEM fare riferimento contemporaneamente a più archivi. In una distribuzione continua, la nuova versione di AEM verde contiene il proprio `/libs` (l&#39;archivio immutabile basato su TarMK), diverso dalla vecchia versione di AEM blu, anche se entrambi fanno riferimento a un archivio mutabile basato su DocumentMK condiviso che contiene aree come `/content` , `/conf` , `/etc` e altre. Poiché sia il blu che il verde hanno le proprie versioni di `/libs`, possono essere entrambi attivi durante l’aggiornamento continuo, assumendo sia il traffico che il blu viene completamente sostituito dal verde.

