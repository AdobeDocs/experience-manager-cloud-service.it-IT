---
title: SDK di AEM as a Cloud Service
description: Una panoramica del AEM come Cloud Service Software Development Kit
translation-type: tm+mt
source-git-commit: 0b46cc8ce4229138df84c70193cf9068e1200f0a
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 1%

---


# Il AEM come SDK di Cloud Service {#aem-as-a-cloud-service-sdk}

L’AEM come SDK per Cloud Service è composta dai seguenti artefatti:

* **Jar**  di Quickstart - Il runtime di AEM utilizzato per lo sviluppo locale
* **Java API Jar**  - La dipendenza Java Jar/Maven che espone tutte le API Java consentite che possono essere utilizzate per lo sviluppo rispetto a AEM come Cloud Service. Precedentemente denominato Uberjar
* **Javadoc Jar**  - I javadocs per Java API Jar
* **Strumenti**  Dispatcher - Set di strumenti utilizzati per lo sviluppo locale contro il Dispatcher. Artefatti separati per unix e finestre

Inoltre, alcuni clienti che erano stati precedentemente distribuiti con AEM 6.5 o versioni precedenti utilizzeranno gli artifact riportati di seguito. Se la compilazione locale non funziona con l&#39;archivio di avvio rapido e si sospetta che sia dovuta a interfacce rimosse dall&#39;AEM distribuito come Cloud Service, contattare l&#39;Assistenza clienti per determinare se è necessario accedere. Ciò richiederà modifiche nel backend.

* **6.5 Jar**  API Java obsoleto - un set aggiuntivo di interfacciati rimosso dalla AEM 6.5
* **6.5 Javadoc Jar**  obsoleto - i Javadocs per il set aggiuntivo di interfacciati

## Creazione per l&#39;SDK {#building-for-the-sdk}

Il AEM come SDK Cloud Service viene utilizzato per creare e distribuire codice personalizzato. Per ulteriori dettagli, fare riferimento alla [AEM documentazione Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en). A un livello elevato, vengono eseguiti i seguenti passaggi:

* **Compila il codice**. Come previsto, il codice sorgente viene compilato, generando i pacchetti di contenuto risultanti
* **Creare artefatti**. Artefatti generati durante questo processo
* **Analizzare i bundle**. I pacchetti vengono analizzati utilizzando il plugin dell&#39;analizzatore Maven, che cerca problemi nel progetto Maven come dipendenze mancanti
* **Implementare gli artefatti**. Gli artifact vengono distribuiti nel server locale.

Gli stessi passaggi vengono eseguiti da Cloud Manager quando si distribuisce in ambienti cloud. L&#39;esecuzione delle build localmente consente lo sviluppo locale e i test in modo che gli sviluppatori possano scoprire in modo efficiente i problemi di codice o strutturali ben prima di impegnarsi nel controllo del codice sorgente e attivare le distribuzioni di Cloud Manager, il che può richiedere più tempo.

## Accesso al AEM come SDK di Cloud Service {#accessing-the-aem-as-a-cloud-service-sdk}

* È possibile controllare l&#39;icona AEM   **Informazioni su Adobe Experience Manager** per conoscere la versione di AEM in esecuzione in produzione.
* Gli strumenti di avvio rapido e Dispatcher possono essere scaricati come file ZIP dal [portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html). L&#39;accesso agli elenchi dell&#39;SDK è limitato a quelli con AEM Managed Services o AEM come ambienti di Cloud Service.
* Java API Jar e Javadoc Jar possono essere scaricati tramite gli strumenti maven, sia dalla riga di comando che con l&#39;IDE preferito.
* I promotori del progetto maven devono fare riferimento al seguente pacchetto API Jar. È inoltre necessario fare riferimento a questa dipendenza in qualsiasi sottomodulo.

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
>La voce della versione per l’SDK deve corrispondere alla versione di AEM come Cloud Service. Per vedere la versione in uso, effettuate l&#39;accesso al AEM, quindi passate al punto interrogativo nell&#39;angolo superiore destro dello schermo e selezionate **[!UICONTROL Informazioni su Adobe Experience Manager]**


## Aggiornamento di un progetto locale con una nuova versione SDK {#refreshing-a-local-project-with-a-new-skd-version}

Quando si consiglia di aggiornare il progetto locale con un nuovo SDK?

È *consigliato* aggiornarlo almeno dopo una versione di manutenzione mensile.

