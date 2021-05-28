---
title: Backup e ripristino in AEM come Cloud Service
description: Backup e ripristino in AEM come Cloud Service
exl-id: 469fb1a1-7426-4379-9fe3-f5b0ebf64d74
source-git-commit: dfbd0f38017d02810da05ccadbc5f2fbd5826aa3
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# Backup e ripristino in AEM come Cloud Service


>[!CONTEXTUALHELP]
>id="aemcloud_golive_backuprestore"
>title="Backup e ripristino"
>abstract="AEM come Cloud Service può ripristinare l&#39;applicazione completa (codice e contenuto) di un cliente a orari specifici e predeterminati negli ultimi sette giorni, sostituendo ciò che era in produzione. Questa funzione deve essere utilizzata solo in caso di gravi problemi con il codice o il contenuto. I dati recenti tra il momento del backup ripristinato e il presente andranno persi. Lo staging verrà ripristinato anche alla vecchia versione."

In caso di danneggiamento dei contenuti o dei dati, AEM come Cloud Service può ripristinare l&#39;applicazione completa (codice e contenuto) di un cliente a orari specifici e predeterminati negli ultimi sette giorni, sostituendo ciò che era in produzione.
Se la distribuzione di un cliente, ovvero il codice dell&#39;applicazione distribuito è danneggiato o non è compatibile, è preferibile correggerla e passare a una nuova versione anziché ripristinarla dal backup. Il backup viene eseguito in un modo che non ha alcun impatto sulle prestazioni di runtime di un&#39;applicazione.

>[!CAUTION]
>
>Questa funzione deve essere utilizzata solo in caso di gravi problemi con il codice o il contenuto. I dati recenti tra il momento del backup ripristinato e il presente andranno persi. Lo staging verrà ripristinato anche alla vecchia versione.

## Guida all’uso

I clienti devono presentare una richiesta di supporto per descrivere il problema riscontrato. Ciò porterà ad un&#39;indagine da parte del supporto Adobe, che determinerà se è necessario un ripristino.

AEM come Cloud Service supporta:

* 24 ore di recupero nel tempo, il che significa che il sistema può essere ripristinato in qualsiasi punto nelle ultime 24 ore.
* Ripristina da una marca temporale definita in Adobe specifica eseguita una volta al giorno per gli ultimi 7 giorni.  Eventuali messaggi di replica (eliminazione, aggiornamenti, creazione) verranno mantenuti.

In tutti i casi, la versione del codice personalizzato verrà presa dall&#39;ultima distribuzione riuscita prima del punto di ripristino.

L&#39;obiettivo RTO (Recovery Time Objective) varia a seconda delle dimensioni dell&#39;archivio, ma come linea guida generale una volta che la sequenza di ripristino inizia dovrebbe richiedere circa 30 minuti.

Dopo un ripristino, la versione AEM verrà aggiornata alla versione più recente.

**I dati degli ambienti eliminati vengono persi in modo permanente e non possono essere recuperati.**
