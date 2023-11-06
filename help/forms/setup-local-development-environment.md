---
title: Come si imposta un ambiente di sviluppo locale per AEM Forms?
description: Configurare un ambiente di sviluppo locale per Adobe Experience Manager Forms as a Cloud Service
exl-id: 12877a77-094f-492a-af58-cffafecf79ae
source-git-commit: a0433718a223a6d3aa7740232caa17650bce5ff6
workflow-type: tm+mt
source-wordcount: '2847'
ht-degree: 3%

---

# Configurare l’ambiente di sviluppo locale per AEM Forms {#overview}

Quando imposti e configuri un’ [!DNL  Adobe Experience Manager Forms] as a [!DNL  Cloud Service] ambiente, puoi configurare ambienti di sviluppo, staging e produzione su cloud. Inoltre, puoi anche impostare e configurare un ambiente di sviluppo locale.

Puoi utilizzare l’ambiente di sviluppo locale per eseguire le seguenti azioni senza effettuare l’accesso all’ambiente di sviluppo cloud:

* [Creare moduli](creating-adaptive-form.md) e risorse correlate (temi, modelli, azioni di invio personalizzate e altro ancora)
* [Conversione di moduli PDF in moduli adattivi](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html?lang=it)
* Creare applicazioni da generare [Comunicazioni con i clienti](aem-forms-cloud-service-communications-introduction.md) su richiesta o in modalità batch.

Dopo che un modulo adattivo o le risorse correlate sono pronti nell’istanza di sviluppo locale o in un’applicazione da generare [Comunicazioni con i clienti] è pronto, è possibile esportare l’applicazione Adaptive Form o Customer Communications dall’ambiente di sviluppo locale a un ambiente di Cloud Service per ulteriori test o per passare agli ambienti di produzione.

Puoi anche sviluppare e testare il codice personalizzato, come componenti personalizzati e il servizio di preriempimento, nell’ambiente di sviluppo locale. Quando il codice personalizzato è testato e pronto, puoi utilizzare l’archivio Git dell’ambiente di sviluppo del Cloud Service per distribuire il codice personalizzato.

Per impostare un nuovo ambiente di sviluppo locale e utilizzarlo per lo sviluppo di per le attività, eseguire le azioni seguenti nell&#39;ordine elencato:

