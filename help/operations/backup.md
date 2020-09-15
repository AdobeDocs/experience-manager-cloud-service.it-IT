---
title: Backup e ripristino in AEM come Cloud Service
description: 'Backup e ripristino in AEM come Cloud Service '
translation-type: tm+mt
source-git-commit: c3af507716ef60541ecca8dafb797651e8ece9d3
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# Backup e ripristino in AEM come Cloud Service

Se si verifica un danneggiamento dei contenuti o dei dati, AEM come Cloud Service è possibile ripristinare l&#39;applicazione completa (codice e contenuto) di un cliente a tempi prestabiliti specifici negli ultimi sette giorni, sostituendo il contenuto in produzione.
Se la distribuzione di un cliente, ovvero il codice dell&#39;applicazione distribuito è interrotta o non funziona correttamente, è preferibile correggerla e passare a una nuova versione anziché ripristinarla dal backup. Il backup viene eseguito in un modo che non ha alcun impatto sulle prestazioni di esecuzione di un&#39;applicazione.

>[!CAUTION]
>
>Questa funzione deve essere utilizzata solo in caso di problemi gravi con il codice o il contenuto. I dati recenti tra il tempo del backup ripristinato e il presente andranno persi. La gestione temporanea verrà inoltre ripristinata alla versione precedente.

## Guida all’uso

I clienti devono presentare un ticket di assistenza, descrivendo il problema riscontrato. Ciò porterà ad un&#39;indagine da parte  supporto del Adobe, che deciderà se è necessario un ripristino.

AEM come Cloud Service supporta:

* 24 ore di recupero, il che significa che il sistema può essere ripristinato in qualsiasi punto nelle ultime 24 ore.
* Ripristina da una marca temporale specifica definita dal Adobe  eseguita una volta al giorno per gli ultimi 7 giorni.  Eventuali messaggi di replica (eliminazione, aggiornamenti, creazione) verranno conservati.

In tutti i casi, la versione del codice personalizzato sarà presa dall&#39;ultima distribuzione riuscita prima del punto di ripristino.

L&#39;obiettivo RTO (Recovery Time Objective) varierà in base alle dimensioni del repository, ma come linea guida generale una volta che la sequenza di ripristino ha inizio dovrebbe richiedere circa 30 minuti.

Dopo un ripristino, la versione AEM verrà aggiornata alla versione più recente.

**I dati provenienti da ambienti eliminati vengono persi in modo permanente e non possono essere recuperati.**
