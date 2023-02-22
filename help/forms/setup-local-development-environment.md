---
title: Configurare un ambiente di sviluppo locale per Adobe Experience Manager Forms as a Cloud Service
description: Configurare un ambiente di sviluppo locale per Adobe Experience Manager Forms as a Cloud Service
exl-id: 12877a77-094f-492a-af58-cffafecf79ae
source-git-commit: 55a53f23ee81877bd3a6ba3b9b0a1c3c98edb764
workflow-type: tm+mt
source-wordcount: '2960'
ht-degree: 2%

---

# Creare un ambiente di sviluppo locale e un progetto di sviluppo iniziale {#overview}

Quando configuri e configuri un [!DNL  Adobe Experience Manager Forms] come [!DNL  Cloud Service] ambiente, puoi configurare ambienti di sviluppo, staging e produzione su cloud. Inoltre, puoi anche configurare un ambiente di sviluppo locale.

È possibile utilizzare l’ambiente di sviluppo locale per eseguire le azioni seguenti senza accedere all’ambiente di sviluppo cloud:

* [Creazione di moduli](creating-adaptive-form.md) e risorse correlate (temi, modelli, azioni di invio personalizzate e altro)
* [Conversione di moduli PDF in moduli adattivi](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html?lang=it)
* Creare applicazioni da generare [Comunicazioni dei clienti](aem-forms-cloud-service-communications-introduction.md) su richiesta o in modalità batch.

Dopo che un Modulo adattivo o le risorse correlate sono pronte nell’istanza di sviluppo locale o in un’applicazione per generare [Comunicazioni dei clienti] è pronto, puoi esportare l’applicazione Moduli adattivi o Comunicazioni cliente dall’ambiente di sviluppo locale a un ambiente di Cloud Service per ulteriori test o per il passaggio ad ambienti di produzione.

Puoi anche sviluppare e testare codice personalizzato come componenti personalizzati e servizio di precompilazione nell’ambiente di sviluppo locale. Quando il codice personalizzato è testato e pronto, puoi utilizzare l’archivio Git dell’ambiente di sviluppo del Cloud Service per distribuire il codice personalizzato.

Per impostare un nuovo ambiente di sviluppo locale e utilizzarlo per lo sviluppo per le attività, esegui le seguenti azioni nell’ordine elencato:

