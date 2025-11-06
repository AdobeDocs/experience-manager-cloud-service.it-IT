---
title: SDK di AEM as a Cloud Service
description: Panoramica di AEM as a Cloud Service Software Development Kit.
exl-id: 06f3d5ee-440e-4cc5-877a-5038f9bd44c6
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 1%

---

# L’SDK AEM as a Cloud Service {#aem-as-a-cloud-service-sdk}

Il SDK di AEM as a Cloud Service è composto dai seguenti artefatti:

* **Quickstart Jar**: il runtime AEM utilizzato per lo sviluppo locale.
* **Java™ API Jar** - La dipendenza Java™ Jar/Maven che espone tutte le API Java™ consentite che possono essere utilizzate per sviluppare su AEM as a Cloud Service. Precedentemente denominato Uberjar.
* **Jar Javadoc** - Documenti Java per Jar API Java™.
* **Strumenti di Dispatcher**: insieme di strumenti utilizzati per lo sviluppo locale in Dispatcher. Separare gli artefatti per UNIX® e le finestre.

Inoltre, alcuni clienti che sono stati distribuiti in precedenza con AEM 6.5 o versioni precedenti utilizzano gli artefatti riportati di seguito. Se la compilazione locale non funziona con QuickStart Jar e si sospetta che sia dovuta alla rimozione di interfacce da AEM implementato as a Cloud Service, contattare l’Assistenza clienti. Possono determinare se è necessario accedere a. Richiede modifiche nel backend.

* **6.5 Deprecato Java™ API Jar** - Un set aggiuntivo di interfacce che sono state rimosse dopo AEM 6.5.
* **6.5 Deprecato Jar Javadoc** - Documenti Java per il set aggiuntivo di interfacciati.

>[!NOTE]
> 
> Esistono differenze tra AEM as a Cloud Service e SDK in una serie di aree diverse. Per le situazioni in cui sono necessari cambiamenti rapidi e iterativi, Adobe ha introdotto ambienti di sviluppo rapido. Per ulteriori informazioni, consulta [Ambienti di sviluppo rapido](/help/implementing/developing/introduction/rapid-development-environments.md).

## Creazione per SDK {#building-for-the-sdk}

AEM as a Cloud Service SDK viene utilizzato per generare e distribuire il codice personalizzato. Consulta la [documentazione di Archetipo progetto AEM](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/developing/archetype/using). Ad alto livello, vengono eseguiti i seguenti passaggi:

* **Compila codice** - Il codice Source viene compilato e genera i pacchetti di contenuto risultanti.
* **Artefatti di compilazione** - Gli artefatti vengono generati durante questo processo.
* **Analizza bundle** - I bundle vengono analizzati utilizzando il plug-in Maven Analyzer, che cerca problemi nel progetto Maven, ad esempio dipendenze mancanti.
* **Distribuisci artefatti** - Gli artefatti vengono distribuiti nel server locale.

Cloud Manager esegue gli stessi passaggi quando distribuisce in ambienti cloud. L’esecuzione locale delle build consente lo sviluppo e il test locali. Gli sviluppatori possono identificare in modo efficiente il codice o i problemi strutturali prima di passare al controllo del codice sorgente. Questo processo consente di evitare ritardi causati dall’attivazione delle implementazioni di Cloud Manager, che possono richiedere più tempo.

>[!NOTE]
>
>Il SDK di AEM as a Cloud Service deve essere generato con una distribuzione e una versione di Java supportate dall&#39;ambiente di build di [Cloud Manager](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). I clienti AEM as a Cloud Service possono scaricare Oracle JDK dal [portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html). Dispongono del supporto esteso Java 11 fino a settembre 2026 a causa dei termini di licenza e supporto di Adobe per la tecnologia Java Oracle nei progetti Adobe Experience Manager.

## Accesso a AEM as a Cloud Service SDK {#accessing-the-aem-as-a-cloud-service-sdk}

* Puoi controllare l&#39;icona **Informazioni su Adobe Experience Manager** di AEM Admin Console per scoprire la versione di AEM in esecuzione in produzione.
* Gli strumenti Jar e Dispatcher QuickStart possono essere scaricati come file zip dal [portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html). L’accesso agli elenchi di SDK è limitato agli utenti che dispongono di ambienti su AEM Managed Services o AEM as a Cloud Service.
* Il file JAR dell’API Java™ e il file JAR Javadoc possono essere scaricati tramite gli strumenti Maven, tramite la riga di comando o con l’IDE preferito.
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
>La voce di versione per SDK deve corrispondere alla versione di AEM as a Cloud Service. Per vedere quale versione stai utilizzando, accedi ad AEM. Nell&#39;angolo superiore destro della schermata, passare al punto interrogativo e fare clic su **[!UICONTROL Informazioni su Adobe Experience Manager]**.


## Aggiornare un progetto locale con una nuova versione di SDK {#refreshing-a-local-project-with-a-new-skd-version}

