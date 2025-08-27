---
title: Controllare e abilitare i componenti core Adaptive Forms in AEM Forms as a Cloud Service
description: Scopri come verificare se i componenti core Adaptive Forms sono abilitati e come abilitarli, se necessario, in AEM Forms as a Cloud Service.
contentOwner: Khushwant Singh
docset: CloudService
role: Admin, Developer, User
feature: Adaptive Forms, Core Components
exl-id: 32a574e2-faa9-4724-a833-1e4c584582cf
hide: true
hidefromtoc: true
source-git-commit: 3c1931d67e69d155e777c8761fe2bbbd21461ddf
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 2%

---

# Controllare e abilitare i componenti core adattivi di Forms {#enable-headless-adaptive-forms-on-aem-forms-cloud-service}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/enable-adaptive-forms-core-components.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

I componenti core Adaptive Forms e Headless Adaptive Forms sono già abilitati per la maggior parte dei clienti AEM Forms as a Cloud Service. Questo consente di creare, pubblicare e distribuire su più canali istanze Forms adattivo e Forms headless basate su Componenti core utilizzando le istanze Cloud Service di AEM Forms.

## Verifica se i componenti core Adaptive Forms sono abilitati {#check-if-enabled}

Prima di seguire qualsiasi passaggio di abilitazione, verifica se i componenti core Adaptive Forms sono già abilitati per il tuo ambiente:

### Per i nuovi programmi AEM Forms as a Cloud Service

Quando crei un nuovo programma AEM Forms as a Cloud Service, i componenti core Adaptive Forms e Headless Adaptive Forms sono già abilitati per il tuo ambiente.

### Per gli ambienti Cloud Service esistenti

Se l&#39;ambiente Cloud Service esistente offre l&#39;opzione di [creare Forms adattivo basato su Componenti core](creating-adaptive-form-core-components.md), i componenti core Forms adattivi e il Forms adattivo headless sono già abilitati per l&#39;ambiente.

### Verifica controllando l’archivio

Per verificare che i componenti core Adaptive Forms siano abilitati per il tuo ambiente:

1. Clona l’archivio AEM Forms as a Cloud Service.

1. Apri il file `[AEM Repository Folder]/all/pom.xml` dell&#39;archivio Git di AEM Forms Cloud Service.

