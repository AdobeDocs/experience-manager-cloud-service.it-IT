---
title: Backup e ripristino in AEM as a Cloud Service
description: Backup e ripristino in AEM as a Cloud Service
exl-id: 469fb1a1-7426-4379-9fe3-f5b0ebf64d74
source-git-commit: eec03acf5d208236ddac338134f95fb3aaa5ee26
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 3%

---


# Backup e ripristino in AEM as a Cloud Service {#backup-aemaacs}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_backuprestore"
>title="Backup e ripristino"
>abstract="AEM as a Cloud Service può ripristinare l&#39;applicazione completa (codice e contenuto) di un cliente a orari specifici e predeterminati negli ultimi sette giorni, sostituendo ciò che era in produzione. Questa funzione deve essere utilizzata solo in caso di gravi problemi con il codice o il contenuto. I dati recenti tra il momento del backup ripristinato e il presente andranno persi. Lo staging verrà ripristinato anche alla vecchia versione."

In caso di danneggiamento del contenuto o dei dati, AEM as a Cloud Service può ripristinare l&#39;applicazione completa (codice e contenuto) di un cliente a orari specifici e predeterminati negli ultimi sette giorni, sostituendo ciò che era in produzione.
Se la distribuzione di un cliente, ovvero il codice dell&#39;applicazione distribuito è danneggiato o non è compatibile, è preferibile correggerla e passare a una nuova versione anziché ripristinarla dal backup. Il backup viene eseguito in un modo che non ha alcun impatto sulle prestazioni di runtime di un&#39;applicazione.

>[!CAUTION]
>
>Questa funzione deve essere utilizzata solo in caso di gravi problemi con il codice o il contenuto. I dati recenti tra il momento del backup ripristinato e il presente andranno persi. Lo staging verrà ripristinato anche alla vecchia versione.

## Guida all’uso {#how-to-use}

I clienti devono presentare una richiesta di supporto per descrivere il problema riscontrato. Ciò porterà ad un&#39;indagine da parte del supporto Adobe, che determinerà se è necessario un ripristino.

AEM supporto as a Cloud Service:

* Backup e ripristino per ambienti di stage, produzione e sviluppo.
* 24 ore di recupero nel tempo, il che significa che il sistema può essere ripristinato in qualsiasi punto nelle ultime 24 ore.
* Ripristina da una marca temporale specifica definita in Adobe eseguita due volte al giorno per gli ultimi 7 giorni.  Eventuali messaggi di replica (eliminazione, aggiornamenti, creazione) verranno mantenuti.

In tutti i casi, la versione del codice personalizzato verrà presa dall&#39;ultima distribuzione riuscita prima del punto di ripristino.

L&#39;obiettivo RTO (Recovery Time Objective) può variare, ma come linea guida generale, la sequenza di ripristino richiede in media tra 60 e 90 minuti a seconda di diversi fattori, come la dimensione dell&#39;archivio. Gli ambienti di anteprima e gli editori con più aree possono estendere l’obiettivo del tempo di ripristino.

Dopo un ripristino, la versione AEM verrà aggiornata alla versione più recente.

>[!CAUTION]
>
>I dati provenienti da ambienti eliminati vengono persi in modo permanente e non possono essere recuperati.

## Backup fuori sede {#offsite-backup}

Anche se i backup regolari coprono il rischio di eliminazioni accidentali o errori tecnici in AEM Cloud Services, devono essere coperti anche i rischi che possono derivare dal guasto di una regione. Oltre alla disponibilità, il rischio maggiore in tali interruzioni dell&#39;area dati è principalmente la perdita di dati.
AEM as a Cloud Service copre questo rischio come standard per tutti gli ambienti di produzione AEM copiando continuamente l&#39;intero contenuto AEM in una regione remota e rendendolo disponibile per il ripristino per un periodo di 3 mesi. Questa funzionalità viene chiamata Offsite Backup.
Il ripristino di AEM Cloud Services per ambienti di stage e produzione viene eseguito da AEM Service Reliability Engineering in caso di interruzioni dell’area dati.
