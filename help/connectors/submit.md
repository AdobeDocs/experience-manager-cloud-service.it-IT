---
title: Invio di un connettore AEM
description: Invio di un connettore AEM
translation-type: tm+mt
source-git-commit: d4e376ab30bb3e1fb533ed32f6ac43580775787c
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 11%

---


Invio di un connettore AEM
===========================

Seguono informazioni utili per l’invio dei connettori AEM, che devono essere lette insieme agli articoli relativi all’[implementazione](implement.md) e alla [manutenzione](maintain.md) dei connettori.

AEM Connettori sono elencati in [Adobe Exchange](https://partners.adobe.com/exchangeprogram/experiencecloud).

Nelle soluzioni AEM precedenti, Package Manager veniva utilizzato per installare i connettori su varie istanze AEM. Tuttavia, con AEM come Cloud Service, i connettori vengono distribuiti durante il processo CI/CD in Cloud Manager. Affinché i connettori vengano distribuiti, è necessario fare riferimento ai connettori nel file pom.xml del progetto maven.

Esistono diverse opzioni per l’inclusione dei pacchetti in un progetto:

1. Archivio pubblico del partner: un partner ospiterà il pacchetto di contenuti in un archivio Web accessibile al pubblico
1. Archivio protetto da password del partner: un partner ospita il pacchetto di contenuti in un archivio Web protetto da password. Per istruzioni, consultate i repository [protetti tramite](/help/onboarding/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories) password all&#39;indirizzo .
1. Artefatto in bundle - in questo caso, il pacchetto di connettori è incluso localmente nel progetto del cliente.

Indipendentemente da dove sono ospitati, i pacchetti devono essere indicati come dipendenze nel file pom.xml, come fornito dal fornitore.

```xml
<!-- UberJAR Dependency to be added to the project's Reactor pom.xml -->
<dependency>
  <groupId>com.partnername</groupId>
  <artifactId>my-artifact</artifactId>
  <version>V123</version> <!-- use the latest! -->
  <scope>provided</scope>
  <classifier>my_classifier</classifier>
</dependency>
```

Se il partner ISV ospita il connettore su un archivio Web accessibile a Internet (ad esempio, con accesso facilitato a Cloud Manager), il ISV deve fornire la configurazione del repository in cui è possibile inserire il file pom.xml, in modo che le dipendenze del connettore (sopra) possano essere risolte in fase di creazione (sia localmente che da Cloud Manager).

```xml
<repository>
    <id>the-repository</id>
    <name>The Repository Where the Connector is Hosted</name>
    <url>https://repo.partnername.com/repositories/aem_connector_repo</url>
    <releases>
        <enabled>true</enabled>
        <updatePolicy>never</updatePolicy>
    </releases>
    <snapshots>
        <enabled>false</enabled>
    </snapshots>
</repository>
```

Se il partner ISV sceglie di distribuire il connettore come file scaricabili, il ISV deve fornire istruzioni su come i file possono essere distribuiti in un repository locale del sistema di file system che deve essere sottoposto a check-in Git come parte del progetto AEM, in modo che Cloud Manager possa risolvere tali dipendenze.
