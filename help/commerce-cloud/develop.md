---
title: Sviluppare AEM Commerce per AEM as a Cloud Service
description: Sviluppare AEM Commerce per AEM as a Cloud Service
translation-type: tm+mt
source-git-commit: 19fa6391913f556b80607f8dd5215489082b50ab
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 95%

---


# Sviluppare AEM Commerce per AEM as a Cloud Service {#develop}

Lo sviluppo di progetti AEM Commerce basati su Commerce Integration Framework (CIF) per AEM as a Cloud Service segue le stesse regole e best practice di altri progetti AEM anche su AEM as a Cloud Service. Prima di tutto, consulta i seguenti argomenti:

- [Struttura dei progetti AEM](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)
- [SDK di AEM as a Cloud Service](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html)
- [Linee guida per lo sviluppo per AEM as a Cloud Service](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/developing/development-guidelines.html)

## Sviluppo locale con SDK di AEM as a Cloud Service {#local}

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

Si consiglia di utilizzare un ambiente di sviluppo locale con progetti CIF. Il componente aggiuntivo CIF fornito per ambienti AEM as a Cloud Service è disponibile anche per lo sviluppo locale. Può essere scaricato dal portale di [distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html).

Il componente aggiuntivo CIF viene fornito come archivio di Sling Feature. Il file zip disponibile nel portale di distribuzione software include due file di archivio Sling Feature, uno per l’istanza AEM di authoring e uno per quella di pubblicazione.

**Ti avvicini adesso ad AEM as a Cloud Service?** Consulta [una guida più dettagliata sulla configurazione di un ambiente di sviluppo locale tramite l’AEM come SDK](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)di Cloud Service.

### Software richiesto

È necessario installare localmente quanto segue:

- [SDK di AEM as a Cloud Service](https://docs.adobe.com/content/help/en/*experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 o successivo)
- [Node.js v10+](https://nodejs.org/it/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### Accesso al componente aggiuntivo CIF

Il componente aggiuntivo CIF può essere scaricato come file zip dal [portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html). The zip file contains the CIF add-on as **Sling Feature archive**, it is not an AEM package. L’accesso agli elenchi dell’SDK è limitato a quelli con licenza di AEM as a Cloud Service.

>[!TIP]
>
>Occorre utilizzare sempre la versione più recente del componente aggiuntivo CIF.

### Configurazione locale

Per lo sviluppo locale del componente aggiuntivo CIF utilizzando l’SDK di AEM as a Cloud Service, è necessario procedere seguendo questi passaggi:

1. Scarica il più recente SDK di AEM as a Cloud Service.
2. Decomprimi il file AEM.jar per creare la cartella `crx-quickstart` ed esegui:

   ```bash
   java -jar <jar name> -unpack
   ```

3. Crea una cartella `crx-quickstart/install`.
4. Copia il file di archivio Sling Feature corretto del componente aggiuntivo CIF nella cartella `crx-quickstart/install`.

   Il file ZIP del componente aggiuntivo CIF contiene due file di archivio Sling Feature `.far`. Usa sempre quello corretto per AEM Author o AEM Publish, a seconda di come verrà eseguito l’SDK locale di AEM as a Cloud Service.

5. Crea una variabile di ambiente del sistema operativo locale denominata `COMMERCE_ENDPOINT` contenente l’endpoint GraphQL di Magento.

   Esempio Mac OSX:

   ```bash
   export COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   Esempio Windows:

   ```bash
   set COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   Questa variabile deve essere impostata anche per l’ambiente di AEM as a Cloud Service.

6. Avvia l’SDK di AEM as a Cloud Service.

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
- [Portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html)
