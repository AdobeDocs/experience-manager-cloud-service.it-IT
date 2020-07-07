---
title: SDK di AEM as a Cloud Service
description: To be completed
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 1%

---


# The AEM as a Cloud Service SDK {#aem-as-a-cloud-service-sdk}

The AEM as a Cloud Service SDK is comprised of the following artifacts:

* **Quickstart Jar** - Runtime AEM utilizzato per lo sviluppo locale
* **Java API Jar** - The Java Jar/Maven Dependency that exposes all allowed Java APIs that can be used to develop against AEM as as Cloud Service. Formerly referred to as the Uberjar
* **Javadoc Jar** - The javadocs for the Java API Jar
* **Dispatcher Tools** - The set of tools used to develop against Dispatcher locally. Separate artifacts for unix and windows

Inoltre, alcuni clienti che erano stati precedentemente distribuiti con AEM 6.5 o versioni precedenti utilizzeranno gli artifact riportati di seguito. If local compilation is not working with the Quickstart jar and you suspect it is due to interfaces that have been removed from AEM deployed as a Cloud Service, reach out to Customer Support to determine if you need access. This will require changes in the backend.

* **6.5 Deprecated Java API Jar** - an additional set of interfaced that have been removed since AEM 6.5
* **6.5 Deprecated Javadoc Jar** - the Javadocs for the additional set of interfaced

## Accessing the AEM as a Cloud Service SDK {#accessing-the-aem-as-a-cloud-service-sdk}

* You can check the AEM Admin Console&#39;s **About Adobe Experience Manager** icon to find out the version of AEM you are running on production.
* The quickstart jar and Dispatcher Tools can be downloaded as a zip file from the [Software Distribution portal](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html). L&#39;accesso agli elenchi dell&#39;SDK è limitato a quelli con AEM Managed Services o AEM come ambienti Cloud Service.
* The Java API Jar and Javadoc Jar can be downloaded through maven tooling, either command line or with your preferred IDE.
* I promotori del progetto maven devono fare riferimento al seguente pacchetto API Jar. This dependency should also be referenced in any subpackage poms.

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
>The version entry for the SDK should match the version of AEM as a Cloud Service. You can see what version you are using by logging in to AEM, then going to the question mark in the top right corner of the screen and selecting **[!UICONTROL About Adobe Experience Manager]**


## Aggiornamento di un progetto locale con una nuova versione SDK {#refreshing-a-local-project-with-a-new-skd-version}

Quando si consiglia di aggiornare il progetto locale con un nuovo SDK?

È *consigliabile* aggiornarlo almeno dopo una versione di manutenzione mensile.

È *facoltativo* aggiornarlo dopo qualsiasi rilascio giornaliero di manutenzione. I clienti verranno informati quando la loro istanza di produzione verrà aggiornata a una nuova versione di AEM. Per le versioni di manutenzione giornaliera, non è previsto che il nuovo SDK sarà cambiato in modo significativo, se del caso. Still, it is recommended to occasionally refresh the local AEM developer environment with the latest SDK, then rebuild and test the custom application. La versione di manutenzione mensile in genere include modifiche di maggiore impatto e pertanto gli sviluppatori dovrebbero aggiornare, ricreare e testare immediatamente.

Below is the recommended procedure for refreshing a local environment:

1. Make sure that any useful content is either committed to the project in source control or available in a mutable content package for later import
1. Il contenuto del test di sviluppo locale deve essere memorizzato separatamente in modo che non venga distribuito come parte della build della pipeline di Cloud Manager. This is because it only needs to be used for local development
1. Stop the currently running quickstart
1. Spostate la `crx-quickstart` cartella in un&#39;altra cartella per mantenerla sicura
1. Prendete nota della nuova versione di AEM, nota in Cloud Manager (verrà utilizzata per identificare la nuova versione di QuickStart Jar da scaricare ulteriormente in seguito)
1. Scaricate il JAR di avvio rapido la cui versione corrisponde alla versione di AEM di produzione dal portale di distribuzione del software
1. Create una nuova cartella e inserite il nuovo QuickStart Jar all&#39;interno
1. Avviate la nuova Avvio rapido con le modalità di esecuzione desiderate (rinominando il file o passando le modalità di esecuzione tramite `-r`).
   * Accertatevi che nella cartella non rimangano altri collegamenti di avvio rapido.
1. Creare l’applicazione AEM
1. Distribuzione dell’applicazione AEM in AEM locale tramite Package Manager
1. Installate tutti i pacchetti di contenuto modificabile necessari per il test dell&#39;ambiente locale tramite PackageManager
1. Proseguire lo sviluppo e distribuire le modifiche in base alle esigenze

Se è presente del contenuto da installare con ciascuna nuova versione di avvio rapido di AEM, includetelo in un pacchetto di contenuti e nel controllo del sorgente del progetto. Quindi, installatelo ogni volta.

È consigliabile aggiornare frequentemente l&#39;SDK (ad esempio, due volte alla settimana) e smaltire giornalmente lo stato locale completo in modo che non dipenda accidentalmente dai dati sullo stato dell&#39;applicazione.

In case you depend on CryptoSupport ([either by configuring the credentials of Cloudservices or the SMTP Mail service in AEM or by using CryptoSupport API in your application](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/crypto/CryptoSupport.html)), the encrypted properties will be encrypted by a key that is autogenerated on the first start of an AEM environment. While the cloudsetup takes care of automatically reusing the environment-specific CryptoKey, it is necessary to inject the cryptokey into the local development environment.

By default AEM is configured to store the key data within the data folder of a folder, but for convenience of easier reuse in development, the AEM process can be initialized on first startup with &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. This will generate the encryption data at &quot;`/etc/key`&quot;.

To be able to reuse content packages containing the encrypted values you need to follow these steps:

* When you initially start up the local quickstart.jar, make sure to add the below parameter: &quot;`-Dcom.adobe.granite.crypto.file.disable=true`&quot;. It is recommended, but optional, to always add it.
* La prima volta che avete avviato un&#39;istanza create un pacchetto contenente un filtro per la radice &quot;`/etc/key`&quot;. Questo manterrà il segreto per essere riutilizzato in tutti gli ambienti per i quali si desidera che vengano riutilizzati
* Esportate eventuale contenuto modificabile contenente segreti o cercate i valori crittografati tramite `/crx/de` per aggiungerlo al pacchetto che verrà riutilizzato tra le installazioni
* Ogni volta che eseguite il spin up di una nuova istanza (per sostituire una nuova versione o in quanto più ambienti di sviluppo dovrebbero condividere le credenziali per il test), installate il pacchetto prodotto nei passaggi 2 e 3 per poter riutilizzare il contenuto senza dover riconfigurare manualmente. This is because now the cryptokey is in synch.
