---
title: Sviluppare AEM Commerce per AEM as a Cloud Service
description: Scopri come generare un progetto AEM abilitato per il commerce utilizzando l’archetipo di progetto AEM. Scopri come generare e distribuire il progetto in un ambiente di sviluppo locale utilizzando AEM as a Cloud Service SDK.
topics: Commerce, Development
feature: Commerce Integration Framework
version: Experience Manager as a Cloud Service
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
exl-id: 6f28a52b-52f8-4b30-95cd-0f9cb521de62
role: Admin
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 41%

---

# Sviluppare AEM Commerce per AEM as a Cloud Service {#develop}

Lo sviluppo di progetti AEM Commerce, basati su Commerce integration framework (CIF) per AEM as a Cloud Service, segue le stesse regole e best practice di altri progetti AEM su AEM as a Cloud Service. Rivedi prima quanto segue:

- [Struttura dei progetti AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=it)
- [SDK di AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=it)
- [Linee guida per lo sviluppo per AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html)

## Sviluppo locale con AEM as a Cloud Service SDK {#local}

>[!VIDEO](https://video.tv.adobe.com/v/39476/?quality=12&learn=on)

Si consiglia di utilizzare un ambiente di sviluppo locale con progetti CIF. Il componente aggiuntivo CIF fornito per AEM as a Cloud Service è disponibile anche per lo sviluppo locale. Può essere scaricato dal portale di [distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html).

Il componente aggiuntivo CIF viene fornito come archivio di Sling Feature. Il file zip disponibile nel portale di distribuzione software include due file di archivio Sling Feature, uno per l’istanza AEM di authoring e uno per quella di pubblicazione.

**Ti avvicini adesso ad AEM as a Cloud Service?** Consulta [una guida più dettagliata per configurare un ambiente di sviluppo locale utilizzando AEM as a Cloud Service SDK](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview).

### Software richiesto

È necessario installare localmente quanto segue:

- [SDK di AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=it#download-the-aem-as-a-cloud-service-sdk)
- [Java™ 11](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/) (3.3.9 o successivo)
- [Node.js v10+](https://nodejs.org/en)
- [npm 6+](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### Accesso al componente aggiuntivo CIF

Il componente aggiuntivo CIF può essere scaricato come file zip dal [portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html). Il file zip contiene il componente aggiuntivo CIF come **archivio Sling Feature**, non è un pacchetto AEM. Le inserzioni SDK sono accessibili con una licenza AEM as a Cloud Service.

>[!TIP]
>
>Occorre utilizzare sempre la versione più recente del componente aggiuntivo CIF.

### Configurazione locale

Per lo sviluppo locale del componente aggiuntivo CIF utilizzando l’SDK di AEM as a Cloud Service, è necessario procedere seguendo questi passaggi:

1. Scarica il più recente SDK di AEM as a Cloud Service.
1. Decomprimi il file AEM .jar per creare la cartella `crx-quickstart` ed esegui:

   ```bash
   java -jar <jar name> -unpack
   ```

1. Crea una cartella `crx-quickstart/install`.
1. Copia il file di archivio Sling Feature corretto del componente aggiuntivo CIF nella cartella `crx-quickstart/install`.

   Il file ZIP del componente aggiuntivo CIF contiene due file di archivio Sling Feature `.far`. Usa sempre quello corretto per AEM Author o AEM Publish, a seconda di come verrà eseguito l’SDK locale di AEM as a Cloud Service.

1. Creare una variabile di ambiente del sistema operativo locale denominata `COMMERCE_ENDPOINT` contenente l&#39;endpoint Adobe Commerce GraphQL.

   Esempio di macOS X:

   ```bash
   export COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
   ```

   Esempio Windows:

   ```bash
   set COMMERCE_ENDPOINT=https://<yourcommercesystem>/graphql
   ```

   Questa variabile viene utilizzata da AEM per la connessione al sistema commerce. Inoltre, il componente aggiuntivo CIF include un proxy inverso locale per rendere disponibile localmente l’endpoint Commerce GraphQL. Questo proxy viene utilizzato dagli strumenti di authoring di CIF (console prodotti e selettori) e per i componenti lato client di CIF che eseguono chiamate dirette a GraphQL.

   Questa variabile deve essere impostata anche per l’ambiente AEM as a Cloud Service. Per ulteriori informazioni sulle variabili, vedere [Configurazione di OSGi per AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html#local-development).

1. (Facoltativo) Per abilitare le funzioni di catalogo per staging, devi creare un token di integrazione per la tua istanza di Adobe Commerce. Segui i passaggi in [Guida introduttiva](./getting-started.md#staging) per creare il token.

   Imposta un segreto OSGi con il nome `COMMERCE_AUTH_HEADER` sul seguente valore:

   ```xml
   Authorization: Bearer <Access Token>
   ```

   Per ulteriori informazioni sui segreti, vedere [Configurazione di OSGi per AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html#local-development).

1. Avvia l’SDK di AEM as a Cloud Service.

>[!NOTE]
>
>Assicurati di avviare AEM as a Cloud Service SDK nella stessa finestra del terminale in cui è stata impostata la variabile di ambiente al punto 5. Se lo avvii in una finestra del terminale separata o facendo doppio clic sul file .jar, accertati che la variabile di ambiente sia visibile.

Verifica la configurazione tramite la console OSGI:`http://localhost:4502/system/console/osgi-installer`. L’elenco deve includere i bundle relativi al componente aggiuntivo CIF, il pacchetto di contenuti e le configurazioni OSGI come definiti nel file di modello della funzione.

## Configurazione del progetto {#project}

Esistono due modi per Bootstrap il progetto CIF per AEM as a Cloud Service.

### Usare AEM Project Archetype

Il [Archetipo progetto AEM](https://github.com/adobe/aem-project-archetype) è lo strumento principale per Bootstrap un progetto preconfigurato per iniziare a utilizzare CIF. I componenti core CIF e tutte le configurazioni richieste possono essere inclusi in un progetto generato con un’opzione aggiuntiva.

>[!TIP]
>
>Utilizza sempre la versione più recente di [Archetipo progetto AEM](https://github.com/adobe/aem-project-archetype/releases) per generare il progetto.

Consulta le [istruzioni d’uso](https://github.com/adobe/aem-project-archetype#usage) di AEM Project Archetype per la generazione di un progetto AEM. Per includere CIF nel progetto, utilizzare l&#39;opzione `includeCommerce`.

Ad esempio:

```bash
mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate \
 -D archetypeGroupId=com.adobe.aem \
 -D archetypeArtifactId=aem-project-archetype \
 -D archetypeVersion=35 \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D includeCommerce=y
```

I componenti core CIF possono essere utilizzati in qualsiasi progetto includendo il pacchetto `all` fornito o singolarmente utilizzando il pacchetto di contenuti CIF e i bundle OSGI correlati. Per aggiungere manualmente componenti core CIF a un progetto, utilizza le dipendenze seguenti:

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

Una seconda opzione per avviare un progetto CIF è clonare e utilizzare [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia). AEM Venia Reference Store è un esempio di applicazione di vetrina di riferimento che illustra l’utilizzo dei componenti core CIF di AEM. Si tratta di un insieme di esempi di best practice e di un potenziale punto di partenza per sviluppare le tue funzionalità.

Per iniziare a utilizzare Venia Reference Store, clona l’archivio Git e inizia a personalizzare il progetto in base alle tue esigenze.

>[!NOTE]
>
>Il progetto Venia Reference Store contiene due profili di build per AEM as a Cloud Service e AEM 6.5. Controlla il [file readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) del progetto per vedere come vengono utilizzati.

## Risorse aggiuntive

- [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [Portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html)
