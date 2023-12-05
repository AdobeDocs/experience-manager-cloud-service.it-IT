---
title: SDK di AEM as a Cloud Service
description: Panoramica di AEM as a Cloud Service Software Development Kit
exl-id: 06f3d5ee-440e-4cc5-877a-5038f9bd44c6
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 1%

---

# L’SDK AEM as a Cloud Service {#aem-as-a-cloud-service-sdk}

L’SDK as a Cloud Service dell’AEM è composto dai seguenti artefatti:

* **Jar Quickstart** - Il runtime AEM utilizzato per lo sviluppo locale
* **Java™ API Jar** - La dipendenza Java™ Jar/Maven che espone tutte le API Java™ consentite che possono essere utilizzate per sviluppare contro AEM as a Cloud Service. Precedentemente denominato Uberjar
* **Jar Javadoc** - Java per Java™ API Jar
* **Strumenti di Dispatcher** : set di strumenti utilizzati per sviluppare a livello locale rispetto a Dispatcher. Artefatti separati per UNIX® e windows

Inoltre, alcuni clienti che sono stati distribuiti in precedenza con AEM 6.5 o versioni precedenti utilizzano gli artefatti riportati di seguito. Se la compilazione locale non funziona con Quickstart Jar e pensi che derivi dalla rimozione di interfacce da AEM implementato as a Cloud Service, contatta l’Assistenza clienti. Possono determinare se è necessario accedere a. Richiede modifiche nel backend.

* **Jar API Java™ 6.5 obsoleto** - un set aggiuntivo di interfacce che sono state rimosse dopo l’AEM 6.5
* **Jar Javadoc Obsoleto 6.5** - JavaScript per il set aggiuntivo di interfacce

## Creazione per l’SDK {#building-for-the-sdk}

L’SDK as a Cloud Service dall’AEM viene utilizzato per generare e distribuire il codice personalizzato. Consulta la [Documentazione di Archetipo progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en). Ad alto livello, vengono eseguiti i seguenti passaggi:

* **Compila codice**. Come previsto, il codice sorgente viene compilato, generando i pacchetti di contenuti risultanti
* **Creare artefatti**. Gli artefatti vengono generati durante questo processo
* **Analizzare i bundle**. I bundle vengono analizzati utilizzando il plug-in Maven Analyzer, che cerca problemi nel progetto Maven, come dipendenze mancanti
* **Distribuire gli artefatti**. Gli artefatti vengono distribuiti nel server locale.

Gli stessi passaggi vengono eseguiti da Cloud Manager durante la distribuzione in ambienti Cloud. L’esecuzione locale delle build consente lo sviluppo e il test locali. Gli sviluppatori possono individuare in modo efficiente problemi di codice o strutturali prima di attivare il controllo del codice sorgente e attivare le distribuzioni di Cloud Manager, che possono richiedere più tempo.

>[!NOTE]
>
>L’SDK as a Cloud Service dall’AEM deve essere costruito con una distribuzione e una versione di Java supportata da [Ambiente di build di Cloud Manager](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). I clienti AEM as a Cloud Service possono scaricare l’Oracle JDK dalla sezione [Portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html) e disporre del supporto esteso Java 11 fino a settembre 2026 a causa dei termini di licenza e supporto Adobe per la tecnologia Java Oracle quando utilizzata nei progetti Adobe Experience Manager.

## Accesso all’SDK as a Cloud Service per l’AEM {#accessing-the-aem-as-a-cloud-service-sdk}

* Puoi controllare l’Admin Console dell’AEM **Informazioni su Adobe Experience Manager** per individuare la versione di AEM in esecuzione in produzione.
* Il file jar quickstart e gli strumenti di Dispatcher possono essere scaricati come file zip dal file [Portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html). L’accesso agli elenchi dell’SDK è limitato alle persone che dispongono di ambienti su AEM Managed Services o AEM as a Cloud Service.
* Il file JAR dell’API Java™ e il file JAR JavaScript possono essere scaricati tramite gli strumenti Maven, tramite la riga di comando o l’IDE preferito.
* Le pom del progetto Maven devono fare riferimento al seguente pacchetto API Jar. È inoltre necessario fare riferimento alla dipendenza da qualsiasi pacchetto secondario.