* [Configurare gli strumenti di sviluppo](#setup-development-tools-for-AEM-projects)

* [Configurare le istanze di authoring e pubblicazione locali](#set-up-local-experience-manager-environment-for-development)

* [Aggiungere l’archivio Forms alle istanze di sviluppo locali e configurare gli utenti](#add-forms-archive-configure-users)

* [Imposta ambiente di sviluppo locale per microservizi](#docker-microservices)

* [Configurare un progetto di sviluppo](#forms-cloud-service-local-development-environment)

* [Configurare gli strumenti locali di Dispatcher](#setup-local-dispatcher-tools)

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

Per configurare un ambiente di sviluppo locale è necessario il software seguente. Scarica questi elementi prima di iniziare a configurare l’ambiente di sviluppo locale:

| Software | Descrizione | Collegamenti di download |
|---|---|---|
| SDK di Adobe Experience Manager as a Cloud Service | L’SDK include [!DNL Adobe Experience Manager] Strumenti QuickStart e Dispatcher | Scarica l’SDK più recente da [Distribuzione di software](#software-distribution) |  |
| Archivio delle funzioni di Adobe Experience Manager Forms (componente aggiuntivo AEM Forms) | Strumenti per creare, assegnare stili e ottimizzare Adaptive Forms e altre funzioni di Adobe Experience Manager Forms | Scarica da [Distribuzione di software](#software-distribution) |
| (Facoltativo) Contenuto di riferimento Adobe Experience Manager Forms | Strumenti per creare, assegnare stili e ottimizzare Adaptive Forms e altre funzioni di Adobe Experience Manager Forms | Scarica da [Distribuzione di software](#software-distribution) |
| (Facoltativo) Adobe Experience Manager Forms Designer | Strumenti per creare, assegnare stili e ottimizzare Adaptive Forms e altre funzioni di Adobe Experience Manager Forms | Scarica da [Distribuzione di software](#software-distribution) |

### Scarica la versione più recente del software da Software Distribution {#software-distribution}

Per scaricare la versione più recente dell’SDK per Adobe Experience Manager as a Cloud Service, l’archivio delle funzioni di Experience Manager Forms (componente aggiuntivo AEM Forms), le risorse di riferimento per i moduli o Forms Designer da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html):

1. Accedi a <https://experience.adobe.com/#/downloads> con il tuo Adobe ID

   >[!NOTE]
   >
   > Per scaricare l’SDK as a Cloud Service per l’AEM, è necessario effettuare il provisioning della tua organizzazione Adobe affinché l’AEM as a Cloud Service possa eseguirne il download.

1. Accedi a **[!UICONTROL AEM as a Cloud Service]** scheda.
1. Ordina per data di pubblicazione in ordine decrescente.
1. Fai clic sull’SDK di Adobe Experience Manager as a Cloud Service più recente, sull’archivio delle funzioni di Experience Manager Forms (componente aggiuntivo AEM Forms), sulle risorse di riferimento per i moduli o su Forms Designer.
1. Rivedere e accettare il contratto di licenza. Tocca il **[!UICONTROL Scarica]** pulsante.

## Impostare gli strumenti di sviluppo per i progetti AEM {#setup-development-tools-for-AEM-projects}

Il progetto Adobe Experience Manager Forms è una base di codice personalizzata. Contiene codice, configurazioni e contenuti distribuiti tramite Cloud Manager per [!DNL Adobe Experience Manager] as a Cloud Service. Il [Progetto AEM Archetipo Maven](https://github.com/adobe/aem-project-archetype) fornisce la struttura della linea di base per il progetto.

Configura i seguenti strumenti di sviluppo da utilizzare per [!DNL Adobe Experience Manager] progetto per lo sviluppo:

* [Java™](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#local-development-environment-set-up)
* [Git](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#install-git)
* [Node.js (npm)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#node-js)
* [Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#install-maven)

Per istruzioni dettagliate sulla configurazione degli strumenti di sviluppo precedentemente menzionati, consulta [Configurare gli strumenti di sviluppo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html).

## Configurare l’ambiente Experience Manager locale per lo sviluppo

L’SDK di Cloud Service fornisce un file QuickStart. Esegue una versione locale di Experience Manager. È possibile eseguire localmente le istanze Author o Publish.

Benché QuickStart offra un&#39;esperienza di sviluppo locale, non dispone di tutte le funzioni disponibili in [!DNL Adobe Experience Manager] as a Cloud Service. Quindi, testa sempre le funzioni e il codice con [!DNL Adobe Experience Manager] ambiente di sviluppo as a Cloud Service prima di spostare le funzioni nell’ambiente di staging o produzione.

Per installare e configurare l’ambiente di Experience Manager locale, effettua le seguenti operazioni:

* [Scarica ed estrai](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html) il [!DNL Adobe Experience Manager] SDK AS A CLOUD SERVICE
* [Configurare un’istanza di authoring](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en#set-up-local-aem-author-service)
* [Configurare un’istanza Publish](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en#set-up-local-aem-publish-service)

## Aggiungere l’archivio Forms alle istanze di authoring e pubblicazione locali e configurare gli utenti specifici di Forms {#add-forms-archive-configure-users}

Per aggiungere un archivio Forms alle istanze di Experience Manager e configurare utenti specifici per i moduli, effettua le seguenti operazioni nell’ordine elencato:

### Installa l’archivio delle funzioni più recente dei componenti aggiuntivi di Forms {#add-forms-archive}

L’archivio delle funzioni di Adobe Experience Manager Forms as a Cloud Service fornisce strumenti per creare, assegnare stili e ottimizzare Adaptive Forms nell’ambiente di sviluppo locale. Installa il pacchetto per creare un modulo adattivo e utilizza varie altre funzioni di [!DNL AEM Forms]. Per installare il pacchetto:

1. Scarica ed estrai la versione più recente [!DNL AEM Forms] per il sistema operativo da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html).

1. Passa alla directory crx-quickstart/install. Se la cartella non esiste, creala.

1. Arrestare l’istanza di AEM, inserire [!DNL AEM Forms] archivio delle funzioni del componente aggiuntivo, `aem-forms-addon-<version>.far`, nella cartella di installazione e riavviare l&#39;istanza.

### Configurare utenti e autorizzazioni {#configure-users-and-permissions}

Creare utenti come sviluppatori di moduli e professionisti dei moduli e [aggiungi questi utenti a gruppi di moduli predefiniti](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=en#accessing) per fornire le autorizzazioni necessarie. Nella tabella seguente sono elencati tutti i tipi di utenti e i gruppi predefiniti per ogni tipo di utente di Forms:

| Tipo utente | Gruppo AEM |
|---|---|
| Professionista del modulo / | [!DNL forms-users] (Utenti AEM Forms), [!DNL template-authors], [!DNL workflow-users], [!DNL workflow-editors], e [!DNL fdm-authors] |
| Sviluppatore modulo | [!DNL forms-users] (Utenti AEM Forms), [!DNL template-authors], [!DNL workflow-users], [!DNL workflow-editors], e [!DNL fdm-authors] |
| Customer Experience Lead o UX Designer | [!DNL forms-users], [!DNL template-authors] |
| Amministratore AEM | [!DNL aem-administrators], [!DNL fd-administrators] |
| Utente finale | Quando un utente deve effettuare l’accesso per visualizzare e inviare un modulo adattivo, aggiungi tali utenti a [!DNL forms-users] gruppo. </br> Se non è richiesta l’autenticazione utente per accedere a Adaptive Forms, non assegnare alcun gruppo a tali utenti. |

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

## Imposta ambiente di sviluppo locale per documento di record (DoR){#docker-microservices}

AEM Forms as a Cloud Service fornisce un ambiente SDK basato su docker per semplificare lo sviluppo di documenti di record e l’utilizzo di altri microservizi. Consente di configurare manualmente binari e adattamenti specifici della piattaforma. Per impostare l’ambiente:

1. Installare e configurare Docker:

   * (Per Microsoft® Windows) Installazione [Docker Desktop](https://www.docker.com/products/docker-desktop). Configura `Docker Engine` e `docker-compose` sul tuo computer.

   * (Apple macOS) Installazione [Docker Desktop per Mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac). Include Docker Engine, il client CLI Docker, Docker Compose, Docker Content Trust, Kubernetes e Credential Helper.

   * (Per Linux®) Installa [Docker Engine](https://docs.docker.com/engine/install/#server) e [Componi Docker](https://docs.docker.com/compose/install/) sul tuo computer.

   >[!NOTE]
   >
   > * Per Apple macOS, inserire nell&#39;elenco Consentiti cartelle contenenti istanze AEM Author locali.
   >
   > * Docker Desktop per Windows supporta due back-end, Hyper-V
   > (legacy) e WSL2 (modern). La condivisione dei file avviene automaticamente
   > gestito da Docker tramite WSL2 (modern). Devi
   > configurare in modo esplicito la condivisione dei file quando si utilizza Hyper-V (legacy).

1. Crea una cartella, ad esempio aem-sdk, in parallelo alle istanze di authoring e pubblicazione. Ad esempio, C:\aem-sdk.

1. Estrai `aem-forms-addon-<version>.zip\aem-forms-addon-native-<version>.zip` file.

   ![aggiunta aem forms estratta nativa](assets/microservice-docker.png)

1. Creare una variabile di ambiente AEM_HOME e puntare all&#39;installazione locale di AEM Author. Ad esempio, C:\aem\author\.

1. Apri sdk.bat o sdk.sh per la modifica. Impostare AEM_HOME in modo che punti all&#39;installazione di AEM Author locale. Ad esempio, C:\aem\author\.

1. Apri il prompt dei comandi e passa alla `aem-forms-addon-native-<version>` cartella.

1. Assicurati che l’istanza locale di AEM Author sia operativa. Esegui il seguente comando per avviare l&#39;SDK:

   * (su Microsoft® Windows) `sdk.bat start`
   * (su Linux® o Apple macOS) `AEM_HOME=[local AEM Author installation] ./sdk.sh start`

   >[!NOTE]
   >
   > Se hai definito la variabile di ambiente nel file sdk.sh, specificarla nella riga di comando è facoltativo. L’opzione per definire la variabile di ambiente nella riga di comando viene fornita per eseguire il comando senza aggiornare lo script della shell.

   ![start-sdk-command](assets/start-sdk.png)

Ora puoi utilizzare l’ambiente di sviluppo locale per eseguire il rendering del documento di record. Per eseguire il test, carica un file XDP nel tuo ambiente ed esegui il rendering. Ad esempio: <http://localhost:4502/libs/xfaforms/profiles/default.print.pdf?template=crx:///content/dam/formsanddocuments/cheque-request.xdp> converte il file XDP nel documento PDF.

## Configurare un progetto di sviluppo per Forms basato su Archetipo Experience Manager {#forms-cloud-service-local-development-environment}

Utilizza questo progetto per creare Forms adattivo, distribuire aggiornamenti di configurazione, sovrapposizioni, creare componenti per moduli adattivi personalizzati, testare e codice personalizzato in locale [!DNL Experience Manager Forms] SDK Dopo il test locale, puoi distribuire il progetto in  [!DNL Experience Manager Forms] ambienti di produzione e non di produzione as a Cloud Service. Quando distribuisci il progetto, vengono distribuite anche le seguenti risorse AEM Forms:

| Temi | Modelli | Modelli dati modulo |
---------|----------|---------
| Area di lavoro 3.0 | Base | Microsoft® Dynamics 365 |
| Tranquilla | Vuoto | Salesforce |
| Urbano |   |  |
| Ultramarina |  |  |
| Beryl |  |  |

>[!NOTE]
>
> Imposta il progetto basato su Archetipo AEM versione 30 o successiva per ottenere e utilizzare modelli di dati per moduli Microsoft® Dynamics 365 e Salesforce con AEM Forms as a Cloud Service.
Imposta il progetto basato su Archetipo AEM versione 32 o successiva per ottenere e utilizzare i temi Tranquil, Urbane e Ultramarine con AEM Forms as a Cloud Service.

Per impostare il progetto:

1. **Clona l’archivio Git di Cloud Manager nell’istanza di sviluppo locale:**  L’archivio Git di Cloud Manager contiene un progetto AEM predefinito. Si basa su [Archetipo AEM](https://github.com/adobe/aem-project-archetype/). Clona l’archivio Git di Cloud Manager utilizzando la gestione self-service dell’account Git dall’interfaccia utente di Cloud Manager per inserire il progetto nell’ambiente di sviluppo locale. Per informazioni dettagliate sull’accesso all’archivio, consulta [Accesso agli archivi](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html).

<!-- 1. 
After the repository is cloned, [integrate your Git repo with Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html)

**Make cloned AEM project compatible with [!DNL AEM Forms] as a Cloud Service:** Remove uber-jar and other non-cloud dependencies from the pom.xml files of the project. You can refer the pom.xml files of the [sample AEM project](assets/FaaCSample.zip) for the list of required dependencies and update your AEM project accordingly. You can also refer [AEM Project Structure](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html) to learn changes required to make an AEM project compatible with AEM as a Cloud Service.  -->

1. **Creare un [!DNL Experience Manager Forms] as a [Cloud Service] progetto:** Creare un [!DNL Experience Manager Forms] as a [Cloud Service] progetto basato sui più recenti [Archetipo AEM](https://github.com/adobe/aem-project-archetype) o più tardi. L’archetipo aiuta gli sviluppatori a iniziare facilmente a sviluppare per [!DNL AEM Forms] as a Cloud Service. Include inoltre alcuni temi e modelli di esempio per aiutarti a iniziare rapidamente.

   Apri il prompt dei comandi ed esegui il comando seguente per creare un [!DNL Experience Manager Forms] progetto as a Cloud Service.

   ```shell
   mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate -D archetypeGroupId=com.adobe.aem -D archetypeArtifactId=aem-project-archetype -D archetypeVersion="41" -D appTitle=mysite -D appId=mysite -D groupId=com.mysite -D includeFormsenrollment="y" -D aemVersion="cloud"
   ```

   Modificare il `appTitle`, `appId`, e `groupId` nel comando precedente per riflettere l’ambiente. Impostare inoltre il valore di includeFormsenrollment, includeFormscommunications e includeFormsheadless su `y` o `n` a seconda della licenza e dei requisiti. IncludeFormsheadless è obbligatorio per creare Forms adattivo basato su Componenti core.

   * Utilizza il `includeFormsenrollment=y` opzione per includere configurazioni, temi, modelli, Componenti core e dipendenze specifiche di Forms necessari per creare Forms adattivo. Se si utilizza Forms Portal, impostare `includeExamples=y` opzione. Aggiunge inoltre al progetto i componenti core di Forms Portal.

   * Utilizza il `includeFormscommunications=y` opzione per includere i Componenti core Forms e le dipendenze necessarie per includere la funzionalità di comunicazione con i clienti.

     >[!WARNING]
     >
     * Quando si crea un progetto Archetipo con versione 45, il [Cartella progetto Archetipo AEM]/pom.xml inizialmente imposta la versione dei componenti core forms su 2.0.64. Prima di creare o distribuire il progetto Archetipo, aggiorna la versione dei componenti core forms al 2.0.62.

1. Implementa il progetto nell’ambiente di sviluppo locale. Puoi utilizzare il seguente comando per distribuire nell’ambiente di sviluppo locale

   `mvn -PautoInstallPackage clean install`

   Per l&#39;elenco completo dei comandi, vedere [Creazione e installazione](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#building-and-installing)

1. [Distribuisci il codice nel tuo [!DNL AEM Forms] ambiente as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#customer-releases).

## Configurare gli strumenti locali di Dispatcher {#setup-local-dispatcher-tools}

Dispatcher è un modulo server web Apache HTTP che fornisce sicurezza e prestazioni tra il livello di CDN e pubblicazione AEM. Dispatcher è parte integrante dell’architettura Experience Manager complessiva e deve far parte dell’ambiente di sviluppo locale.

Per configurare il Dispatcher locale e quindi aggiungere a esso regole specifiche per Forms, effettua le seguenti operazioni:

### Configurare il Dispatcher locale {#setup-local-dispatcher}

Il [!DNL Experience Manager] L’SDK as a Cloud Service include la versione consigliata degli strumenti di Dispatcher, che facilita la configurazione, la convalida e la simulazione locale di Dispatcher. Gli strumenti di Dispatcher sono basati su Docker e forniscono strumenti per riga di comando per trasferire i file di configurazione del server web Apache HTTP e del Dispatcher in un formato compatibile e distribuirli a Dispatcher in esecuzione nel contenitore Docker.

La memorizzazione in cache in Dispatcher consente [!DNL AEM Forms] per precompilare il Forms adattivo su un client. Migliora la velocità di rendering dei moduli precompilati.

Per istruzioni dettagliate sulla configurazione di Dispatcher, vedi [Configurare gli strumenti locali di Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#local-development-environment-set-up)

### Aggiungere regole specifiche di Forms a Dispatcher {#forms-specific-rules-to-dispatcher}

Per configurare la cache di Dispatcher per Experience Manager Forms as a Cloud Service, effettua le seguenti operazioni:

1. Apri il progetto AEM e passa a `\src\conf.dispatcher.d\available_farms`
1. Crea una copia di `default.farm` file. Esempio: `forms.farm`.
1. Apri il nuovo `forms.farm` file per la modifica e sostituire il seguente codice:

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
1. Compila e distribuisci il progetto nel tuo [!DNL AEM Forms] ambiente as a Cloud Service.

### Considerazioni sul caching {#considerations-about-caching}

* Il caching di Dispatcher consente [!DNL AEM Forms] per precompilare il Forms adattivo su un client. Migliora la velocità di rendering dei moduli precompilati.
* Per impostazione predefinita, la memorizzazione nella cache delle funzioni di contenuto protetto è disabilitata. Per attivare la funzione, è possibile eseguire le istruzioni fornite nella [Caching di contenuto protetto](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=en) articolo
* Il Dispatcher può non invalidare alcuni Forms adattivi e i relativi Forms adattivi. Per risolvere questi problemi, vedi [[!DNL AEM Forms] Memorizzazione in cache](troubleshooting-caching-performance.md) nella sezione risoluzione dei problemi.
* Memorizzazione in cache di Forms adattivo localizzato:
   * Usa formato URL `http://host:port/content/forms/af/<afName>.<locale>.html` per richiedere una versione localizzata di un modulo adattivo anziché `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * Per impostazione predefinita, l&#39;opzione Impostazioni internazionali browser è disabilitata. Per modificare le impostazioni internazionali del browser:
* Quando si utilizza il formato URL `http://host:port/content/forms/af/<adaptivefName>.html`, e Use Browser Locale in configuration manager è disabilitato, viene distribuita la versione non localizzata del modulo adattivo. Il linguaggio non localizzato è il linguaggio utilizzato durante lo sviluppo del modulo adattivo. Le impostazioni locali configurate per il browser (impostazioni locali del browser) non vengono considerate e viene distribuita una versione non localizzata del modulo adattivo.
* Quando si utilizza il formato URL `http://host:port/content/forms/af/<adaptivefName>.html`, e l’opzione Usa impostazioni locali del browser nella gestione della configurazione è abilitata, viene distribuita una versione localizzata del modulo adattivo, se disponibile. La lingua del modulo adattivo localizzato si basa sulle impostazioni locali configurate per il browser (impostazioni locali del browser). Può portare a [memorizzazione nella cache solo della prima istanza di un modulo adattivo]. Per evitare che il problema si verifichi nell’istanza, consulta [solo la prima istanza di un modulo adattivo è memorizzata in cache](troubleshooting-caching-performance.md) nella sezione risoluzione dei problemi.

L’ambiente di sviluppo locale è pronto.

## Abilitare i componenti core dei moduli adattivi in AEM Forms as a Cloud Service e nell’ambiente di sviluppo locale

Abilitando i componenti core Adaptive Forms su AEM Forms as a Cloud Service, puoi iniziare a creare, pubblicare e distribuire componenti core basati su Adaptive Forms e Headless Forms utilizzando le istanze del Cloud Service AEM Forms su più canali. Per utilizzare Headless Adaptive Forms è necessario un ambiente abilitato per i Componenti core Forms adattivi.

Per istruzioni, consulta [Abilitare i componenti core Adaptive Forms nell’ambiente di sviluppo as a Cloud Service e locale di AEM Forms](/help/forms/enable-adaptive-forms-core-components.md)


## Aggiornare l’ambiente di sviluppo locale {#upgrade-your-local-development-environment}

L’aggiornamento dell’SDK a una nuova versione richiede la sostituzione dell’intero ambiente di sviluppo locale, con conseguente perdita di codice, configurazione e contenuto negli archivi locali. Assicurati che qualsiasi codice, configurazione o contenuto che non deve essere eliminato sia salvato in modo sicuro in Git o esportato dalle istanze di Experience Manager locali come CRX-Packages.

### Come evitare la perdita di contenuti durante l’aggiornamento dell’SDK {#avoid-content-loss-when-upgrading--SDK}

L’aggiornamento dell’SDK crea efficacemente una nuova istanza di authoring e pubblicazione, incluso un nuovo archivio ([Configura progetto AEM](#forms-cloud-service-local-development-environment)), il che significa che tutte le modifiche apportate all’archivio di un SDK precedente andranno perse. Per strategie valide per contribuire alla persistenza dei contenuti tra gli aggiornamenti dell’SDK, consulta [Come evitare la perdita di contenuti durante l’aggiornamento dell’SDK per AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en#optional-local-aem-runtime-set-up-tasks)

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

### Backup e importazione di contenuti specifici per Forms in un nuovo ambiente SDK {#backup-and-import-Forms-specific-content-to-new-SDK-environment}

Per eseguire il backup e spostare le risorse dall’SDK esistente a un nuovo ambiente SDK:

* Crea un backup del contenuto esistente.

* Configurare un nuovo ambiente SDK.

* Importa il backup nel nuovo ambiente SDK.

### Creare un backup del contenuto esistente {#create-backup-of-your-existing-content}

Esegui il backup del Forms adattivo, dei modelli, del modello dati del modulo, del tema, delle configurazioni e del codice personalizzato. Per creare il backup, è possibile eseguire le operazioni seguenti:

1. [Scarica](import-export-forms-templates.md#manage-forms-and-related-assets) Forms, temi e PDF forms adattivi.
1. Esportare modelli di moduli adattivi.

1. Scarica modelli dati modulo

1. Esporta modelli modificabili, configurazioni cloud e modello di flusso di lavoro. Per esportare tutti gli elementi precedentemente menzionati dall’SDK esistente, crea un’ [CRX-Package](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=it) con i seguenti filtri:

   * /conf/ReferenceEditableTemplates
   * /conf/global/settings/cloudconfigs
   * /conf/global/settings/wcm
   * /var/workflow/models
   * /conf/global/settings/workflow
1. Esporta configurazioni e-mail, invia e precompila il codice delle azioni dal tuo ambiente di sviluppo locale. Per esportare queste impostazioni e configurazione, crea una copia delle cartelle e dei file seguenti nell’ambiente di sviluppo locale:

   * `[Archetype Project in Cloud Service Git]/core/src/main/java/com/<program name>/core/service`
   * `[Archetype Project in Cloud Service Git] /core/src/main/java/com/<program name>/core/servlets/FileAttachmentServlet.java`
   * `[Archetype Project in Cloud Service Git]/ui.apps/src/main/content/jcr_root/apps/<program name>/config`

### Importare il backup nel nuovo ambiente SDK {#import-the-backup-to-your-new-SDK-environment}

Importa Forms adattivo, modelli, modello dati modulo, tema, configurazioni e codice personalizzato nel nuovo ambiente. Per importare il backup, è possibile effettuare le seguenti operazioni:

1. [Importa](import-export-forms-templates.md#manage-forms-and-related-assets) Forms, temi e PDF forms adattivi per nuovi ambienti SDK.
1. Importare modelli di moduli adattivi nel nuovo ambiente SDK.

1. Carica modelli dati modulo nel nuovo ambiente SDK.

1. Importa modelli modificabili, configurazioni cloud e modello di flusso di lavoro. Per importare nel nuovo ambiente SDK tutti gli elementi precedentemente menzionati, importa il pacchetto CRX contenente tali elementi.

1. Importa le configurazioni e-mail, invia e precompila il codice delle azioni dal tuo ambiente di sviluppo locale. Per importare queste impostazioni e configurazione, inserisci i seguenti file dal vecchio progetto Archetipo al nuovo progetto Archetipo:

   * `[Archetype Project in Cloud Service Git]/core/src/main/java/com/<program name>/core/service`
   * `[Archetype Project in Cloud Service Git] /core/src/main/java/com/<program name>/core/servlets/FileAttachmentServlet.java`
   * `[Archetype Project in Cloud Service Git]/ui.apps/src/main/content/jcr_root/apps/<program name>/config`

Il nuovo ambiente ora dispone di moduli e risorse correlate del vecchio ambiente.
