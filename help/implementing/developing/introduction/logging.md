---
title: Registrazione
description: Scoprite come configurare i parametri globali per il servizio di registrazione centrale, le impostazioni specifiche per i singoli servizi o come richiedere la registrazione dei dati.
translation-type: tm+mt
source-git-commit: a7c8e1ab8e0196a3a79d8e0963192775e64a2400
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 3%

---


# Registrazione {#logging}

AEM come Cloud Service è una piattaforma che consente ai clienti di includere codice personalizzato per creare esperienze univoche per la propria base di clienti. In questo senso, la registrazione è una funzione fondamentale per eseguire il debug e comprendere l&#39;esecuzione del codice sullo sviluppo locale e gli ambienti cloud, in particolare l&#39;AEM come un ambiente di sviluppo  Cloud Service.

AEM livelli di registrazione e di registro vengono gestiti in file di configurazione memorizzati come parte del progetto AEM in Git e distribuiti come parte del progetto AEM tramite Cloud Manager. L&#39;accesso AEM come Cloud Service può essere suddiviso in due set logici:

* Registrazione AEM, che esegue la registrazione a livello di applicazione AEM
* Registrazione Apache HTTPD Web Server/Dispatcher, che esegue la registrazione del server Web e di Dispatcher sul livello di pubblicazione.

## Registrazione AEM {#aem-loggin}

La registrazione a livello di applicazione AEM è gestita da tre registri:

1. AEM registri Java, che eseguono il rendering delle istruzioni di registrazione Java per l&#39;applicazione AEM.
1. Registri di richieste HTTP, che registrano le informazioni sulle richieste HTTP e le risposte fornite da AEM
1. Registri di accesso HTTP, quali informazioni di riepilogo del registro e richieste HTTP inviate da AEM

Notate che le richieste HTTP servite dalla cache Dispatcher del livello di pubblicazione o dalla rete CDN upstream non si riflettono in questi registri.

### Registrazione Java AEM {#aem-java-logging}

AEM come Cloud Service  fornisce l&#39;accesso alle istruzioni di registro Java. Gli sviluppatori di applicazioni per AEM devono seguire le best practice generali di registrazione Java, registrare le relative istruzioni sull&#39;esecuzione di codice personalizzato, ai seguenti livelli di registro:

<table>
<tbody>
<tr>
<td> <b>Ambiente AEM</b></td>
<td> <b>Livello registro</b></td>
<td> <b>Descrizione</b></td>
<td> <b>Disponibilità dell'istruzione del registro</b></td>
</tr>
<tr>
<td> Sviluppo</td>
<td> DEBUG</td>
<td> Descrive cosa accade nell'applicazione.

Quando la registrazione DEBUG è attiva, le istruzioni che forniscono un&#39;immagine chiara delle attività che si verificano e tutti i parametri chiave che influenzano l&#39;elaborazione vengono registrate.</td>
<td> <ul>
<li> Sviluppo locale</li>
<li>Sviluppo</li>
</ul></td>
</tr>
<tr>
<td> Stadio</td>
<td> AVVISO</td>
<td> Descrive le condizioni che possono diventare errori.

Quando la registrazione WARN è attiva, vengono registrate solo le istruzioni che indicano i condizionatori che si stanno avvicinando alla sub-ottimizzazione.</td>
<td> <ul>
<li> Sviluppo locale</li>
<li>Sviluppo</li>
<li>Area di visualizzazione</li>
</ul></td>
</tr>
<tr>
<td> Produzione</td>
<td> ERRORE</td>
<td> Descrive le condizioni che indicano un errore e che devono essere risolte.

Quando la registrazione degli errori è attiva, vengono registrate solo le istruzioni che indicano gli errori. Le istruzioni del registro degli errori indicano un problema grave che dovrebbe essere risolto il prima possibile.</td>
<td> <ul>
<li> Sviluppo locale</li>
<li>Sviluppo</li>
<li>Area di visualizzazione</li>
<li>Produzione</li>
</ul></td>
</tr>
</tbody>
</table>