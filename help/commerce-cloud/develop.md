---
title: Sviluppare AEM Commerce per AEM come Cloud Service
description: Sviluppare AEM Commerce per AEM come Cloud Service
translation-type: tm+mt
source-git-commit: e30086c546d9efcc1da07ac5862c012a0db02c09
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 10%

---


# Sviluppare AEM Commerce per AEM come Cloud Service {#develop}

Lo sviluppo di progetti AEM Commerce basati su Commerce Integration Framework (CIF) per AEM come Cloud Service segue le stesse regole e le migliori prassi come altri progetti AEM su AEM come Cloud Service. Prima di tutto, consulta i seguenti argomenti:

- [Struttura dei progetti AEM](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)
- [SDK di AEM as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html)
- [Linee guida per lo sviluppo per AEM as a Cloud Service](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/developing/development-guidelines.html)

## Sviluppo locale con AEM come SDK Cloud Service {#local}

Si raccomanda di utilizzare un ambiente di sviluppo locale con progetti CIF. Il componente aggiuntivo CIF fornito per AEM come ambienti di Cloud Service è disponibile anche per lo sviluppo locale. Può essere scaricato dal portale [Distribuzione](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html)software.

Il componente aggiuntivo CIF viene fornito come archivio delle funzioni Sling. Il file zip disponibile nel portale di distribuzione software include due file di archivio Sling Feature, uno per AEM autore e uno per AEM istanze di pubblicazione.

**Per AEM come Cloud Service?** Consulta la [seguente guida per configurare un ambiente di sviluppo locale utilizzando il AEM come SDK](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)di Cloud Service.

### Software richiesto

È necessario installare localmente quanto segue:

- [SDK di AEM as a Cloud Service](https://docs.adobe.com/content/help/en/*experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#download-the-aem-as-a-cloud-service-sdk)
- [Java 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 o successivo)
- [Node.js v10+](https://nodejs.org/en/)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### Accesso al componente aggiuntivo CIF

The CIF add-on can be downloaded as a zip file from the [Software Distribution portal](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html). Il file zip contiene il componente aggiuntivo CIF come archivio Sling Feature, non è un pacchetto AEM. L&#39;accesso agli elenchi dell&#39;SDK è limitato a quelli con AEM come licenza di Cloud Service.

>[!TIP]
>
>Accertatevi di utilizzare sempre la versione CIF più recente del componente aggiuntivo.

### Configurazione locale

Per lo sviluppo locale CIF Add-on utilizzando l&#39;AEM come SDK di Cloud Service, procedere come segue:

1. Ottenere la AEM più recente come SDK di Cloud Service
2. Per creare la `crx-quickstart` cartella, decomprimete il file .jar AEM ed eseguite:

   ```bash
   java -jar <jar name> -unpack
   ```

3. Create a `crx-quickstart/install` folder
4. Copiate il file di archivio Sling Feature corretto del componente aggiuntivo CIF nella `crx-quickstart/install` cartella.

   Il file ZIP CIF del componente aggiuntivo contiene due `.far` file di archivio Sling Feature. Accertatevi di usare quello corretto per AEM Author o AEM Publish, a seconda di come intendete eseguire la AEM locale come Cloud Service SDK.

5. Create una variabile di ambiente del sistema operativo locale denominata `COMMERCE_ENDPOINT` contenente l&#39;endpoint GraphQL del Magento.

   Esempio Mac OSX:

   ```bash
   export COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   Esempio di finestre:

   ```bash
   set COMMERCE_ENDPOINT=https://demo.magentosite.cloud/graphql
   ```

   Questa variabile deve essere impostata anche per il AEM come ambiente Cloud Service.

6. Avviare il AEM come SDK di Cloud Service

Verificare la configurazione tramite la console OSGI:`http://localhost:4502/system/console/osgi-installer`. L&#39;elenco deve includere i bundle CIF del componente aggiuntivo, il pacchetto di contenuti e le configurazioni OSGI come definiti nel file del modello di feature.

## Configurazione progetto {#project}

Esistono due modi per avviare il progetto CIF per AEM come Cloud Service.

### Usa AEM tipo di archivio del progetto

Il [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) è lo strumento principale per avviare un progetto preconfigurato per iniziare a utilizzare CIF. CIF I componenti core e tutte le configurazioni richieste possono essere inclusi in un progetto generato con un&#39;opzione aggiuntiva.

>[!TIP]
>
>Utilizzate [AEM Project Archetype 24 o successivo](https://github.com/adobe/aem-project-archetype/releases) per generare il progetto.

Consultate AEM [Istruzioni](https://github.com/adobe/aem-project-archetype#usage) sull&#39;uso del tipo di archivio del progetto per la generazione di un progetto AEM. Per includere CIF nel progetto utilizzate l&#39; `includeCommerce` opzione.

Ad esempio:

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

CIF I componenti di base possono essere utilizzati in qualsiasi progetto includendo il `all` pacchetto fornito o singolarmente utilizzando il pacchetto di contenuti CIF e i relativi bundle OSGI. Per aggiungere manualmente i componenti CIF di base a un progetto, utilizzate le seguenti dipendenze:

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

### Usa AEM Venia Reference Store

Una seconda opzione per avviare un progetto CIF è duplicare e utilizzare il negozio [di riferimento di](https://github.com/adobe/aem-cif-guides-venia)Venia. AEM Venia Reference Store è un esempio di applicazione di riferimento storefront che illustra l&#39;utilizzo di componenti CIF di base per AEM. Si tratta di un insieme di esempi di best practice e di un potenziale punto di partenza per sviluppare le proprie funzionalità.

Per iniziare con Venia Reference Store basta clonare il repository Git e iniziare a personalizzare il progetto in base alle vostre esigenze.

>[!NOTE]
>
>Il progetto Venia Reference Store contiene due profili di build per AEM come Cloud Service e AEM 6.5. Controlla il [progetto readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) per vedere come vengono utilizzati.

## Risorse aggiuntive

- [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [Portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html)
