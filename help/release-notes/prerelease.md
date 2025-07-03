---
title: Canale prerelease Adobe Experience Manager as a Cloud Service
description: Scopri come utilizzare il canale prerelease per ottenere un’anteprima delle prossime funzionalità su AEM as a Cloud Service.
exl-id: cfc91699-0087-40fa-a76c-0e5e1e03a5bd
feature: Release Information
role: Admin
source-git-commit: e6567c965a026967e7a5baa67050eb5615979531
workflow-type: ht
source-wordcount: '893'
ht-degree: 100%

---


# Canale prerelease Adobe Experience Manager as a Cloud Service {#prerelease-channel}

Scopri come utilizzare il canale prerelease per ottenere un’anteprima delle prossime funzionalità su AEM as a Cloud Service.

## Introduzione {#introduction}

Adobe Experience Manager as a Cloud Service offre nuove funzioni a cadenza regolare. L’elenco delle nuove e prossime funzioni per il rilascio di una data funzione è pubblicato all’interno delle [note sulla versione.](/help/release-notes/release-notes-cloud/release-notes-current.md)

Le prossime funzioni sono generalmente rese disponibili in uno dei due modi seguenti:

* Come parte di un programma Alpha, Beta o Disponibilità limitata
* Come parte del canale di pre-release

Questo documento descrive come abilitare il canale di pre-release. Il canale di pre-release fornisce l’accesso alle funzioni preliminari che verranno introdotte in una versione futura delle funzioni di AEM. Questo offre l’opportunità di convalidare le nuove funzioni e pianificarne l’adozione in vista del loro rilascio futuro. Per informazioni dettagliate sulla pianificazione del rilascio di AEM, consulta il documento [Note sulla versione di Adobe Experience Manager (AEM) as a Cloud Service](/help/release-notes/home.md).

## Abilitare il canale di pre-release per accedere e provare le prossime funzioni {#enable-prerelease}

Il canale prerelease può essere abilitato su qualsiasi ambiente di sviluppo o sandbox. Non è possibile abilitare il canale di pre-release negli ambienti di staging o produzione.

Il canale di pre-release è accessibile in due diversi modi:

