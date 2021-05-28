---
title: SDK di AEM as a Cloud Service
description: Panoramica del kit di sviluppo software AEM as a Cloud Service
exl-id: 06f3d5ee-440e-4cc5-877a-5038f9bd44c6
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 1%

---

# L&#39;SDK AEM come Cloud Service {#aem-as-a-cloud-service-sdk}

L’SDK di AEM come Cloud Service è composto dai seguenti artefatti:

* **Jar Quickstart**  - Il runtime AEM utilizzato per lo sviluppo locale
* **Java API Jar**  - La dipendenza Java Jar/Maven che espone tutte le API Java consentite che possono essere utilizzate per sviluppare rispetto a AEM come Cloud Service. Precedentemente denominato Uberjar
* **Javadoc Jar**  - I javadocs per Java API Jar
* **Strumenti Dispatcher** : set di strumenti utilizzati per lo sviluppo locale contro Dispatcher. Artefatti separati per unix e finestre

Inoltre, alcuni clienti che sono stati precedentemente distribuiti con AEM 6.5 o versioni precedenti utilizzeranno gli artefatti riportati di seguito. Se la compilazione locale non funziona con il jar Quickstart e si sospetta che sia dovuto a interfacce rimosse da AEM implementate come Cloud Service, contatta l’Assistenza clienti per determinare se hai bisogno di accedere. Ciò richiederà modifiche nel backend.

* **6.5 Java API Jar**  obsoleto - un set aggiuntivo di interfacciati rimosso dalla versione 6.5 di AEM
* **6.5 Javadoc Jar**  obsoleto - i Javadocs per l&#39;ulteriore set di interfacciato

## Creazione per l&#39;SDK {#building-for-the-sdk}

L’SDK AEM as a Cloud Service viene utilizzato per generare e distribuire codice personalizzato. Per ulteriori informazioni, consulta la documentazione [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en). Ad alto livello, vengono eseguiti i seguenti passaggi:

* **Codice di compilazione**. Come previsto, il codice sorgente viene compilato, generando i pacchetti di contenuto risultanti
* **Creare artefatti**. Artifact costruiti durante questo processo
* **Analizza i bundle**. I bundle vengono analizzati utilizzando il plugin Maven analyzer, che cerca problemi nel progetto Maven, come le dipendenze mancanti.
* **Distribuire artefatti**. Gli artifact vengono distribuiti nel server locale.

Gli stessi passaggi vengono eseguiti da Cloud Manager durante la distribuzione in ambienti Cloud. L’esecuzione delle build localmente consente lo sviluppo locale e i test in modo che gli sviluppatori possano individuare in modo efficiente il codice o i problemi strutturali ben prima di impegnarsi nel controllo del codice sorgente e attivare le distribuzioni di Cloud Manager, che possono richiedere più tempo.

## Accesso al AEM come SDK di Cloud Service {#accessing-the-aem-as-a-cloud-service-sdk}

* Puoi controllare l&#39;icona AEM Admin Console **Informazioni su Adobe Experience Manager** per scoprire la versione di AEM in esecuzione in produzione.
* Gli strumenti jar e Dispatcher di quickstart possono essere scaricati come file zip dal [portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html). L’accesso agli elenchi dell’SDK è limitato a quelli con AEM Managed Services o AEM come ambienti di Cloud Service.
* Jar API Java e Javadoc Jar possono essere scaricati tramite strumenti maven, sia dalla riga di comando che con l’IDE preferito.
* I risultati del progetto Maven devono fare riferimento al seguente pacchetto Jar API. È inoltre necessario fare riferimento a questa dipendenza in tutti i programmi dei pacchetti secondari.

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
>La voce della versione per l&#39;SDK deve corrispondere alla versione di AEM come Cloud Service. Per visualizzare la versione in uso, accedi a AEM, quindi vai al punto interrogativo nell&#39;angolo in alto a destra dello schermo e seleziona **[!UICONTROL Informazioni su Adobe Experience Manager]**


## Aggiornamento di un progetto locale con una nuova versione SDK {#refreshing-a-local-project-with-a-new-skd-version}

Quando si consiglia di aggiornare il progetto locale con un nuovo SDK?

È *consigliato* aggiornarlo almeno dopo una versione di manutenzione mensile.

