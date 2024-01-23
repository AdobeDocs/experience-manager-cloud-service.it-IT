---
title: Backup e ripristino in AEM as a Cloud Service
description: Informazioni su Backup e ripristino in AEM as a Cloud Service
exl-id: 469fb1a1-7426-4379-9fe3-f5b0ebf64d74
source-git-commit: b77ee0697e8f6f4aeaa6651336588f1c5321abd1
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 24%

---


# Backup e ripristino in AEM as a Cloud Service {#backup-aemaacs}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_backuprestore"
>title="Backup e ripristino"
>abstract="AEM as a Cloud Service può ripristinare l’applicazione completa (codice e contenuto) di un cliente a orari specifici e predeterminati negli ultimi sette giorni, sostituendo ciò che era in produzione. Questa funzione deve essere utilizzata solo in caso di gravi problemi con il codice o il contenuto. I dati recenti tra il momento del backup ripristinato e il momento attuale andranno persi. Anche lo staging verrà ripristinato alla versione precedente."

In caso di danneggiamento dei contenuti o dei dati, AEM as a Cloud Service può ripristinare l’applicazione completa di un cliente (codice e contenuto). Viene ripristinato in tempi specifici e predeterminati negli ultimi sette giorni, sostituendo ciò che era in produzione.
Se la distribuzione di un cliente, ovvero il codice dell&#39;applicazione distribuito è danneggiato o in stato di bug, è preferibile correggerla e passare a una nuova versione anziché ripristinarla dal backup. Il backup viene eseguito in modo da non influire sulle prestazioni di esecuzione di un&#39;applicazione.

>[!CAUTION]
>
>Questa funzione deve essere utilizzata solo in caso di gravi problemi con il codice o il contenuto. I dati recenti tra il momento del backup ripristinato e il momento attuale andranno persi. Anche la gestione temporanea viene ripristinata alla versione precedente. Se i dati recenti vengono conservati, devono essere esportati tramite un pacchetto di contenuti prima del ripristino e reinstallati nell’archivio ripristinato.

## Guida all’uso {#how-to-use}

I clienti devono inviare un ticket di supporto, descrivendo il problema riscontrato. Il ticket di supporto di solito porta a un&#39;indagine da parte del supporto Adobe che può quindi determinare se è necessario un ripristino.

AEM as a Cloud Service supporta:

* Backup e ripristino per ambienti di staging, produzione e sviluppo.
* Ripristino point-in-time di 24 ore, che consente di ripristinare il sistema in qualsiasi momento delle ultime 24 ore.
* Ripristina da una marca temporale specifica definita dall’Adobe, rilevata due volte al giorno per gli ultimi sette giorni. Tutti i messaggi di replica (eliminazioni, aggiornamenti, creazioni) vengono mantenuti.

In tutti i casi, la versione del codice personalizzato è quella dell’ultima distribuzione riuscita prima del punto di ripristino.

L&#39;obiettivo del tempo di ripristino (RTO, Recovery Time Objective) può variare, ma come linea guida generale, la sequenza di ripristino dura in media da 60 a 90 minuti a seconda di diversi fattori, come la dimensione dell&#39;archivio. Gli ambienti di anteprima e gli editori con più aree geografiche possono estendere l’obiettivo del tempo di ripristino.

Dopo un ripristino, la versione dell’AEM viene aggiornata alla più recente.

>[!CAUTION]
>
>I dati provenienti da ambienti eliminati vengono persi in modo permanente e non possono essere recuperati.

## Backup fuori sede {#offsite-backup}

Mentre i backup regolari coprono il rischio di cancellazioni accidentali o di guasti tecnici all&#39;interno dei Cloud Service AEM, devono essere coperti anche i rischi che possono derivare dal guasto di una regione. Oltre alla disponibilità, il rischio maggiore in tali interruzioni dell’area dati è principalmente la perdita di dati.
AEM as a Cloud Service copre questo rischio come standard per tutti gli ambienti di produzione AEM. Copia in modo continuo l&#39;intero contenuto dell&#39;AEM in un&#39;area remota e lo rende disponibile per il ripristino per tre mesi. L&#39;Adobe chiama questa funzionalità Offsite Backup.
Il ripristino dei Cloud Service AEM per gli ambienti di staging e produzione viene eseguito da AEM Service Reliability Engineering in caso di interruzioni dell’area dati.