```
<dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>aem-sdk-api</artifactId>
  <version>2019.11.3006.20191108T223635Z-191201</version>
  <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>La voce di versione per l’SDK deve corrispondere alla versione dell’AEM as a Cloud Service. Puoi vedere quale versione stai utilizzando accedendo a AEM. Nell’angolo superiore destro dello schermo, vai al punto interrogativo e seleziona **[!UICONTROL Informazioni su Adobe Experience Manager]**.


## Aggiornamento di un progetto locale con una nuova versione SDK {#refreshing-a-local-project-with-a-new-skd-version}

Quando è consigliabile aggiornare il progetto locale con un nuovo SDK?

Adobe *consiglia* aggiornamento dopo una versione di manutenzione mensile.

È *facoltativo* per aggiornarla dopo qualsiasi versione di manutenzione giornaliera. I clienti vengono informati quando la loro istanza di produzione viene aggiornata correttamente a una nuova versione AEM. Per le versioni di manutenzione giornaliere, non si prevede che il nuovo SDK sia cambiato in modo significativo, se non del tutto. Tuttavia, si consiglia di aggiornare occasionalmente l’ambiente di sviluppo AEM locale con l’SDK più recente, quindi di ricreare e testare l’applicazione personalizzata. La versione di manutenzione mensile in genere include modifiche di maggiore impatto e pertanto gli sviluppatori devono immediatamente aggiornare, ricreare e testare.

Di seguito è riportata la procedura consigliata per l’aggiornamento di un ambiente locale:

1. Assicurati che qualsiasi contenuto utile sia confermato nel progetto nel controllo del codice sorgente o disponibile in un pacchetto di contenuto mutabile per un’importazione successiva.
1. Il contenuto dei test di sviluppo locale deve essere archiviato separatamente in modo che non venga distribuito come parte della build della pipeline di Cloud Manager. Il motivo è che viene usato solo per lo sviluppo locale.
1. Arresta l&#39;avvio rapido in esecuzione.
1. Sposta il `crx-quickstart` in una cartella diversa per la conservazione sicura.
1. Nota la nuova versione dell’AEM, riportata in Cloud Manager (viene utilizzata per identificare la nuova versione di QuickStart Jar per scaricarla ulteriormente in).
1. Scarica il file JAR QuickStart la cui versione corrisponde a quella dell’AEM di produzione dal portale di distribuzione software.
1. Crea una nuova cartella e inserisci il nuovo file JAR QuickStart.
1. Avviare il nuovo QuickStart con le modalità di esecuzione desiderate (rinominando il file o passando in modalità di esecuzione mediante `-r`).
   * Assicurati che nella cartella non sia presente alcun resto del vecchio modulo quickstart.
1. Crea la tua applicazione AEM.
1. Distribuisci l’applicazione AEM nell’AEM locale tramite Gestione pacchetti.
1. Installa tutti i pacchetti di contenuti mutabili necessari per il test dell’ambiente locale tramite Gestione pacchetti.
1. Continua lo sviluppo e implementa le modifiche necessarie.

Se è necessario installare un contenuto con ogni nuova versione di avvio rapido per AEM, includerlo in un pacchetto di contenuti e nel controllo del codice sorgente del progetto. Quindi, installarlo ogni volta.

Si consiglia di aggiornare frequentemente l’SDK (ad esempio, ogni due settimane) ed eliminare giornalmente lo stato locale completo in modo che non dipenda accidentalmente dai dati di stato nell’applicazione.

Se si utilizza CryptoSupport ([configurando le credenziali dei servizi Cloud o del servizio di posta SMTP in AEM oppure utilizzando l’API CryptoSupport nell’applicazione](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/crypto/CryptoSupport.html)), le proprietà crittografate sono crittografate da una chiave. Questa chiave viene generata automaticamente al primo avvio di un ambiente AEM. Anche se la configurazione cloud si occupa del riutilizzo automatico della CryptoKey specifica per l’ambiente, è necessario inserire la crittografia nell’ambiente di sviluppo locale.

Per impostazione predefinita, l’AEM è configurato per memorizzare i dati chiave all’interno della cartella dati di una cartella, ma per facilitare il riutilizzo in fase di sviluppo, il processo AEM può essere inizializzato al primo avvio con &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Questo processo genera i dati di crittografia in &quot;`/etc/key`&quot;.

Per poter riutilizzare i pacchetti di contenuto che contengono i valori crittografati, effettua le seguenti operazioni:

* Quando avvii inizialmente il file quickstart.jar locale, assicurati di aggiungere il seguente parametro: &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Si consiglia, ma facoltativo, di aggiungerlo sempre.
* La prima volta che hai avviato un’istanza, crea un pacchetto contenente un filtro per la radice &quot;`/etc/key`&quot;. Questo pacchetto contiene il segreto da riutilizzare in tutti gli ambienti per i quali desideri riutilizzarli.
* Esporta qualsiasi contenuto mutabile contenente segreti o cerca i valori crittografati tramite `/crx/de` in modo da poterlo aggiungere al pacchetto riutilizzato nelle diverse installazioni.
* Ogni volta che crei una nuova istanza (per sostituirla con una nuova versione o poiché più ambienti di sviluppo devono condividere le credenziali per il test), installa il pacchetto prodotto nei passaggi 2 e 3. In questo modo è possibile riutilizzare il contenuto senza dover riconfigurare manualmente. Il motivo è che ora la crittografia è sincronizzata.
