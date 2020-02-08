---
title: Backup e ripristino in AEM come servizio cloud
description: 'Backup e ripristino in AEM come servizio cloud '
translation-type: tm+mt
source-git-commit: 8fba31951276d7e0de1f3bd079e42e431edaff4e

---


# Backup e ripristino in AEM come servizio cloud

In caso di danneggiamento dei contenuti o dei dati, AEM come servizio cloud può ripristinare l’applicazione completa (codice e contenuto) di un cliente a orari specifici e predeterminati negli ultimi sette giorni, sostituendo gli elementi in produzione.
Se la distribuzione di un cliente, ovvero il codice dell&#39;applicazione distribuito è interrotta o non funziona correttamente, è preferibile correggerla e passare a una nuova versione anziché ripristinarla dal backup.

>[!CAUTION]
>
>Questa funzione deve essere utilizzata solo in caso di problemi gravi con il codice o il contenuto. I dati recenti tra il tempo del backup ripristinato e il presente andranno persi. La gestione temporanea verrà inoltre ripristinata alla versione precedente.

## Guida all’uso

I clienti devono presentare un ticket di assistenza, descrivendo il problema riscontrato. Questo determinerà un&#39;indagine da parte del supporto Adobe, che determinerà se è necessario eseguire il ripristino.

AEM come servizio Cloud supporta:

* 24 ore di recupero, il che significa che il sistema può essere ripristinato in qualsiasi punto nelle ultime 24 ore.
* Ripristina da una marca temporale specifica definita da Adobe, utilizzata una volta al giorno per gli ultimi 7 giorni.  Eventuali messaggi di replica (eliminazione, aggiornamenti, creazione) verranno conservati.

In tutti i casi, la versione del codice personalizzato sarà presa dall&#39;ultima distribuzione riuscita prima del punto di ripristino.

L&#39;obiettivo RTO (Recovery Time Objective) varierà in base alle dimensioni del repository, ma come linea guida generale una volta che la sequenza di ripristino ha inizio dovrebbe richiedere circa 30 minuti.

Dopo un ripristino, la versione di AEM verrà aggiornata al più recente.

**I dati provenienti da ambienti eliminati vengono persi in modo permanente e non possono essere recuperati.**
