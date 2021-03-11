---
title: Sviluppare AEM Commerce per AEM as a Cloud Service
description: Scopri come generare un progetto AEM abilitato per e-commerce utilizzando l’archetipo di progetto AEM. Scopri come creare e distribuire il progetto in un ambiente di sviluppo locale utilizzando l’SDK di AEM come Cloud Service.
topics: Commerce, Development
feature: Commerce Integration Framework
version: cloud-service
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
translation-type: tm+mt
source-git-commit: a9c9a866c03bc15ebddddc7f2086f1f3ffd38a07
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 77%

---


# Sviluppare AEM Commerce per AEM as a Cloud Service {#develop}

Lo sviluppo di progetti AEM Commerce basati su Commerce Integration Framework (CIF) per AEM as a Cloud Service segue le stesse regole e best practice di altri progetti AEM anche su AEM as a Cloud Service. Prima di tutto, consulta i seguenti argomenti:

- [Struttura dei progetti AEM](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)
- [SDK di AEM as a Cloud Service](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html)
- [Linee guida per lo sviluppo per AEM as a Cloud Service](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/developing/development-guidelines.html)

## Sviluppo locale con SDK di AEM as a Cloud Service {#local}

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

Si consiglia di utilizzare un ambiente di sviluppo locale con progetti CIF. Il componente aggiuntivo CIF fornito per AEM come Cloud Service è disponibile anche per lo sviluppo locale. Può essere scaricato dal portale di [distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html).

Il componente aggiuntivo CIF viene fornito come archivio di Sling Feature. Il file zip disponibile nel portale di distribuzione software include due file di archivio Sling Feature, uno per l’istanza AEM di authoring e uno per quella di pubblicazione.

**Ti avvicini adesso ad AEM as a Cloud Service?** Consulta  [una guida più dettagliata per configurare un ambiente di sviluppo locale utilizzando l’SDK](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html) AEM come Cloud Service.

### Software richiesto

È necessario installare localmente quanto segue:

- [SDK di AEM as a Cloud Service](https://docs.adobe.com/content/help/en/*experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 o successivo)
- [Node.js v10+](https://nodejs.org/it/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### Accesso al componente aggiuntivo CIF

Il componente aggiuntivo CIF può essere scaricato come file zip dal [portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). Il file zip contiene il componente aggiuntivo CIF come **archivio Sling Feature**, non è un pacchetto AEM. L’accesso agli elenchi dell’SDK è limitato a quelli con licenza di AEM as a Cloud Service.

>[!TIP]
>
>Occorre utilizzare sempre la versione più recente del componente aggiuntivo CIF.

### Configurazione locale

Per lo sviluppo locale del componente aggiuntivo CIF utilizzando l’SDK di AEM as a Cloud Service, è necessario procedere seguendo questi passaggi:

1. Scarica il più recente SDK di AEM as a Cloud Service.
1. Decomprimi il file AEM.jar per creare la cartella `crx-quickstart` ed esegui:

   ```bash
   java -jar <jar name> -unpack
   ```

1. Crea una cartella `crx-quickstart/install`.
1. Copia il file di archivio Sling Feature corretto del componente aggiuntivo CIF nella cartella `crx-quickstart/install`.

   Il file ZIP del componente aggiuntivo CIF contiene due file di archivio Sling Feature `.far`. Usa sempre quello corretto per AEM Author o AEM Publish, a seconda di come verrà eseguito l’SDK locale di AEM as a Cloud Service.

1. Crea una variabile di ambiente del sistema operativo locale denominata `COMMERCE_ENDPOINT` contenente l’endpoint GraphQL di Magento.

   Esempio Mac OSX:

   ```bash
   export COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   Esempio Windows:

   ```bash
   set COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   Questa variabile viene utilizzata da AEM per connettersi al sistema commerce. Inoltre, il componente aggiuntivo CIF include un proxy inverso locale per rendere disponibile localmente l’endpoint GraphQL di Magento. Viene utilizzato dagli strumenti di authoring CIF (console del prodotto e selettori) e per i componenti CIF lato client che eseguono chiamate GraphQL dirette.

   Questa variabile deve essere impostata anche per l’ambiente di AEM as a Cloud Service. Per ulteriori informazioni sulle variabili, consulta [Configurazione di OSGi per AEM come Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html#local-development).

1. (Facoltativo) Per abilitare le funzioni di catalogo in staging, devi creare un token di integrazione per l’istanza di Magento. Segui i passaggi descritti in [Guida introduttiva](./getting-started.md#staging) per creare il token.

   Imposta un segreto OSGi con il nome `COMMERCE_AUTH_HEADER` al seguente valore:

   ```xml
   Authorization: Bearer <Access Token>
   ```

   Per ulteriori informazioni sui segreti, consulta [Configurazione di OSGi per AEM come Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html#local-development).

1. Avvia l’SDK di AEM as a Cloud Service.

Verifica la configurazione tramite la console OSGI:`http://localhost:4502/system/console/osgi-installer`. L’elenco deve includere i bundle relativi al componente aggiuntivo CIF, il pacchetto di contenuti e le configurazioni OSGI come definiti nel file di modello della funzione.

## Configurazione del progetto {#project}

Esistono due modi per avviare il progetto CIF per AEM as a Cloud Service.

### Usare AEM Project Archetype

Il [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) è lo strumento principale per avviare un progetto preconfigurato con cui iniziare a utilizzare CIF. I componenti core CIF e tutte le configurazioni richieste possono essere inclusi in un progetto generato con un’opzione aggiuntiva.

>[!TIP]
>
>Usa [AEM Project Archetype 24 o versioni successive](https://github.com/adobe/aem-project-archetype/releases) per generare il progetto.

Consulta le [istruzioni d’uso](https://github.com/adobe/aem-project-archetype#usage) di AEM Project Archetype per la generazione di un progetto AEM. Per includere CIF nel progetto, usa l’opzione `includeCommerce`.

Esempio:

```bash
mvn -B archetype:generate \
 -D archetypeGroupId=com.adobe.granite.archetypes \
 -D archetypeArtifactId=aem-project-archetype \
 -D archetypeVersion=24 \
 -D aemVersion=cloud \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D frontendModule=general \
 -D includeExamples=n \
 -D includeCommerce=y
```

I componenti core CIF possono essere utilizzati in qualsiasi progetto includendo il pacchetto fornito `all` o singolarmente utilizzando il pacchetto di contenuti CIF e i relativi bundle OSGI. Per aggiungere manualmente componenti core CIF a un progetto, usa le seguenti dipendenze:

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-config</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-core</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>graphql-client</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>magento-graphql</artifactId>
    <version>x.y.z</version>
</dependency>
```

### Usare AEM Venia Reference Store

Una seconda opzione per avviare un progetto CIF è clonare e utilizzare [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia). AEM Venia Reference Store è un esempio di applicazione di vetrina di riferimento che illustra l’utilizzo dei componenti core CIF di AEM. Si tratta di un insieme di esempi di best practice e di un potenziale punto di partenza che potrai utilizzare per sviluppare le tue funzionalità.

Per iniziare a usare Venia Reference Store, è sufficiente clonare l’archivio Git e iniziare a personalizzare il progetto in base alle proprie esigenze.

>[!NOTE]
>
>Il progetto Venia Reference Store contiene due profili di generazione per AEM as a Cloud Service e AEM 6.5. Controlla il [progetto readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) per vedere come vengono utilizzati.

## Risorse aggiuntive

- [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [Portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)