* [Ambienti cloud](#cloud-environments)
* [SDK locale](#local-sdk)

### Ambienti cloud {#cloud-environments}

Per aggiornare un ambiente cloud per utilizzare il canale di pre-release, devi aggiungere una nuova variabile di ambiente. Puoi eseguire questa operazione utilizzando l’interfaccia utente di Cloud Manager o tramite CLI.

#### Aggiungere una variabile di ambiente utilizzando l’interfaccia utente {#add-with-ui}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Passa al programma in cui desideri abilitare il canale di pre-release.

1. Seleziona l’ambiente in cui desideri abilitare il canale di pre-release e accedi alla relativa configurazione tramite **Programma** > **Ambiente** > **Configurazione ambiente**.

1. Aggiungi una nuova [variabile di ambiente](/help/implementing/cloud-manager/environment-variables.md)

   | Nome | Valore | Servizio applicato | Tipo |
   |------|-------|-----------------|------|
   | `AEM_RELEASE_CHANNEL` | `prerelease` | Tutti i bundle  | Variabile |

1. Salva le modifiche; l’ambiente verrà aggiornato con il canale di pre-release abilitato.

   ![Nuova variabile di ambiente](assets/env-configuration-prerelease.png)

#### Aggiungi una variabile di ambiente utilizzando CLI {#add-with-cli}

In alternativa puoi utilizzare l’API di Cloud Manager e la CLI per aggiornare le variabili di ambiente.

* Utilizzando l’[endpoint per le variabili di ambiente dell’API di Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/patchEnvironmentVariables), imposta la `AEM_RELEASE_CHANNEL`variabile di ambiente al valore`prerelease`.

  ```text
  PATCH /program/{programId}/environment/{environmentId}/variables
  [
          {
                  "name" : "AEM_RELEASE_CHANNEL",
                  "value" : "prerelease",
                  "type" : "string"
          }
  ]
  ```

* Può essere utilizzato anche [CLI di Cloud Manager](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)

  ```shell
  aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL "prerelease
  ```

La variabile può essere eliminata se desideri ripristinare il comportamento standard dell’ambiente (canale non di pre-release).

### SDK locale {#local-sdk}

Puoi accedere alle prossime funzioni nel canale di pre-release nell’SDK Quickstart locale e nel codice relativo alle nuove API facendo riferimento al progetto Maven nel canale di pre-release `API Jar` posizionato in Maven Central. Puoi visualizzare l’accesso al canale di pre-release anche nell’ambiente di sviluppo locale avviando il regolare SDK Quickstart in modalità pre-release.

#### Avviare l’SDK di Quickstart in modalità prerelease {#prerelease-mode}

1. Scarica l’SDK dal portale di distribuzione del software e installalo come descritto in [Accesso a SDK di AEM as a Cloud Service.](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
1. Quando avvii l’SDK Quickstart, includi l’argomento `-r prerelease`.

Il valore è permanente quindi può essere selezionato solo al primo avvio. Reinstalla l’SDK per modificare l’opzione della riga di comando.

Poiché possono esservi più versioni di manutenzione AEM tra le versioni delle rilasci mensili, puoi scaricare questi nuovi SDK e fare riferimento alle nuove versioni SDK Jar nei progetti Maven. Le versioni di manutenzione non aggiungeranno ulteriori funzionalità prerelease, ma potrebbero includere altre modifiche minori, come correzioni di bug, correzioni di sicurezza e miglioramenti delle prestazioni.
Gli Javadoc vengono pubblicati in Maven Central.

#### Generare in base all’SDK della versione prerelease {#build-sdk}

1. Modifica il `pom.xml` del progetto maven per fare riferimento a un jar api sdk prerelease distinto, pubblicato su Maven Central. Contiene eventuali nuove api Java per le funzionalità prerelease e ha una dipendenza dal jar dell’api SDK. Usa la stessa versione.

   Come esempio, di seguito è riportato uno snippet dalla sezione gestione delle dipendenze del pom principale che fa riferimento al Jar API regolare:

   ```
   <dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.adobe.aem</groupId>
            <artifactId>aem-sdk-api</artifactId>
            <version>${aem.sdk.api}</version>
            <scope>provided</scope>
        </dependency>
   ```

   E quindi l’utilizzo in un modulo:

   ```
    <dependencies>
     <dependency>
         <groupId>com.adobe.aem</groupId>
         <artifactId>aem-sdk-api</artifactId>
     </dependency>
   ```

   Per passare all’SDK della versione prerelease, è sufficiente modificare la dipendenza da `com.adobe.aem:aem-sdk-api` a `com.adobe.aem:aem-prerelease-sdk-api` come indicato di seguito:

   ```
   <dependencyManagement>
    <dependencies>
      <dependency>
            <groupId>com.adobe.aem</groupId>
            <artifactId>aem-prerelease-sdk-api</artifactId>
            <version>${aem.sdk.api}</version>
            <scope>provided</scope>
      </dependency>
   <dependencies>
      <dependency>
         <groupId>com.adobe.aem</groupId>
         <artifactId>aem-prerelease-sdk-api</artifactId>
      </dependency>
   ```

   Come di consueto, i singoli progetti possono utilizzare la dipendenza.

1. Implementa sul server locale.

1. Se hai la certezza che funziona come previsto localmente, invia il codice a un ramo di sviluppo e utilizza una pipeline di non produzione di Cloud Manager per l’implementazione in un [ambiente con il canale prerelease abilitato.](#cloud-environments)

>[!CAUTION]
> 
> L’artifactId `aem-prerelease-sdk-api` non deve mai essere utilizzato per l’implementazione nell’ambiente di staging o produzione. Utilizza sempre `aem-sdk-api` quando distribuisci tramite la pipeline di produzione. Allo stesso modo, il codice che fa riferimento alle API prerelease non deve essere distribuito tramite la pipeline di produzione.

Il [plug-in maven di AEM CS SDK build Analyzer v1.0 e versioni successive](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=it#developing) rileva se l’api prerelease è utilizzata in un progetto controllando le dipendenze. Se l’analizzatore ne trova, utilizza l’API SDK prerelease per analizzare il progetto.

## Considerazioni {#considerations}

Ci sono alcuni elementi da notare quando si utilizza il canale prerelease.

* Il canale prerelease non contiene necessariamente tutte le nuove funzioni da distribuire nella versione successiva.
* Le funzioni della versione prerelease sono garantite da una qualità elevata e sono state progettate per essere complete piuttosto che per la qualità beta. Se noti eventuali problemi, segnalali, come faresti se sospettassi bug nelle funzioni in una versione AEM regolare.
* Per determinare se un ambiente è configurato per il canale prerelease, passa alla pagina **Informazioni** della console AEM e controlla se il numero di versione AEM include un suffisso `PRERELEASE` prerelease come `Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE`.

![Informazioni](/help/release-notes/assets/about.png)
