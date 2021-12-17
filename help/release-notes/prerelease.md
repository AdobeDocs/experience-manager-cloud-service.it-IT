---
title: '[!DNL Adobe Experience Manager] Canale pre-rilascio as a Cloud Service'
description: '[!DNL Adobe Experience Manager] Canale pre-rilascio as a Cloud Service'
exl-id: cfc91699-0087-40fa-a76c-0e5e1e03a5bd
source-git-commit: 6cd454eaf70400f3507bc565237567cace66991f
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager] Canale pre-rilascio as a Cloud Service {#prerelease-channel}


## Introduzione {#introduction}

[!DNL Adobe Experience Manager] as a Cloud Service offre nuove funzionalità su cadenza mensile, in base alla pianificazione [Roadmap dei rilasci di Experienci Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=en#aem-as-cloud-service). Per acquisire familiarità con le funzioni programmate per andare in diretta il mese successivo, i clienti possono iscriversi al canale pre-rilascio, che è accessibile configurando in modo appropriato negli ambienti di sviluppo dei programmi standard o in qualsiasi ambiente di programma sandbox. I clienti possono visualizzare in anteprima le modifiche apportate alla console Sites e generare il codice rispetto a qualsiasi nuova API prerelease.

L’elenco delle funzioni prerelease per un dato mese è pubblicato all’interno di [note sulla versione mensili](/help/release-notes/release-notes-cloud/release-notes-current.md).

>[!VIDEO](/help/release-notes/assets/prerelease-overview.mp4)

## Come abilitare la versione pre-rilascio {#enable-prerelease}

Le funzioni prerelease possono essere utilizzate in diversi modi:

* Ambienti cloud (ambienti di sviluppo di programmi standard o qualsiasi tipo di ambiente di programmi sandbox)
* SDK locale

### Ambienti cloud {#cloud-environments}

Per visualizzare le nuove funzioni nella console Sites negli ambienti di sviluppo cloud e il risultato di eventuali personalizzazioni del progetto:

* Utilizzo della [Endpoint per le variabili di ambiente dell’API di Cloud Manager](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Variables/patchEnvironmentVariables), imposta le **AEM_RELEASE_CHANNEL** variabile di ambiente al valore **prerelease**.

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

È inoltre possibile utilizzare Cloud Manager CLI, come indicato nelle istruzioni all’indirizzo [https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)
```aio cloudmanager:environment:set-variables <ENVIRONMENT_ID> --programId=<PROGRAM_ID> --variable AEM_RELEASE_CHANNEL “prerelease”```


La variabile può essere eliminata o impostata su un valore diverso se desideri che l’ambiente venga ripristinato al comportamento del canale normale (non pre-rilascio)

* In alternativa, puoi anche configurare le variabili di ambiente dal [Interfaccia utente di Cloud Manager](/help/implementing/cloud-manager/environment-variables.md).

### SDK locale {#local-sdk}

Puoi vedere le nuove funzioni nella console Sites nell’SDK Quickstart locale e il codice relativo alle nuove API nella versione prerelease facendo riferimento al progetto maven nella versione prerelease `API Jar` situato in Maven Central. Puoi anche vedere queste funzioni prerelease nel computer locale avviando il normale SDK Quickstart in modalità prerelease:

* Scarica l’SDK dal portale di distribuzione del software e installalo come descritto in [Accesso all’SDK AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).
* Quando avvii l&#39;SDK Quickstart, includi l&#39;argomento `-r prerelease`.
* Il valore è *appiccicoso* quindi può essere selezionato solo al primo avvio. Reinstalla l&#39;SDK per modificare l&#39;opzione della riga di comando.

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

   Come di consueto, i singoli progetti possono utilizzare la dipendenza .

1. Distribuisci sul server locale
1. Se si è certi che funziona come previsto localmente, invia il codice a un ramo di sviluppo e utilizza una pipeline di non produzione di Cloud Manager per l’implementazione in un ambiente che si abbona al canale prerelease

>[!CAUTION]
> 
> La `aem-prerelease-sdk-api` artifactId non deve mai essere utilizzato quando si distribuisce in Stage o Production. Utilizza sempre l’api aem-sdk-api quando distribuisci tramite la pipeline di produzione. Allo stesso modo, il codice che fa riferimento alle API prerelease non deve essere distribuito tramite la pipeline di produzione .

La [Plug-in maven di AEM CS SDK build Analyzer v1.0 e versioni successive](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing) rileva se l’api prerelease è utilizzata in un progetto controllando le dipendenze. Se l’analizzatore lo trova, utilizza l’api sdk prerelease per analizzare il progetto.

## Considerazioni {#considerations}

Ci sono alcune cose da notare quando si tratta del canale prerelease:

* Alcune funzionalità che verranno implementate nella versione del mese successivo potrebbero non essere incluse nel canale prerelease.
* Le funzioni della versione prerelease sono garantite da una qualità elevata e sono state progettate per essere complete piuttosto che per la qualità beta. Se noti eventuali problemi, segnalali, come faresti se sospetti bug nelle funzioni in una versione AEM regolare.
* Per determinare se un ambiente è configurato per il canale prerelease, vai alla console AEM **Informazioni** e controlla se il numero di versione AEM include un *prerelease* suffisso come ```Adobe Experience Manager 2021.4.5226.20210427T070726Z-210429-PRERELEASE```.

![informazioni](/help/release-notes/assets/about.png)
