---
title: Guida introduttiva di Adaptive Forms.
description: Scopri come creare moduli adattivi mobile-responsive con il nostro tutorial dettagliato. Questi moduli si adattano perfettamente ai diversi dispositivi, garantendo un’esperienza fluida.
keywords: Forms adattivo, Forms reattivo, Forms HTML5
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
hide: true
hidefromtoc: true
exl-id: b59cb56c-9629-48e4-b5c9-a861013a1360
source-git-commit: af58a784f24f212962ad73f11015fb788493d8b5
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 2%

---

# Creare un modulo adattivo (componenti core) - Tutorial

Al giorno d’oggi, gli utenti si aspettano un’esperienza di facile utilizzo in tutte le loro interazioni, e i moduli non fanno eccezione. I moduli adattivi possono aiutarti a creare moduli che non solo siano facili da usare sui dispositivi mobili, ma anche a migliorare il coinvolgimento degli utenti e a ridurre il tempo necessario per completarli.

Questa esercitazione fornisce una guida dettagliata alla creazione di un modulo adattivo. È suddiviso in un caso d’uso e diverse guide, ciascuna delle quali illustra come aggiungere una nuova funzione al modulo adattivo.

Al termine dell’esercitazione, sarai in grado di:

* Creare un modulo adattivo e il relativo modello dati
* Personalizzare lo stile del modulo adattivo
* Creare regole business utilizzando l’editor di regole per moduli adattivi
* Campi precompilati del modulo adattivo
* Aggiungere firme elettroniche al modulo
* Protect il modulo dai bot utilizzando Google reCAPTCHA
* Localizzare il modulo adattivo per lingue diverse
* Configurare il modulo per produrre dati strutturati
* Configurare il modulo per inviare i dati a un endpoint REST
* Publish modulo adattivo


## Perché creare moduli basati su Componenti core?

AEM Forms fornisce Componenti di base e Componenti core per creare esperienze Forms. I Componenti core sono l’approccio moderno e consigliato per creare qualsiasi nuova esperienza di Forms. Perché utilizzare i Componenti core? Questi componenti sono leggeri, open source (disponibili su github), offrono un ottimo punteggio Google Lighthouse e web vitals, sono compatibili con l’accessibilità e presentano tutte le funzioni familiari di AEM Sites (come il controllo delle versioni e la localizzazione). Inoltre, questi componenti sono più facili da formattare e possono essere facilmente personalizzati in base alle linee guida di branding della tua organizzazione. Questi non hanno dipendenze di terze parti, qualsiasi sviluppatore con conoscenze di JavaScript e CSS può facilmente personalizzare questi componenti.

![Perché creare componenti core basati su Adaptive Forms? Questi componenti sono leggeri, più facili da personalizzare, offrono un punteggio elevato per il faro, supportano gli standard di accessibilità, sono facilmente personalizzabili, open source, sono disponibili su github, non dipendono da librerie di terze parti e non hanno quasi nessuna curva di apprendimento per gli sviluppatori AEM e gli autori AEM. Inoltre, i componenti core AEM Forms presentano tutte le funzioni dei componenti core AEM WCM.](/help/forms/assets/cc-core-components-benefits.png){width="50%"}

## Caso d’uso: prequalificazione semplificata del prestito domestico con Forms adattivo

In questo tutorial crei un modulo adattivo per una banca di grandi dimensioni. Il caso d’uso è:

Potenziali acquirenti di casa visitano il sito web della banca o la filiale per esplorare le opzioni di prestito della casa. Il processo di applicazione tradizionale è lungo e travolgente, spesso richiede una documentazione iniziale. Questo scoraggia alcuni acquirenti dall&#39;avviare il processo, ostacolando sia la generazione di lead della banca che la capacità dell&#39;acquirente di cercare con sicurezza la casa dei loro sogni.

Hai il compito di sviluppare un modulo interattivo di pre-qualificazione del prestito per la casa. Questo modulo raccoglierebbe informazioni di base, prequalificherebbe il mutuatario in base al suo input, offrendo importi di prestito stimati, potenziale fabbisogno di acconto e tassi di interesse basati su diversi tipi di prestito. Gli utenti prequalificati sarebbero in grado di avviare una richiesta di prestito completa direttamente dal modulo di prequalifica.

Il modulo viene creato utilizzando moduli adattivi. Ciò consente un’esperienza personalizzata durante la raccolta dei dati finanziari necessari per un’accurata prequalificazione del prestito per l’abitazione.

Una volta completata l’esercitazione, il modulo apparirà e funzionerà come nel seguente modulo:

![Aggiungere qui un modulo di lavoro](/help/forms/assets/cc-tutorial-final-form.png)

## Configurare l’ambiente di sviluppo

Puoi generare e testare il modulo adattivo direttamente sul computer locale, prima di distribuirlo in un ambiente di Cloud Service. Adobe fornisce un SDK AEM a per lo sviluppo locale che consente di:

* Creare, personalizzare e testare i moduli localmente.
* Progettare i temi dei moduli e creare le configurazioni a livello locale
* Distribuisci facilmente le risorse finite nel cloud.

Lo sviluppo locale con l’SDK dell’AEM consente di risparmiare tempo e semplifica il processo di sviluppo


**Inizio?**