1. Cerca le dipendenze seguenti:

   * core-forms-components-af-core
   * core-forms-components-core
   * core-forms-components-apps
   * core-forms-components-af-apps
   * core-forms-components-examples-apps
   * core-forms-components-examples-content

   ![individua l&#39;artefatto core-forms-components-af-core in all/pom.xml](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service-locate-core-af-artifact.png)

   Se queste dipendenze esistono, i Componenti core adattivi di Forms vengono abilitati per il tuo ambiente.

## Quando è necessaria l’abilitazione manuale {#when-manual-enablement-needed}

Solo se disponi di un programma Forms as a Cloud Service precedente in cui i Componenti core non sono abilitati (confermato dal controllo riportato sopra), devi aggiungere manualmente le dipendenze dei Componenti core Adaptive Forms all’archivio AEM as a Cloud Service e distribuire l’archivio negli ambienti Cloud Service.

+++ Passaggi di attivazione manuale 

>[!WARNING]
>
>Segui questi passaggi solo se il controllo di verifica di cui sopra conferma che i Componenti core adattivi di Forms NON sono abilitati per il tuo ambiente.

Per abilitare i componenti core Adaptive Forms e Headless Adaptive Forms per un ambiente AEM Forms as a Cloud Service, effettua le seguenti operazioni, nell’ordine indicato:

![Abilita componenti core e moduli adattivi headless](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service.png)


## &#x200B;1. Clonare l’archivio Git di AEM Forms as a Cloud Service {#clone-git-repository}

1. Accedi a [Cloud Manager](https://my.cloudmanager.adobe.com/) e seleziona la tua organizzazione e il tuo programma.

1. Passa alla scheda **Pipeline** dalla pagina **Panoramica del programma**, quindi fai clic sul pulsante **Accedi a dati archivio** per accedere e gestire il tuo archivio Git. La pagina include le seguenti informazioni:

   * URL dell’archivio Git di Cloud Manager.
   * Credenziali dell’archivio Git (nome utente e password), nome utente Git.

   Fare clic su **Genera password** per visualizzare o generare la password.

1. Aprire il terminale o il prompt dei comandi sul computer locale ed eseguire il comando seguente:

   ```Shell
   git clone [Git Repository URL]
   ```

   Quando richiesto, immettere le credenziali. L&#39;archivio viene clonato nel computer locale.


## &#x200B;2. Aggiungere all’archivio Git le dipendenze dei Componenti core adattivi di Forms {#add-adaptive-forms-core-components-dependencies}

1. Apri la cartella dell’archivio Git in un editor di codice di testo normale. Ad esempio, Codice VS.
1. Apri il file `[AEM Repository Folder]\pom.xml` per la modifica.
1. Sostituire le versioni dei componenti `core.forms.components.version`, `core.forms.components.af.version` e `core.wcm.components.version` con le versioni specificate nella [documentazione dei componenti core](https://github.com/adobe/aem-core-forms-components). Se il componente non esiste, aggiungi questi componenti.

   ```XML
   <!-- Replace the version with the latest released version at https://github.com/adobe/aem-core-forms-components/tags -->
   
   <properties>
       <core.wcm.components.version>2.22.10</core.wcm.components.version>
       <core.forms.components.version>2.0.18</core.forms.components.version>
       <core.forms.components.af.version>2.0.18</core.forms.components.af.version>
   </properties>
   ```

   ![Menzionare la versione più recente dei componenti core di Forms](/help/forms/assets/latest-forms-component-version.png)

1. Nella sezione delle dipendenze del file `[AEM Repository Folder]\pom.xml`, aggiungere le dipendenze seguenti e salvare il file.

   ```XML
       <!-- WCM Core Component Examples Dependencies -->
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.apps</artifactId>
               <type>zip</type>
               <version>${core.wcm.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.content</artifactId>
               <type>zip</type>
               <version>${core.wcm.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.config</artifactId>
               <version>${core.wcm.components.version}</version>
               <type>zip</type>
           </dependency>    
           <!-- End of WCM Core Component Examples Dependencies -->
           <!-- Forms Core Component Dependencies -->
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-core</artifactId>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-apps</artifactId>
               <version>${core.forms.components.version}</version>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-core</artifactId>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-apps</artifactId>
               <version>${core.forms.components.version}</version>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-apps</artifactId>
               <type>zip</type>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-content</artifactId>
               <type>zip</type>
               <version>${core.forms.components.version}</version>
           </dependency>
   <!-- End of AEM Forms Core Component Dependencies -->
   ```

1. Apri il file `[AEM Repository Folder]/all/pom.xml` per la modifica. Aggiungere le dipendenze seguenti nella sezione `<embeddeds>` e salvare il file.

   ```XML
   <!-- WCM Core Component Examples Dependencies -->
   
   <!-- inside plugin config of filevault-package-maven-plugin -->  
   <!-- embed wcm core components examples artifacts -->
   
   <embedded>
       <groupId>com.adobe.cq</groupId>
       <artifactId>core.wcm.components.examples.ui.apps</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.cq</groupId>
       <artifactId>core.wcm.components.examples.ui.content</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.cq</groupId>
       <artifactId>core.wcm.components.examples.ui.config</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <!-- embed forms core components artifacts -->
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-apps</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/application/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-core</artifactId>
       <target>/apps/${appId}-vendor-packages/application/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-examples-apps</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-examples-content</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   ```

   >[!NOTE]
   >
   >
   >  Sostituisci `${appId}` con il tuo appId.
   >
   >  Per trovare `${appId}`, nel file `[AEM Repository Folder]/all/pom.xml`, cerca il termine `-packages/application/install`. Il testo prima del termine `-packages/application/install` è `${appId}`. Il codice seguente, ad esempio, `myheadlessform` è `${appId}`.
   >
   >   ```
   >             <embedded>
   >                     <groupId>com.myheadlessform</groupId>
   >                     <artifactId>myheadlessform.ui.apps<artifactId>
   >                     <type>zip</type>
   >                   <target>/apps/myheadlessform-packages/application install</target>
   >             </embedded>
   >   ```

1. Nella sezione `<dependencies>` del file `[AEM Repository Folder]/all/pom.xml`, aggiungere le dipendenze seguenti e salvare il file:

   ```XML
           <!-- Other existing dependencies -->
           <!-- wcm core components examples dependencies -->
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.apps</artifactId>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.config</artifactId>
               <type>zip</type>
               </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.content</artifactId>
               <type>zip</type>
           </dependency>
               <!-- forms core components dependencies -->
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-apps</artifactId>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-apps</artifactId>
               <type>zip</type>
           </dependency>
               <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-content</artifactId>
               <type>zip</type>
           </dependency>
   ```

1. Apri `[AEM Repository Folder]/ui.apps/pom.xml` per la modifica. Aggiungere la dipendenza `af-core bundle` e salvare il file.

   ```XML
       <dependency>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-core</artifactId>
       </dependency>
   ```

   >[!NOTE]
   >
   >Assicurati che i seguenti artefatti dei Componenti core adattivi di Forms non siano inclusi nel progetto.
   >
   > `<dependency>`
   >
   >   `<groupId>com.adobe.aem</groupId>`
   >   `<artifactId>core-forms-components-apps</artifactId>`
   >
   > `</dependency>`
   >
   > e
   >
   > `<dependency>`
   >
   >   `<groupId>com.adobe.aem</groupId>`
   >   `<artifactId>core-forms-components-core</artifactId>`
   >
   > `</dependency>`


1. Salva e chiudi il file.

## &#x200B;3. Genera e distribuisci il codice aggiornato

Distribuisci il codice aggiornato negli ambienti di sviluppo locali e Cloud Service per abilitare i Componenti core in entrambi gli ambienti:

* [Generare e distribuire il codice aggiornato in un ambiente di sviluppo locale (AEM as a Cloud Service SDK)](#core-components-on-aem-forms-local-sdk)

* [Creare e distribuire il codice aggiornato in un ambiente AEM Forms as a Cloud Service](#core-components-on-aem-forms-cs)

### Generare e distribuire il codice aggiornato in un ambiente di sviluppo locale {#core-components-on-aem-forms-local-sdk}

1. Apri il prompt dei comandi o il terminale.

1. Passa alla directory principale del progetto dell’archivio Git.

1. Esegui il seguente comando per generare il pacchetto per il tuo ambiente:

   ```Shell
       mvn clean install
   ```



   Una volta creato correttamente il pacchetto, puoi trovarlo nella [cartella dell&#39;archivio Git]\all\target\[appid].all-[versione].zip

1. Utilizza [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=it) per distribuire il pacchetto [Cartella di progetto Archetipo AEM]\all\target\[appid].all-[versione].zip nell&#39;ambiente di sviluppo locale.


### Creare e distribuire il codice aggiornato in un ambiente AEM Forms as a Cloud Service {#core-components-on-aem-forms-cs}

1. Aprire il terminale o il prompt dei comandi.
1. Passa a `[AEM Repository Folder]` ed esegui i seguenti comandi nell&#39;ordine elencato

   ```Shell
    git add pom.xml
    git add all/pom.xml
    git add ui.apps/pom.xml
    git commit -m "Added dependencies for Adaptive Forms Core Components"
    git push origin
   ```

1. Dopo il commit dei file nell&#39;archivio Git, [Esegui la pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=it).

   Una volta completata l’esecuzione della pipeline, i componenti core Adaptive Forms vengono abilitati per l’ambiente corrispondente. Inoltre, all’ambiente Forms as a Cloud Service vengono aggiunti un modello Forms adattivo (Componenti core) e un tema Canvas 3.0, che offrono opzioni per personalizzare e creare componenti core basati su Adaptive Forms.

+++

## Domande frequenti {#faq}

### Cosa sono i Componenti core? {#core-components}

I [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) sono un insieme di componenti WCM (Web Content Management) standardizzati di AEM che consentono di velocizzare i tempi di sviluppo e ridurre i costi di manutenzione dei siti Web.

### Quali sono tutte le funzionalità aggiunte all’abilitazione dei componenti core? {#core-components-capabilities}

Quando i componenti core Adaptive Forms sono abilitati per il tuo ambiente, all’ambiente vengono aggiunti un modello di modulo adattivo basato su Componenti core vuoto e un tema Canvas 3.0. Dopo aver abilitato i componenti core Forms adattivi per il tuo ambiente, puoi:

* [Creazione di componenti core basati su Forms adattivo](/help/forms/creating-adaptive-form-core-components.md).
* [Creare modelli di modulo adattivo basati su componenti core](/help/forms/template-editor.md).
* [Creare temi personalizzati per i modelli di modulo adattivo basati su Componenti core](/help/forms/using-themes-in-core-components.md).
* [Distribuisci le rappresentazioni JSON del modulo adattivo basate su Componente core a canali quali dispositivi mobili, web, app native e servizi che richiedono la rappresentazione headless di un modulo](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=it).

### Come posso sapere se devo abilitare manualmente i componenti core di Forms adattivi? {#manual-enablement-needed-faq}

La maggior parte dei clienti dispone già di componenti core Adaptive Forms abilitati. È necessario abilitarli manualmente solo se:

1. Hai un programma Forms as a Cloud Service precedente creato prima che i Componenti core venissero inclusi automaticamente
1. Il controllo di verifica nella sezione [Verifica se i componenti core adattivi di Forms sono abilitati](#check-if-enabled) conferma che le dipendenze richieste non sono presenti nell&#39;archivio

In caso di dubbi, segui i passaggi di verifica descritti nella sezione precedente [Verifica se i componenti core adattivi di Forms sono abilitati](#check-if-enabled).

### Perché i moduli basati su Componenti core non vengono riprodotti nel progetto?

Il rendering dei moduli basati su Componenti core potrebbe non riuscire a causa di una mancata corrispondenza tra la versione del pacchetto dei Componenti core di Forms e quella inclusa nell’archetipo del progetto. Questo problema si verifica in genere quando la versione specificata nell’archetipo del progetto è uguale o superiore alla versione inclusa nel pacchetto dei Componenti core di Forms. Per risolvere il problema, eseguire una delle operazioni seguenti:

* Utilizza una versione inferiore del pacchetto dei Componenti core di Forms nell’archetipo del progetto.
* Rimuovi la dipendenza dai Componenti core Forms dall’archetipo del progetto, in quanto la versione richiesta è già inclusa in AEM as a Cloud Service. Il pacchetto dei Componenti core Forms è incluso con AEM as a Cloud SDK a partire dalla versione 20133, ad esempio `AEM SDK v2025.3.20133.20250325T063357Z-250300`.

>[!MORELIKETHIS]
>
>* [Creare un modulo adattivo](/help/forms/creating-adaptive-form-core-components.md)