* [Impostare strumenti di sviluppo](#setup-development-tools-for-AEM-projects)

* [Configurare istanze Author e Publish locali](#set-up-local-experience-manager-environment-for-development)

* [Aggiungi archivio Forms alle istanze di sviluppo locali e configura gli utenti](#add-forms-archive-configure-users)

* [Configurare l&#39;ambiente di sviluppo locale per i microservizi](#docker-microservices)

* [Configurare un progetto di sviluppo](#forms-cloud-service-local-development-environment)

* [Configurare gli strumenti del Dispatcher locale](#setup-local-dispatcher-tools)

<!--
You can use the local development environment to create and test Adaptive Forms without connecting to the Cloud Service. [!DNL AEM Forms] provides an SDK to help test all the cloud-ready functionalities on the local development environment. When your forms and related assets are ready and tested on the local development environment, you can import these forms and related assets to an [!DNL AEM Forms] as a Cloud Service instance for publishing. 

You can also develop and test custom code like custom components and prefill service on the local development environment. When the custom code is tested and ready, you can use the Git repository of your [!DNL AEM Forms] as a Cloud Service development environment to deploy the custom code. 

>[!NOTE]
>
> Pre-pilot release does not support using an [!DNL AEM Forms] as a Cloud Service development instance to create forms. You can create forms, related assets, and custom code only on a local development environment.-->

<!--
You configure two types of development environments:

* **[!DNL AEM Forms] as a Cloud Service development environment:** Use the [[!DNL AEM Forms] as a Cloud Service](setup-forms-cloud-service.md) environment to store, manage, and publish Adaptive Forms and related assets. Do not use an [!DNL AEM Forms] as a Cloud Service environment to create Adaptive Forms and related assets <!--, form-centric workflows, a form data model, or to generate a Document of Record. -->

<!--
* **Local development environment:** You can use the local development environment to create and test Adaptive Forms without connecting to the service. Adobe provides a SDK for the local development to help test all the cloud-ready functionalities. 
Use a local development environment:
    
    * To create forms and related assets (themes, templates, custom Submit Actions, and more) and convert PDF forms to Adaptive Forms. After an Adaptive Form or related assets are ready on the local development instance, you can export the Adaptive Form and related assets from the local development environment to an [!DNL AEM Forms] as a Cloud Service development environment for publishing.  
    
    * To update configuration settings and develop and test custom code like custom components and prefill service. When the custom code is tested and ready, you can use the Git repository of your [!DNL AEM Forms] as a Cloud Service development environment to deploy the custom code.  

You can use the local development environment to create and test Adaptive Forms without connecting to the service. Adobe provides a SDK for the local development to help test all the cloud-ready functionalities. When your forms and related assets are ready and tested on the local development environment, you can import these forms and related assets to an [!DNL AEM Forms] as a Cloud Service instance for publishing. 

You can use the [development tools](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/dev-tools.html) to write custom code, customize or create new Adaptive Forms components, create a custom prefill service, or modify default configurations of an [!DNL AEM Forms] as a Cloud Service instance. 

-->

## Prerequisiti

Per configurare un ambiente di sviluppo locale è necessario disporre del software seguente. Scarica questi prima di iniziare a configurare l’ambiente di sviluppo locale:

| Software | Descrizione | Collegamenti di download |
|---|---|---|
| Adobe Experience Manager as a Cloud Service SDK | L&#39;SDK include [!DNL Adobe Experience Manager] Strumenti QuickStart e Dispatcher | Scarica l&#39;SDK più recente da [Distribuzione di software](#software-distribution) |  |
| Archivio delle funzioni di Adobe Experience Manager Forms (componente aggiuntivo di AEM Forms) | Strumenti per creare, personalizzare lo stile e ottimizzare Adaptive Forms e altre funzionalità di Adobe Experience Manager Forms | Scarica da [Distribuzione di software](#software-distribution) |
| (Facoltativo) Contenuto di riferimento di Adobe Experience Manager Forms | Strumenti per creare, personalizzare lo stile e ottimizzare Adaptive Forms e altre funzionalità di Adobe Experience Manager Forms | Scarica da [Distribuzione di software](#software-distribution) |
| (Facoltativo) Adobe Experience Manager Forms Designer | Strumenti per creare, personalizzare lo stile e ottimizzare Adaptive Forms e altre funzionalità di Adobe Experience Manager Forms | Scarica da [Distribuzione di software](#software-distribution) |

### Scarica la versione più recente del software da Distribuzione di software {#software-distribution}

Per scaricare la versione più recente dell’SDK Adobe Experience Manager as a Cloud Service, l’archivio delle funzioni di Experience Manager Forms (componente aggiuntivo di AEM Forms), le risorse di riferimento dei moduli o Forms Designer da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html):

1. Accedi a <https://experience.adobe.com/#/downloads> con il tuo Adobe ID

   >[!NOTE]
   >
   > Per scaricare l’SDK as a Cloud Service AEM, è necessario eseguire il provisioning dell’organizzazione Adobe per AEM as a Cloud Service.

1. Passa a **[!UICONTROL AEM as a Cloud Service]** scheda .
1. Ordina per data pubblicata in ordine decrescente.
1. Fai clic sull’SDK Adobe Experience Manager as a Cloud Service più recente, sull’archivio delle funzioni di Experience Manager Forms (componente aggiuntivo per AEM Forms), sulle risorse di riferimento dei moduli o su Forms Designer.
1. Rivedere e accettare l&#39;EULA. Tocca **[!UICONTROL Scarica]** pulsante .

## Impostare strumenti di sviluppo per progetti AEM {#setup-development-tools-for-AEM-projects}

Il progetto Adobe Experience Manager Forms è una base di codice personalizzata. Contiene codice, configurazioni e contenuti distribuiti tramite Cloud Manager su [!DNL Adobe Experience Manager] as a Cloud Service. La [Archetipo AEM progetto Maven](https://github.com/adobe/aem-project-archetype) fornisce la struttura di base per il progetto.

Imposta i seguenti strumenti di sviluppo da utilizzare per [!DNL Adobe Experience Manager] progetto di sviluppo:

* [Java™](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#local-development-environment-set-up)
* [Git](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#install-git)
* [Node.js (npm)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#node-js)
* [Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#install-maven)

Per istruzioni dettagliate su come impostare gli strumenti di sviluppo precedentemente menzionati, vedi [Impostare strumenti di sviluppo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html).

## Configurare l&#39;ambiente di Experience Manager locale per lo sviluppo

L&#39;SDK del Cloud Service fornisce un file QuickStart. Esegue una versione locale dell&#39;Experience Manager. Puoi eseguire localmente le istanze Author o Publish .

Mentre QuickStart fornisce un&#39;esperienza di sviluppo locale, non dispone di tutte le funzioni disponibili in [!DNL Adobe Experience Manager] as a Cloud Service. Quindi, verifica sempre le tue funzioni e codifica con [!DNL Adobe Experience Manager] Ambiente di sviluppo as a Cloud Service prima di spostare le funzioni in stage o produzione.

Per installare e configurare l’ambiente di Experience Manager locale, effettua le seguenti operazioni:

* [Scarica ed estrai](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html) la [!DNL Adobe Experience Manager] SDK as a Cloud Service
* [Configurare un’istanza di authoring](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en#set-up-local-aem-author-service)
* [Configurare un&#39;istanza Publish](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en#set-up-local-aem-publish-service)

## Aggiungere l’archivio Forms alle istanze Author e Publish locali e configurare gli utenti specifici di Forms {#add-forms-archive-configure-users}

Esegui i seguenti passaggi nell’elenco per aggiungere l’archivio Forms alle istanze di Experience Manager e configurare gli utenti specifici per i moduli:

### Installare l’archivio delle funzioni aggiuntive più recente di Forms {#add-forms-archive}

L’archivio delle funzioni as a Cloud Service di Adobe Experience Manager Forms fornisce gli strumenti per creare, personalizzare lo stile e ottimizzare Adaptive Forms nell’ambiente di sviluppo locale. Installa il pacchetto per creare un modulo adattivo e utilizza varie altre funzioni di [!DNL AEM Forms]. Per installare il pacchetto:

1. Scarica ed estrai l&#39;ultima [!DNL AEM Forms] archiviare il sistema operativo da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html).

1. Passa alla directory crx-quickstart/install . Se la cartella non esiste, creala.

1. Interrompi l&#39;istanza AEM, posiziona il [!DNL AEM Forms] archivio di funzionalità aggiuntive, `aem-forms-addon-<version>.far`, nella cartella di installazione e riavvia l’istanza.

### Configurare utenti e autorizzazioni {#configure-users-and-permissions}

Creare utenti come sviluppatore di moduli e sviluppatore di moduli e [aggiungere questi utenti a gruppi di moduli predefiniti](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=en#accessing) per fornire loro le autorizzazioni necessarie. Nella tabella seguente sono elencati tutti i tipi di utenti e i gruppi predefiniti per ciascun tipo di utente dei moduli:

| Tipo di utente | Gruppo AEM |
|---|---|
| Professionista / | [!DNL forms-users] (Utenti AEM Forms), [!DNL template-authors], [!DNL workflow-users], [!DNL workflow-editors]e [!DNL fdm-authors] |
| Sviluppatore di moduli | [!DNL forms-users] (Utenti AEM Forms), [!DNL template-authors], [!DNL workflow-users], [!DNL workflow-editors]e [!DNL fdm-authors] |
| Customer Experience Lead o UX Designer | [!DNL forms-users], [!DNL template-authors] |
| Amministratore AEM | [!DNL aem-administrators], [!DNL fd-administrators] |
| Utente finale | Quando un utente deve effettuare l’accesso per visualizzare e inviare un modulo adattivo, aggiungi tali utenti a [!DNL forms-users] gruppo. </br> Se non è richiesta alcuna autenticazione utente per accedere a Adaptive Forms, non assegnare alcun gruppo a tali utenti. |

<!--  

## Set up a local AEM instance for development

Perform the following steps in the listed order to set up and configure your local development environment:

1. **Set up an AEM author instance:** You require an author instance to create Adaptive Forms. Download and extract the latest AEM SDK archive. Run the quick start file in author run mode to set up an author instance. For detailed instructions, see [default local instance](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html).  

1. **Install the latest [!DNL AEM Forms] add-on feature archive:** [!DNL AEM Forms] add-on feature archive provides tools to create, style, and optimize Adaptive Forms on the local development environment. Install the package to create an Adaptive Form and use various other features of [!DNL AEM Forms]. To install the package:

    1. Download and extract the latest [!DNL AEM Forms] archive for your operating system from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

    1. Navigate to the crx-quickstart/install directory. If the folder does not exist, create it.

    1. Stop your Cloud ready AEM instance, place the [!DNL AEM Forms] add-on feature archive, `aem-forms-addon-<version>.far`,  in the install folder, and restart the instance.

1. **Configure users and permissions:** Create users like Form Developer and Form Practitioner a nd add these users to pre-defined forms group to provide them required permissions. The table below lists all types of users and pre-defined groups for each type of forms users:
  
    | User Type | AEM Group |
    |---|---|
    | Form Practitioner  | forms-users (AEM Forms Users), template-authors  |
    | Form Developer | forms-users (AEM Forms Users), template-authors |
    | End-User| everyone* |

    `*` When a user should log in to access or submit Adaptive Forms, add such users to the everyone group.  -->

<!--    
### Set up an AEM project for the development tasks related to local AEM 6.5.5 Forms instance

Use this project to update configurations, create overlays, develop custom Adaptive Form components, and custom code using the local development environment. To set up the project:

1. **Install and configure Maven and set up an AEM project based on Apache Maven:** Apache Maven is an open-source tool for managing software projects. It helps automate builds and provides quality project information. It is the recommended build management tool for AEM projects. For detailed instructions to set up an AEM project based on Apache Maven, see [How to Build AEM Projects using Apache Maven](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/ht-projects-maven.html).

1. Configure the project to use [uber-jar](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=en#install-aem-forms-jee-installer) version 6.5.5 or later and [[!DNL AEM Forms] Client SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/) version 6.0.160 or later.  

1. **Set Up an Integrated Development Environment:**  Set up an IDE of your choice for development, see [Set Up an Integrated Development Environment](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) for detailed instructions.
 -->

## Configurare l&#39;ambiente di sviluppo locale per Document of Record (DoR){#docker-microservices}

AEM Forms as a Cloud Services offre un ambiente SDK basato su docker per uno sviluppo più semplice di Document of Record e per l’utilizzo di altri microservizi. Consente di configurare manualmente i binari e le adattazioni specifici per la piattaforma. Per configurare l’ambiente:

1. Installa e configura Docker:

   * (Per Microsoft® Windows) Installa [Docker Desktop](https://www.docker.com/products/docker-desktop). Configura `Docker Engine` e `docker-compose` sulla tua macchina.

   * (Apple macOS) Installa [Docker Desktop per Mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac). Include Docker Engine, Docker CLI client, Docker Compose, Docker Content Trust, Kubernetes e Credential Helper.

   * (Per Linux®) Installazione [Motore Docker](https://docs.docker.com/engine/install/#server) e [Composizione Docker](https://docs.docker.com/compose/install/) sulla tua macchina.
   >[!NOTE]
   >
   > * Per Apple macOS, inserire nell&#39;elenco Consentiti cartelle contenenti istanze AEM Author locali.
   >
   > * Docker Desktop per Windows supporta due backend, Hyper-V
      > (legacy) e WSL2 (moderna). La condivisione dei file viene eseguita automaticamente
      > gestito da Docker quando si utilizza WSL2 (moderno). Devi
      > configura esplicitamente la condivisione dei file durante l’utilizzo di Hyper-V (legacy).


1. Crea una cartella, ad esempio aem-sdk, in parallelo alle istanze di authoring e pubblicazione. Ad esempio C:\aem-sdk.

1. Estrai il `aem-forms-addon-<version>.zip\aem-forms-addon-native-<version>.zip` file.

   ![aggiunta aem forms estratta su nativa](assets/microservice-docker.png)

1. Crea una variabile di ambiente AEM_HOME e puntale all’installazione locale di AEM Author. Ad esempio C:\aem\author\.

1. Apri sdk.bat o sdk.sh per la modifica. Imposta AEM_HOME per puntare all’installazione locale di AEM Author. Ad esempio C:\aem\author\.

1. Apri il prompt dei comandi e passa alla `aem-forms-addon-native-<version>` cartella.

1. Assicurati che l’istanza locale di AEM Author sia attiva e in esecuzione. Esegui il seguente comando per avviare l&#39;SDK:

   * (su Microsoft® Windows) `sdk.bat start`
   * (su Linux® o Apple macOS) `AEM_HOME=[local AEM Author installation] ./sdk.sh start`

   >[!NOTE]
   >
   > Se hai definito la variabile di ambiente nel file sdk.sh, specificarla nella riga di comando è facoltativa. L&#39;opzione per definire la variabile di ambiente alla riga di comando viene fornita per eseguire il comando senza aggiornare lo script della shell.

   ![start-sdk-command](assets/start-sdk.png)

È ora possibile utilizzare l&#39;ambiente di sviluppo locale per eseguire il rendering del documento di record. Per eseguire il test, carica un file XDP nel tuo ambiente ed eseguine il rendering. Ad esempio: <http://localhost:4502/libs/xfaforms/profiles/default.print.pdf?template=crx:///content/dam/formsanddocuments/cheque-request.xdp> converte il file XDP nel documento PDF.

## Imposta un progetto di sviluppo per Forms basato su archetipo di Experience Manager {#forms-cloud-service-local-development-environment}

Utilizza questo progetto per creare Adaptive Forms, distribuire aggiornamenti di configurazione, sovrapposizioni, creare componenti modulo adattivo personalizzati, testare e codice personalizzato in locale [!DNL Experience Manager Forms] SDK. Dopo il test locale, puoi distribuire il progetto in  [!DNL Experience Manager Forms] Ambienti di produzione e non di produzione as a Cloud Service. Quando distribuisci il progetto, vengono anche distribuite le seguenti risorse AEM Forms:

| Temi | Modelli | Modelli dati modulo |
---------|----------|---------
| Area di lavoro 3.0 | Base | Microsoft® Dynamics 365 |
| Tranquillo | Vuoto | Salesforce |
| Urbane |  |  |
| Ultramarina |  |  |
| Berile |  |  |

>[!NOTE]
>
> Imposta AEM progetto basato su Archetype versione 30 o successiva per ottenere e utilizzare i modelli di dati dei moduli Microsoft® Dynamics 365 e Salesforce con AEM Forms as a Cloud Service.
Imposta AEM Archetype versione 32 o successiva per ottenere e utilizzare i temi Tranquil, Urbane e Ultramarine con AEM Forms as a Cloud Service.

Per impostare il progetto:

1. **Clona l’archivio Git di Cloud Manager nella tua istanza di sviluppo locale:**  L’archivio Git di Cloud Manager contiene un progetto AEM predefinito. Si basa su [Archetipo AEM](https://github.com/adobe/aem-project-archetype/). Clona il tuo archivio Git di Cloud Manager utilizzando Self-Service Git Account Management dall’interfaccia utente di Cloud Manager per portare il progetto nell’ambiente di sviluppo locale. Per informazioni dettagliate sull&#39;accesso all&#39;archivio, vedi [Accesso agli archivi](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html).

<!-- 1. 
After the repository is cloned, [integrate your Git repo with Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html)

**Make cloned AEM project compatible with [!DNL AEM Forms] as a Cloud Service:** Remove uber-jar and other non-cloud dependencies from the pom.xml files of the project. You can refer the pom.xml files of the [sample AEM project](assets/FaaCSample.zip) for the list of required dependencies and update your AEM project accordingly. You can also refer [AEM Project Structure](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html) to learn changes required to make an AEM project compatible with AEM as a Cloud Service.  -->

1. **Crea un [!DNL Experience Manager Forms] come [Cloud Service] progetto:** Crea un [!DNL Experience Manager Forms] come [Cloud Service] in base all&#39;ultima [Archetipo AEM](https://github.com/adobe/aem-project-archetype) o successiva. L’archetipo aiuta gli sviluppatori a iniziare facilmente a sviluppare per [!DNL AEM Forms] as a Cloud Service. Include inoltre alcuni temi e modelli di esempio per aiutarti a iniziare rapidamente.

   Apri il prompt dei comandi ed esegui il comando sottostante per creare un [!DNL Experience Manager Forms] Progetto as a Cloud Service.

   ```shell
   mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate -D archetypeGroupId=com.adobe.aem -D archetypeArtifactId=aem-project-archetype -D archetypeVersion=40 -D aemVersion="cloud" -D appTitle="Borgo AEM Forms" -D appId="bgaemforms" -D groupId="com.bgaemforms" -D includeFormsenrollment="y" -D includeFormscommunications="y" -D includeExamples="y" -D 
   ```

   Modificare la `appTitle`, `appId`e `groupId` nel comando precedente per riflettere l&#39;ambiente. Inoltre, imposta il valore per includeFormsenrollment, includeFormscommunication e includeFormsheadless su `y` o `n` a seconda della licenza e dei requisiti. IncludeFormsheadless è obbligatorio per la creazione di Forms adattivo basato su componenti core.

   * Utilizza la `includeFormsenrollment=y` per includere configurazioni specifiche di Forms, temi, modelli, componenti core e dipendenze necessarie per creare Forms adattivo. Se utilizzi Forms Portal, imposta la variabile `includeExamples=y` opzione . Aggiunge anche componenti core di Forms Portal al progetto.

   * Utilizza la `includeFormscommunications=y` per includere i componenti core di Forms e le dipendenze necessarie per includere la funzionalità di comunicazioni cliente.

1. Distribuisci il progetto nell’ambiente di sviluppo locale. È possibile utilizzare il comando seguente per distribuire nell&#39;ambiente di sviluppo locale

   `mvn -PautoInstallPackage clean install`

   Per l&#39;elenco completo dei comandi, vedere [Creazione e installazione](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#building-and-installing)

1. [Distribuisci il codice nel tuo [!DNL AEM Forms] Ambiente as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#customer-releases).

## Configurare gli strumenti del Dispatcher locale {#setup-local-dispatcher-tools}

Dispatcher è un modulo server web Apache HTTP che fornisce una protezione e prestazioni tra il livello CDN e AEM Publish. Dispatcher è parte integrante dell’architettura Experience Manager generale e deve far parte dell’ambiente di sviluppo locale.

Esegui i seguenti passaggi per configurare il Dispatcher locale e aggiungervi regole specifiche per Forms:

### Configurare il Dispatcher locale {#setup-local-dispatcher}

La [!DNL Experience Manager] L’SDK as a Cloud Service include la versione consigliata degli strumenti di Dispatcher, che facilita la configurazione, la convalida e la simulazione locale di Dispatcher. Gli strumenti di Dispatcher sono basati su Docker e forniscono strumenti a riga di comando per trasferire i file di configurazione di Apache HTTP Web Server e Dispatcher in un formato compatibile e distribuirli in Dispatcher in esecuzione nel contenitore Docker.

La memorizzazione in cache su Dispatcher consente [!DNL AEM Forms] per precompilare Adaptive Forms in un client. Migliora la velocità di rendering dei moduli precompilati.

Per istruzioni dettagliate su come impostare Dispatcher, vedi [Configurare gli strumenti del Dispatcher locale](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#local-development-environment-set-up)

### Aggiungere regole specifiche di Forms a Dispatcher {#forms-specific-rules-to-dispatcher}

Esegui i seguenti passaggi per configurare la cache del Dispatcher per Experience Manager Forms as a Cloud Service:

1. Apri il progetto AEM e passa a `\src\conf.dispatcher.d\available_farms`
1. Crea una copia del `default.farm` file. Esempio: `forms.farm`.
1. Apri la nuova creazione `forms.farm` per modificare e sostituire il codice seguente:

   ```json
   #/ignoreUrlParams {
   #/0001 { /glob "*" /type "deny" }
   #/0002 { /glob "q" /type "allow" }
   #}
   ```

   con

   ```json
   /ignoreUrlParams {
   /0001 { /glob "*" /type "deny" }
   /0002 { /glob "dataRef" /type "allow" }
   }
   ```

1. Salva e chiudi il file.
1. Vai a `conf.d/enabled_farms` e creare un collegamento simbolico al `forms.farm` file.
1. Compila e implementa il progetto nel tuo [!DNL AEM Forms] Ambiente as a Cloud Service.

### Considerazioni sulla memorizzazione in cache {#considerations-about-caching}

* La memorizzazione in cache di Dispatcher consente [!DNL AEM Forms] per precompilare Adaptive Forms in un client. Migliora la velocità di rendering dei moduli precompilati.
* Per impostazione predefinita, la memorizzazione nella cache delle funzioni di contenuto protetto è disabilitata. Per abilitare la funzione, puoi eseguire le istruzioni fornite nella [Memorizzazione in cache di contenuti protetti](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=en) articolo
* Il Dispatcher potrebbe non riuscire a invalidare alcuni Forms adattivi e i relativi Forms adattivi. Per risolvere tali problemi, vedi [[!DNL AEM Forms] Memorizzazione in cache](troubleshooting-caching-performance.md) nella sezione risoluzione dei problemi .
* Memorizzazione in cache di Forms adattivo localizzato:
   * Usa formato URL `http://host:port/content/forms/af/<afName>.<locale>.html` per richiedere una versione localizzata di un modulo adattivo anziché `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * Per impostazione predefinita, l’opzione Impostazioni internazionali del browser è disabilitata. Per modificare le impostazioni internazionali del browser,
* Quando si utilizza il formato URL `http://host:port/content/forms/af/<adaptivefName>.html`e l’opzione Usa impostazione internazionale browser in configuration manager è disabilitata; viene fornita la versione non localizzata del modulo adattivo. La lingua non localizzata è la lingua utilizzata durante lo sviluppo del Modulo adattivo. Le impostazioni internazionali configurate per il browser (impostazioni internazionali del browser) non vengono considerate e viene distribuita una versione non localizzata del modulo adattivo.
* Quando si utilizza il formato URL `http://host:port/content/forms/af/<adaptivefName>.html`, e se è abilitato l’opzione Usa impostazioni internazionali browser in configuration manager, viene fornita una versione localizzata del modulo adattivo, se disponibile. La lingua del modulo adattivo localizzato si basa sulle impostazioni internazionali configurate per il browser (impostazioni internazionali del browser). Può portare a [memorizzazione in cache solo della prima istanza di un modulo adattivo]. Per evitare che il problema si verifichi nell’istanza, vedi [Solo la prima istanza di un modulo adattivo viene memorizzata nella cache](troubleshooting-caching-performance.md) nella sezione risoluzione dei problemi .

Il tuo ambiente di sviluppo locale è pronto.

## Abilitare i componenti core di Forms adattivi per un progetto basato su Archetype AEM esistente {#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project}

Se utilizzi AEM programma basato su Archetype versione 40 o successiva per AEM Forms as a Cloud Service, i componenti core vengono abilitati automaticamente per il tuo ambiente.

Per abilitare i componenti core Forms adattivi per l’ambiente as a Cloud Service AEM Forms in base alle versioni precedenti di Archetype, incorpora nel progetto gli artefatti relativi agli esempi di componenti core WCM e gli artefatti dei componenti core Forms (inclusi gli esempi):

1. Apri la cartella di progetto Archetype AEM in un editor di codice di testo normale. Ad esempio, Codice VS.

1. Apri il file .pom di primo livello (pom padre) del progetto Archetype AEM nel tuo ambiente locale, aggiungi le seguenti proprietà al file e salvalo.

   ```XML
   <properties>
       <core.forms.components.version>2.0.4</core.forms.components.version> <!-- Replace the version with the latest released version at https://github.com/adobe/aem-core-forms-components/tags -->
       <core.wcm.components.version>2.21.2</core.wcm.components.version>
   </properties>
   ```

   Per l&#39;ultima versione di `core.forms.components` e `core.wcm.components`, controlla [documentazione sui componenti core](https://github.com/adobe/aem-core-forms-components).

1. Nella sezione dipendenze del file principale (padre) ppm.xml di livello superiore, aggiungi le seguenti dipendenze:

   ```XML
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

1. Apri il file all/pom.xml e aggiungi le seguenti dipendenze per aggiungere gli artefatti dei componenti core di Forms adattivi al progetto Archetype AEM:

   ```XML
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

   >[!NOTE]
   Assicurati che i seguenti artefatti di componenti core di Forms adattivi non siano inclusi nel progetto.
   `<dependency>`
   `<groupId>com.adobe.aem</groupId>`
   `<artifactId>core-forms-components-apps</artifactId>`
   `</dependency>`
   e
   `<dependency>`
   `<groupId>com.adobe.aem</groupId>`
   `<artifactId>core-forms-components-core</artifactId>`
   `</dependency>`

1. [Eseguire la pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html). Dopo l’esecuzione corretta della pipeline, i componenti core di Forms adattivi sono abilitati per l’ambiente. Inoltre, il modello di Forms adattivo (componenti core) e il tema Canvas vengono aggiunti all’ambiente as a Cloud Service Forms.


## Aggiornare l’ambiente di sviluppo locale {#upgrade-your-local-development-environment}

Per aggiornare l&#39;SDK a una nuova versione è necessario sostituire l&#39;intero ambiente di sviluppo locale, con la conseguente perdita di tutto il codice, la configurazione e il contenuto negli archivi locali. Assicurati che qualsiasi codice, configurazione o contenuto che non deve essere distrutto sia correttamente impegnato in Git o esportato dalle istanze di Experience Manager locali come CRX-Packages.

### Come evitare la perdita di contenuto durante l&#39;aggiornamento dell&#39;SDK {#avoid-content-loss-when-upgrading--SDK}

L&#39;aggiornamento dell&#39;SDK sta creando in modo efficace nuove istanze di authoring e pubblicazione, tra cui un nuovo archivio ([Configurare AEM progetto](#forms-cloud-service-local-development-environment)), il che significa che tutte le modifiche apportate all’archivio di un SDK precedente andranno perse. Per strategie valide per aiutare a mantenere il contenuto tra gli aggiornamenti dell’SDK, vedi [Come evitare la perdita di contenuto durante l&#39;aggiornamento dell&#39;SDK AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en#optional-local-aem-runtime-set-up-tasks)

<!--When you update any  Forms-specifc configuration, create overlays, develop custom Adaptive Form components, or develop and test any custom code in AEM project for the development tasks related to local development instance, use the AEM project cloned from the Cloud Manager Git repository to [deploy the custom code and other changes to your [!DNL AEM Forms] as a Cloud Service's production or non-production environment](https://video.tv.adobe.com/v/30191?quality=9).

## Upgrade your local development environment {#update-local-setup}

Update the local AEM setup (AEM SDK) to latest version at least monthly on, or shortly after, the last Thursday of each month, which is the release cadence for AEM as a Cloud Service "feature releases". You can download local AEM SDK from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

Updating the AEM SDK to a new version requires replacing the entire local development environment, resulting in a loss of all code, configuration and content in the local AEM repositories. Ensure that any code, config or content that should not be destroyed is safely committed to Git, or exported from the local AEM instance as AEM Packages.

### How to avoid content loss when upgrading the AEM SDK {#avoid-content-loss-when-upgrading--AEM-SDK}

Upgrading the AEM SDK is effectively creating a brand new AEM runtime ([Set up a local AEM instance](setup-forms-cloud-service.md)), including a new repository ([Set up AEM project](#forms-cloud-service-local-development-environment)), meaning any changes made to a prior AEM SDK's repository are lost. The following are viable strategies for aiding in persisting content between AEM SDK upgrades, and can be used discretely or in concert:

1. Create a content package dedicated to containing the sample content to aid in development and maintain it in Git. Any content that should be persisted through AEM SDK upgrades would be persisted into this package and re-deployed after upgrading the AEM SDK.
1. Use [oak-upgrade](https://jackrabbit.apache.org/oak/docs/migration.html) with the `includepaths` directive, to copy content from the prior AEM SDK repository to the new AEM SDK repository.
1. Back up any content using AEM Package Manager and content packages on the prior AEM SDK and re-install them on the new AEM SDK.

Remember, using the above approaches to maintain code between AEM SDK upgrades, indicates a development anti-pattern. Non-disposable code should originate in your Development IDE and flow into AEM SDK via deployments.

For information about troubleshooting, stopping local AEM environment, run modes, and deployment, see [Set up local AEM Runtime](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#local-development-environment-set-up).-->

### Eseguire il backup e importare contenuti specifici di Forms in un nuovo ambiente SDK {#backup-and-import-Forms-specific-content-to-new-SDK-environment}

Per eseguire il backup e spostare le risorse dall’SDK esistente a un nuovo ambiente SDK:

* Crea un backup del contenuto esistente.

* Imposta un nuovo ambiente SDK.

* Importa il backup nel tuo nuovo ambiente SDK.

### Creare un backup del contenuto esistente {#create-backup-of-your-existing-content}

Esegui il backup di Forms adattivo, modelli, modello dati modulo, tema, configurazioni e codice personalizzato. Per creare un backup è possibile eseguire le seguenti operazioni:

1. [Scarica](import-export-forms-templates.md#manage-forms-and-related-assets) Forms adattivo, temi e PDF forms.
1. Esportare modelli di moduli adattivi.

1. Download di modelli di dati per moduli

1. Esporta modelli modificabili, configurazioni cloud e modello di flusso di lavoro. Per esportare tutti gli elementi precedentemente menzionati dall’SDK esistente, crea un [CRX-Package](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=it) con i seguenti filtri:

   * /conf/ReferenceEditableTemplates
   * /conf/global/settings/cloudconfigs
   * /conf/global/settings/wcm
   * /var/workflow/models
   * /conf/global/settings/workflow
1. Esporta configurazioni e-mail, invia e precompila il codice delle azioni dall’ambiente di sviluppo locale. Per esportare queste impostazioni e configurazioni, crea una copia delle seguenti cartelle e file nell’ambiente di sviluppo locale:

   * `[Archetype Project in Cloud Service Git]/core/src/main/java/com/<program name>/core/service`
   * `[Archetype Project in Cloud Service Git] /core/src/main/java/com/<program name>/core/servlets/FileAttachmentServlet.java`
   * `[Archetype Project in Cloud Service Git]/ui.apps/src/main/content/jcr_root/apps/<program name>/config`

### Importare il backup nel nuovo ambiente SDK {#import-the-backup-to-your-new-SDK-environment}

Importa Forms adattivo, modelli, modello dati modulo, tema, configurazioni e codice personalizzato nel tuo nuovo ambiente. Per importare il backup è possibile eseguire le seguenti operazioni:

1. [Importa](import-export-forms-templates.md#manage-forms-and-related-assets) Forms adattivo, temi e PDF forms per nuovi ambienti SDK.
1. Importare modelli di moduli adattivi nel nuovo ambiente SDK.

1. Carica i modelli di dati dei moduli nel nuovo ambiente SDK.

1. Importa modelli modificabili, configurazioni cloud e modello di flusso di lavoro. Per importare tutti gli elementi precedentemente menzionati nel tuo nuovo ambiente SDK, importa il CRX-Package contenente questi elementi nel tuo nuovo ambiente SDK.

1. Importa configurazioni e-mail, invia e precompila il codice delle azioni dall’ambiente di sviluppo locale. Per importare queste impostazioni e configurazioni, inserisci i seguenti file dal vecchio progetto Archetype nel nuovo progetto Archetype:

   * `[Archetype Project in Cloud Service Git]/core/src/main/java/com/<program name>/core/service`
   * `[Archetype Project in Cloud Service Git] /core/src/main/java/com/<program name>/core/servlets/FileAttachmentServlet.java`
   * `[Archetype Project in Cloud Service Git]/ui.apps/src/main/content/jcr_root/apps/<program name>/config`

Il nuovo ambiente dispone ora di moduli e delle relative risorse del vecchio ambiente.
