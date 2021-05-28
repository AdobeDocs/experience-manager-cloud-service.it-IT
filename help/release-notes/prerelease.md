---
title: '[!DNL Adobe Experience Manager] come canale pre-rilascio Cloud Service'
description: '[!DNL Adobe Experience Manager] come canale pre-rilascio Cloud Service'
source-git-commit: 4ee9a5744cdcec00dd497a00b0d8dbf288a5adcb
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---


# [!DNL Adobe Experience Manager] come canale pre-rilascio Cloud Service  {#prerelease-channel}


## Introduzione {#introduction}

[!DNL Adobe Experience Manager] come Cloud Service offre nuove funzioni su cadenza mensile, in base alla pianificazione della roadmap dei rilasci di  [Experienci Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=en#aem-as-cloud-service). Per acquisire familiarità con le funzioni programmate per andare in diretta il mese successivo, i clienti possono iscriversi al canale pre-rilascio, che è accessibile configurando in modo appropriato negli ambienti di sviluppo dei programmi standard o in qualsiasi ambiente di programma sandbox. I clienti possono visualizzare in anteprima le modifiche apportate alla console Sites e generare il codice rispetto a qualsiasi nuova API prerelease.

L&#39;elenco delle funzioni prerelease per un dato mese è pubblicato nelle [note sulla versione mensili](/help/release-notes/release-notes-cloud/release-notes-current.md).

>[!VIDEO](/help/release-notes/assets/prerelease-overview.mp4)

## Come abilitare la versione pre-rilascio {#enable-prerelease}

Le funzioni prerelease possono essere utilizzate in diversi modi:

* Ambienti cloud (ambienti di sviluppo di programmi standard o qualsiasi tipo di ambiente di programmi sandbox)
* SDK locale

### Ambienti cloud {#cloud-environments}

Per visualizzare le nuove funzioni nella console Sites negli ambienti di sviluppo cloud e il risultato di eventuali personalizzazioni del progetto:

* Utilizzando l&#39;endpoint delle variabili di ambiente [Cloud Manager API](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Variables/patchEnvironmentVariables), imposta la variabile di ambiente **AEM_RELEASE_CHANNEL** sul valore **prerelease**.

```
PATCH /program/{programId}/environment/{environmentId}/variables
[
        {
                "name" : "AEM_RELEASE_CHANNEL",
                "value" : "prerelease",
                "type" : "string"
        }
]
```

È inoltre possibile utilizzare Cloud Manager CLI, come da istruzioni all&#39;indirizzo [https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)
```aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL “prerelease”```


La variabile può essere eliminata o impostata su un valore diverso se desideri che l’ambiente venga ripristinato al comportamento del canale normale (non pre-rilascio)

### SDK locale {#local-sdk}

Puoi vedere le nuove funzioni nella console Sites nell’SDK di Quickstart locale e il codice per le nuove API nella versione prerelease facendo riferimento al progetto maven `API Jar` nella versione prerelease  di Maven Central. Puoi anche vedere queste funzioni prerelease nel computer locale avviando il normale SDK Quickstart in modalità prerelease:

* Scarica l&#39;SDK dal portale di distribuzione software e installalo come descritto in [Accesso al AEM come SDK di Cloud Service](/help/implementing/developing/aem-as-a-cloud-service-sdk.md#accessing-the-aem-as-a-cloud-service-sdk.)
* Quando avvii l&#39;SDK Quickstart, includi l&#39;argomento `-r prerelease`.
* Il valore è *fisso*, quindi può essere selezionato solo al primo avvio. Reinstalla l&#39;SDK per modificare l&#39;opzione della riga di comando.

Poiché possono esservi più versioni di manutenzione AEM tra le versioni delle funzioni mensili, puoi scaricare questi nuovi SDK e fare riferimento alle nuove versioni SDK Jar nei progetti Maven. Le versioni di manutenzione non aggiungeranno ulteriori funzionalità prerelease, ma potrebbero includere altre modifiche minori, come correzioni di bug, correzioni di sicurezza e miglioramenti delle prestazioni.
Gli JavaScript vengono pubblicati in Maven Central.

Per generare in base all’SDK della versione prerelease:

1. modifica il pom.xml del progetto maven per fare riferimento a un jar api sdk prerelease distinto, pubblicato su Maven Central. Contiene eventuali nuove api Java per le funzionalità prerelease e ha una dipendenza dal jar dell’api sdk. Usa la stessa versione.

   Ad esempio, di seguito è riportato uno snippet dalla sezione gestione delle dipendenze del pom padre che fa riferimento al Jar API regolare:

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

   E poi l&#39;utilizzo in un modulo:

   ```
    <dependencies>
     <dependency>
         <groupId>com.adobe.aem</groupId>
         <artifactId>aem-sdk-api</artifactId>
     </dependency>
   ```

   Per passare all’SDK della versione pre-rilascio, modifica semplicemente la dipendenza da `com.adobe.aem:aem-sdk-api` a `com.adobe.aem:aem-prerelease-sdk-api` come indicato di seguito:

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

   Come di consueto, i singoli progetti possono utilizzare la dipendenza .

1. Distribuisci sul server locale
1. Se si è certi che funziona come previsto localmente, effettua il commit del codice in un ramo di sviluppo e utilizza una pipeline non di produzione di Cloud Manager per l’implementazione in un ambiente che si abbona al canale prerelease

>[!CAUTION]
L’ `aem-prerelease-sdk-api` artifactId non deve mai essere utilizzato durante la distribuzione in Stage o Production. Utilizza sempre l’api aem-sdk-api quando distribuisci tramite la pipeline di produzione. Allo stesso modo, il codice che fa riferimento alle API prerelease non deve essere distribuito tramite la pipeline di produzione .

Il plug-in maven di [AEM CS SDK build Analyzer v1.0 e versioni successive](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing) rileverà se l&#39;api prerelease è utilizzata in un progetto ispezionando le dipendenze. Se l’analizzatore lo trova, utilizza l’api sdk prerelease per analizzare il progetto.

## Considerazioni {#considerations}

Ci sono alcune cose da notare quando si tratta del canale prerelease:

* Alcune funzionalità che verranno implementate nella versione del mese successivo potrebbero non essere incluse nel canale prerelease.
* Le funzioni della versione prerelease sono garantite da una qualità elevata e sono state progettate per essere complete piuttosto che per la qualità beta. Se noti eventuali problemi, segnalali, come faresti se sospetti bug nelle funzioni in una versione AEM regolare.
* Per determinare se un ambiente è configurato per il canale prerelease, vai alla pagina **Informazioni su** della console AEM e controlla se il numero di versione AEM include un suffisso *prerelease* come ```Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE```.

![informazioni](/help/release-notes/assets/about.png)