È *facoltativo* aggiornarlo dopo qualsiasi rilascio giornaliero di manutenzione. I clienti verranno informati quando la loro istanza di produzione verrà aggiornata a una nuova versione AEM. Per le versioni di manutenzione giornaliera, non è previsto che il nuovo SDK sarà cambiato in modo significativo, se del caso. Tuttavia, si consiglia di aggiornare occasionalmente l&#39;ambiente locale AEM sviluppatore con l&#39;SDK più recente, quindi di rigenerare e testare l&#39;applicazione personalizzata. La versione di manutenzione mensile in genere include modifiche di maggiore impatto e pertanto gli sviluppatori dovrebbero aggiornare, ricreare e testare immediatamente.

Di seguito è riportata la procedura consigliata per l&#39;aggiornamento di un ambiente locale:

1. Verificate che eventuali contenuti utili siano impegnati nel progetto nel controllo del codice sorgente o siano disponibili in un pacchetto di contenuti modificabile per un&#39;importazione successiva
1. Il contenuto del test di sviluppo locale deve essere memorizzato separatamente in modo che non venga distribuito come parte della build della pipeline di Cloud Manager. Questo perché deve essere utilizzato solo per lo sviluppo locale
1. Interrompi Avvio rapido in esecuzione
1. Spostate la cartella `crx-quickstart` in un&#39;altra cartella per garantire la massima sicurezza
1. Prendete nota della nuova versione AEM, nota in Cloud Manager (che verrà utilizzata per identificare la nuova versione di QuickStart Jar da scaricare ulteriormente in seguito)
1. Scaricate il JAR di QuickStart la cui versione corrisponde alla versione di Production AEM dal portale di distribuzione del software
1. Create una nuova cartella e inserite il nuovo QuickStart Jar all&#39;interno
1. Avviate la nuova Avvio rapido con le modalità di esecuzione desiderate (rinominando il file o passando le modalità di esecuzione tramite `-r`).
   * Accertatevi che nella cartella non rimangano altri collegamenti di avvio rapido.
1. Creare l&#39;applicazione AEM
1. Distribuzione dell&#39;applicazione AEM a AEM locale tramite PackageManager
1. Installate tutti i pacchetti di contenuto modificabile necessari per il test dell&#39;ambiente locale tramite PackageManager
1. Proseguire lo sviluppo e distribuire le modifiche in base alle esigenze

Se è presente del contenuto che deve essere installato con ogni nuova AEM versione di QuickStart, includetelo in un pacchetto di contenuto e nel controllo del sorgente del progetto. Quindi, installatelo ogni volta.

È consigliabile aggiornare frequentemente l&#39;SDK (ad esempio, due volte alla settimana) e smaltire giornalmente lo stato locale completo in modo che non dipenda accidentalmente dai dati sullo stato dell&#39;applicazione.

Nel caso in cui tu dipenda da CryptoSupport ([configurando le credenziali di Cloudservices o il servizio di posta SMTP in AEM o utilizzando l&#39;API CryptoSupport nella tua applicazione](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/crypto/CryptoSupport.html)), le proprietà crittografate saranno crittografate da una chiave generata automaticamente al primo avvio di un ambiente AEM. Mentre la configurazione del cloud si occupa di riutilizzare automaticamente la CryptoKey specifica per l&#39;ambiente, è necessario inserire la chiave di crittografia nell&#39;ambiente di sviluppo locale.

Per impostazione predefinita AEM è configurato per memorizzare i dati chiave nella cartella di dati di una cartella, ma per semplificare il riutilizzo in fase di sviluppo, il processo AEM può essere inizializzato al primo avvio con &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Verranno generati i dati di cifratura in &quot;`/etc/key`&quot;.

Per poter riutilizzare i pacchetti di contenuto contenenti i valori crittografati, è necessario eseguire la procedura seguente:

* Quando avviate inizialmente quickstart.jar locale, accertatevi di aggiungere il parametro seguente: &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. È consigliabile, ma facoltativo, aggiungerlo sempre.
* La prima volta che avete avviato un&#39;istanza create un pacchetto contenente un filtro per la radice &quot;`/etc/key`&quot;. Questo manterrà il segreto per essere riutilizzato in tutti gli ambienti per i quali si desidera che vengano riutilizzati
* Esportate eventuale contenuto modificabile contenente segreti o cercate i valori crittografati tramite `/crx/de` per aggiungerlo al pacchetto che verrà riutilizzato tra le installazioni
* Ogni volta che eseguite il spin up di una nuova istanza (per sostituire una nuova versione o in quanto più ambienti di sviluppo dovrebbero condividere le credenziali per il test), installate il pacchetto prodotto nei passaggi 2 e 3 per poter riutilizzare il contenuto senza dover riconfigurare manualmente. Questo perché ora la crittografia è sincronizzata.