È *facoltativo* aggiornarlo dopo qualsiasi rilascio di manutenzione giornaliera. I clienti verranno informati quando la loro istanza di produzione è stata aggiornata con successo a una nuova versione di AEM. Per le versioni di manutenzione giornaliera, non ci si aspetta che il nuovo SDK sia cambiato in modo significativo, se del caso. Tuttavia, è consigliabile aggiornare occasionalmente l’ambiente di sviluppo AEM locale con l’SDK più recente, quindi ricreare e testare l’applicazione personalizzata. La versione di manutenzione mensile in genere include modifiche di maggiore impatto, pertanto gli sviluppatori devono aggiornare, ricreare e testare immediatamente.

Di seguito è riportata la procedura consigliata per l’aggiornamento di un ambiente locale:

1. Assicurati che eventuali contenuti utili siano impegnati nel progetto nel controllo del codice sorgente o siano disponibili in un pacchetto di contenuti modificabili per un’importazione successiva
1. Il contenuto del test di sviluppo locale deve essere memorizzato separatamente in modo che non venga distribuito come parte della build della pipeline di Cloud Manager. Questo perché deve essere utilizzato solo per lo sviluppo locale
1. Interrompi avvio rapido in esecuzione
1. Sposta la cartella `crx-quickstart` in un&#39;altra cartella per la conservazione sicura
1. Nota la nuova versione AEM, nota in Cloud Manager (verrà utilizzata per identificare la nuova versione di QuickStart Jar da scaricare ulteriormente)
1. Scarica QuickStart JAR la cui versione corrisponde alla versione Production AEM dal portale di distribuzione software
1. Crea una nuova cartella e inserisci il nuovo Jar QuickStart all&#39;interno
1. Avvia il nuovo QuickStart con le modalità di esecuzione desiderate (rinominando il file o passando le modalità di esecuzione tramite `-r`).
   * Assicurati che nella cartella non ci siano residui del vecchio avvio rapido.
1. Creare l&#39;applicazione AEM
1. Distribuire l&#39;applicazione AEM a AEM locali tramite PackageManager
1. Installa tutti i pacchetti di contenuto modificabile necessari per il test dell&#39;ambiente locale tramite PackageManager
1. Continua lo sviluppo e implementa le modifiche in base alle esigenze

Se è presente del contenuto da installare con ogni nuova versione di quickstart AEM, includilo in un pacchetto di contenuti e nel controllo del codice sorgente del progetto. Poi, installalo ogni volta.

Si consiglia di aggiornare frequentemente l’SDK (ad esempio due volte al giorno) e di eliminare ogni giorno lo stato locale completo in modo che non dipenda accidentalmente da dati sullo stato dell’applicazione.

Nel caso in cui tu dipenda da CryptoSupport ([configurando le credenziali di Cloud Services o del servizio di posta SMTP in AEM o utilizzando l&#39;API CryptoSupport nella tua applicazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service-javadoc/com/adobe/granite/crypto/CryptoSupport.html)), le proprietà crittografate saranno crittografate da una chiave che viene generata automaticamente al primo avvio di un ambiente AEM. Mentre il cloud setup si occupa di riutilizzare automaticamente CryptoKey specifico per l&#39;ambiente, è necessario inserire la cryptokey nell&#39;ambiente di sviluppo locale.

Per impostazione predefinita AEM è configurato per memorizzare i dati chiave all&#39;interno della cartella di dati di una cartella, ma per facilitare il riutilizzo nello sviluppo, il processo di AEM può essere inizializzato al primo avvio con &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. In questo modo i dati di crittografia verranno generati in &quot;`/etc/key`&quot;.

Per poter riutilizzare i pacchetti di contenuto contenenti i valori crittografati, segui questi passaggi:

* Quando si avvia inizialmente quickstart.jar locale, assicurarsi di aggiungere il seguente parametro: &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. È consigliabile, ma facoltativo, aggiungerlo sempre.
* La prima volta che hai avviato un&#39;istanza, crea un pacchetto contenente un filtro per la radice &quot;`/etc/key`&quot;. Questo manterrà il segreto da riutilizzare in tutti gli ambienti per i quali si desidera che vengano riutilizzati
* Esporta qualsiasi contenuto modificabile contenente segreti o cerca i valori crittografati tramite `/crx/de` per aggiungerlo al pacchetto che verrà riutilizzato tra le installazioni
* Ogni volta che si avvia una nuova istanza (per sostituire con una nuova versione o come più ambienti di sviluppo devono condividere le credenziali per il test), installare il pacchetto prodotto nei passaggi 2 e 3 per poter riutilizzare il contenuto senza la necessità di riconfigurare manualmente. Questo perché ora la crittografia è sincronizzata.
