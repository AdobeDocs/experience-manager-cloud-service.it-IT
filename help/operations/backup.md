---
title: Backup e ripristino in AEM as a Cloud Service
description: Backup e ripristino in AEM as a Cloud Service
exl-id: 469fb1a1-7426-4379-9fe3-f5b0ebf64d74
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 22%

---


# Backup e ripristino in AEM as a Cloud Service {#backup-aemaacs}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_backuprestore"
>title="Backup e ripristino"
>abstract="AEM as a Cloud Service può ripristinare l’applicazione completa (codice e contenuto) di un cliente a orari specifici e predeterminati negli ultimi sette giorni, sostituendo ciò che era in produzione. Questa funzione deve essere utilizzata solo in caso di gravi problemi con il codice o il contenuto. I dati recenti tra il momento del backup ripristinato e il momento attuale andranno persi. Lo staging verrà anch’esso ripristinato alla versione precedente."

In caso di danneggiamento dei contenuti o dei dati, AEM as a Cloud Service può ripristinare l’applicazione completa di un cliente (codice e contenuto) in tempi specifici e predeterminati negli ultimi sette giorni, sostituendo ciò che era in produzione.
Se la distribuzione di un cliente, ovvero il codice dell&#39;applicazione distribuito è danneggiato o in stato di bug, è preferibile correggerla e passare a una nuova versione anziché ripristinarla dal backup. Il backup viene eseguito in modo da non influire sulle prestazioni di esecuzione di un&#39;applicazione.

>[!CAUTION]
>
>Questa funzione deve essere utilizzata solo in caso di gravi problemi con il codice o il contenuto. I dati recenti tra il momento del backup ripristinato e il momento attuale andranno persi. Anche la gestione temporanea viene ripristinata alla versione precedente.

## Guida all’uso {#how-to-use}

I clienti devono inviare un ticket di supporto, descrivendo il problema riscontrato. Ciò comporterà un&#39;indagine da parte del supporto Adobe che determinerà se è necessario un ripristino.

AEM as a Cloud Service supporta:

* Backup e ripristino per ambienti di staging, produzione e sviluppo.
* Ripristino point-in-time di 24 ore, il che significa che il sistema può essere ripristinato a qualsiasi punto nelle ultime 24 ore.
* Ripristina da una marca temporale specifica definita dall’Adobe rilevata due volte al giorno per gli ultimi 7 giorni.  Tutti i messaggi di replica (eliminazioni, aggiornamenti, creazioni) vengono mantenuti.

In tutti i casi, la versione del codice personalizzato è quella dell’ultima distribuzione riuscita prima del punto di ripristino.

L&#39;obiettivo del tempo di ripristino (RTO, Recovery Time Objective) può variare, ma come linea guida generale, la sequenza di ripristino richiede in media tra 60 e 90 minuti a seconda di diversi fattori, come la dimensione dell&#39;archivio. Gli ambienti di anteprima e gli editori con più aree geografiche possono estendere l’obiettivo del tempo di ripristino.

Dopo un ripristino, la versione dell’AEM viene aggiornata alla più recente.

>[!CAUTION]
>
>I dati provenienti da ambienti eliminati vengono persi in modo permanente e non possono essere recuperati.

## Backup fuori sede {#offsite-backup}

Anche se i backup regolari coprono il rischio di eliminazioni accidentali o di errori tecnici in AEM Cloud Services, è necessario coprire anche i rischi che possono sorgere dal fallimento di un’area. Oltre alla disponibilità, il rischio maggiore in tali interruzioni dell’area dati è principalmente la perdita di dati.
AEM as a Cloud Service copre questo rischio come standard per tutti gli ambienti di produzione AEM copiando continuamente l&#39;intero contenuto AEM in una regione remota e rendendolo disponibile per il ripristino per un periodo di 3 mesi. Questa funzionalità viene chiamata backup fuori sede.
Il ripristino di AEM Cloud Services per gli ambienti di staging e produzione viene eseguito da AEM Service Reliability Engineering in caso di interruzioni dell’area dati.