1. [Configura strumenti di sviluppo per progetti AEM](/help/forms/setup-local-development-environment.md#set-up-development-tools-for-aem-projects): scarica e installa la versione più recente di [Java 11™](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#local-development-environment-set-up), [Git](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#install-git), [Node.js (npm)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#node-js) e [Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#install-maven). Installare inoltre un editor di testo normale. Gli esempi contenuti in questa esercitazione sono basati su Visual Studio Code.

1. [Installa l&#39;SDK per AEM](/help/forms/setup-local-development-environment.md#set-up-local-experience-manager-environment-for-development): scarica e installa la versione più recente dell&#39;SDK per AEM. Ciò fornisce gli strumenti essenziali per lo sviluppo dell’AEM. Nota la versione dell’SDK per AEM.

   ![Distribuzione-Software](/help/forms/assets/software-distribution.png)

   ![installa AEM SDK](/help/forms/assets/start-aem-sdk.png)

1. [Aggiungi il componente aggiuntivo AEM Forms](/help/forms/setup-local-development-environment.md#add-forms-archive-to-local-author-and-publish-instances-and-configure-forms-specific-users): scarica e installa il componente aggiuntivo AEM Forms corrispondente alla versione dell&#39;SDK AEM dal portale [Distribuzione software](https://experience.adobe.com/#/downloads).
   ![install-aem-forms-add-on](/help/forms/assets/install-aem-forms-add-on.png)

   +++Installare il componente aggiuntivo AEM Forms:

   Per installare AEM Forms Add-on:

   1. Interrompere l’SDK per AEM.
   1. Aggiungere il file del componente aggiuntivo AEM Forms (.far) alla cartella `AEM SDK/crx-quickstart/install`
   1. Riavvia l’SDK dell’AEM.

   +++

1. [Configura autorizzazioni utente](/help/forms/setup-local-development-environment.md#configure-users-and-permissions): crea utenti con autorizzazioni di sviluppo, creazione e altro e aggiungi questi utenti a gruppi di moduli predefiniti.


1. [Aggiungi modelli Forms adattivi](/help/forms/setup-local-development-environment.md#set-up-a-development-project-for-forms-based-on-experience-manager-archetype): utilizza gli archetipi AEM 48 o versioni successive per creare un nuovo progetto AEM e distribuirlo nell&#39;SDK AEM. Il progetto aggiunge modelli di Forms adattivi all’SDK dell’AEM.

   ![Modelli di modulo adattivo](/help/forms/assets/adaptive-forms-templates.png)

   +++Aggiungi modelli di Forms adattivi all’SDK dell’AEM:

   1. Esegui il comando seguente per creare un progetto AEM.

      ```
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate -D archetypeGroupId=com.adobe.aem -D archetypeArtifactId=aem-project-archetype -D archetypeVersion="48" -D appTitle=securbank -D appId=securbank -D groupId=com.securbank -D includeFormsenrollment="y" -D aemVersion="cloud"
      ```

      ![Progetto-Archetipo-AEM](/help/forms/assets/aem-archetype-project.png)

   1. Implementa il progetto nell’ambiente di sviluppo locale. Puoi utilizzare il seguente comando per distribuire nell’ambiente di sviluppo locale

      ```
      cd securbank
      
      mvn -PautoInstallPackage clean install
      ```

   Dopo aver implementato il progetto AEM, puoi visualizzare i modelli di Forms adattivi nel tuo ambiente.

   +++


Per istruzioni dettagliate e guida dettagliata sulla configurazione dell&#39;ambiente di sviluppo AEM Forms locale, fare riferimento all&#39;articolo [configurazione dell&#39;ambiente di sviluppo locale per AEM Forms](/help/forms/setup-local-development-environment.md).



## Passaggio successivo

Dopo aver configurato l’ambiente di sviluppo, puoi creare un modulo adattivo. Nel prossimo articolo imparerai a:

* Creare un modulo adattivo dal modello vuoto
* Layout dei campi per visualizzare e accettare facilmente le informazioni.
* Visualizzare l&#39;anteprima del modulo.

<!-- 

### Step 2: Create Form Data Model

A form data model lets you connect an adaptive form to disparate data sources. For example, AEM user profile, RESTful web services, SOAP-based web services, OData services, and relational databases. You can use the form data model with an adaptive form to retrieve, update, delete, and add data to connected data sources.

Goals of article:

* Create the form data model using Rest endpoint.
* Add data model objects so you can form the data model.
* Configure read and write services for the form data model.
* Test form data model and configured services with test data.

### Step 4: Apply rules to adaptive form fields

AEM Forms provide an editor to write rules on adaptive form objects. These rules define actions to trigger on form objects based on preset conditions, user inputs, and user actions on the form. It helps ensure accuracy and speeds up the form-filling experience.

Goals:

* Create and apply rules to adaptive form fields.
* Use rules to trigger form data model services to update the data to database.

### Step 5: Style your adaptive form

Adaptive forms provide OOTB themes and allows you to customize an existing theme to make a brand specific theme. 


A theme contains styling details for components and panels, and you can reuse a theme in different forms. Styles include properties such as background colors, state colors, transparency, alignment, and size. When you apply the theme to your form, the specified style reflects on corresponding components of your form.

Goals:

* Apply an out of the box theme to an adaptive form.
* Create your brand specific theme.


### Step 6: Publish your adaptive form

You can publish adaptive forms as a stand-alone form (single page application), include in AEM Sites page, or include in a non-AEM Sites page.

Goals:

* Publish the adaptive form as an AEM Page.
* Embed the adaptive form in an AEM Sites Page.
* Embed the adaptive form in an external webpage (a non-AEM webpage hosted outside AEM).

-->