Quando si consiglia di aggiornare il progetto locale con un nuovo SDK?

Adobe *consiglia* di aggiornarla dopo una versione di manutenzione mensile.

È *facoltativo* aggiornarlo dopo qualsiasi versione di manutenzione giornaliera. I clienti vengono informati quando la loro istanza di produzione viene aggiornata correttamente a una nuova versione di AEM. Per le versioni di manutenzione giornaliere, non si prevede che il nuovo SDK sia cambiato in modo significativo, se non del tutto. Tuttavia, Adobe consiglia di aggiornare occasionalmente l’ambiente di sviluppo AEM locale con la versione più recente di SDK, quindi di ricreare e testare l’applicazione personalizzata. La versione di manutenzione mensile in genere include modifiche di maggiore impatto e pertanto gli sviluppatori devono immediatamente aggiornare, ricreare e testare.

**Per aggiornare un progetto locale con una nuova versione di SDK:**

1. Assicurati che tutti i contenuti utili siano inseriti nel controllo del codice sorgente. Oppure, memorizzato in un pacchetto di contenuti modificabili per un’importazione successiva.
1. Il contenuto dei test di sviluppo locale deve essere archiviato separatamente in modo che non venga distribuito come parte della build della pipeline di Cloud Manager. Il motivo è che viene usato solo per lo sviluppo locale.
1. Arresta l&#39;avvio rapido in esecuzione.
1. Sposta la cartella `crx-quickstart` in un&#39;altra cartella per la conservazione sicura.
1. Nota la nuova versione di AEM, indicata in Cloud Manager (viene utilizzata per identificare la nuova versione di QuickStart Jar per scaricarla ulteriormente in).
1. Scarica il file JAR QuickStart la cui versione corrisponde a quella di Production AEM dal portale di distribuzione software.
1. Crea una nuova cartella e inserisci il nuovo file JAR QuickStart.
1. Avviare il nuovo QuickStart con le modalità di esecuzione desiderate (rinominando il file o passando in modalità di esecuzione tramite `-r`).
Assicurati che nella cartella non sia presente alcun resto del vecchio modulo quickstart.
1. Crea la tua applicazione AEM.
1. Distribuisci l’applicazione AEM nell’AEM locale tramite Gestione pacchetti.
1. Installa tutti i pacchetti di contenuti mutabili necessari per il test dell’ambiente locale tramite Gestione pacchetti.
1. Continua lo sviluppo e implementa le modifiche necessarie.

Se è necessario installare del contenuto con ogni nuova versione di AEM quickstart, includerlo in un pacchetto di contenuti e nel controllo del codice sorgente del progetto. Quindi, installarlo ogni volta.

Adobe consiglia di aggiornare SDK frequentemente, ad esempio ogni due settimane. Inoltre, elimina tutti i giorni lo stato locale in modo da non dipendere accidentalmente dai dati di stato nell’applicazione.

Se si utilizza CryptoSupport per Cloud Services, la configurazione della posta SMTP o l&#39;API CryptoSupport, le proprietà crittografate vengono protette con una chiave. Ulteriori dettagli sono disponibili nella [documentazione dell&#39;API CryptoSupport](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/crypto/CryptoSupport.html). Questa chiave viene generata automaticamente al primo avvio di un ambiente AEM. Anche se la configurazione cloud si occupa del riutilizzo automatico della CryptoKey specifica per l’ambiente, è necessario inserire la crittografia nell’ambiente di sviluppo locale.

Per impostazione predefinita, AEM è configurato per memorizzare i dati chiave all&#39;interno della cartella dati di una cartella, ma per facilitare il riutilizzo in fase di sviluppo, il processo AEM può essere inizializzato al primo avvio con &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Questo processo genera i dati di crittografia in &quot;`/etc/key`&quot;.

**Per riutilizzare i pacchetti di contenuto contenenti i valori crittografati:**

* Quando avvii il file quickstart.jar locale, assicurati di aggiungere il seguente parametro: &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. Adobe consiglia facoltativamente di aggiungerlo sempre.
* Al primo avvio di un&#39;istanza, creare un pacchetto contenente un filtro per la radice &quot;`/etc/key`&quot;. Questo pacchetto contiene il segreto da riutilizzare in tutti gli ambienti per i quali desideri riutilizzarli.
* Esporta qualsiasi contenuto mutabile contenente segreti. In alternativa, cercare i valori crittografati tramite `/crx/de` in modo da poterli aggiungere al pacchetto riutilizzato in tutte le installazioni.
* Ogni volta che crei una nuova istanza (per sostituirla con una nuova versione o poiché più ambienti di sviluppo devono condividere le credenziali per il test), installa il pacchetto prodotto nei passaggi 2 e 3. In questo modo è possibile riutilizzare il contenuto senza dover riconfigurare manualmente. Il motivo è che ora la crittografia è sincronizzata.

