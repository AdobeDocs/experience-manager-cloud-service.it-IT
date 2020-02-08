---
title: Invio di un connettore AEM
description: Invio di un connettore AEM
translation-type: tm+mt
source-git-commit: 629de3a9f55d2e4c52ef91c9e0bb5d439aebe84f

---


Invio di un connettore AEM
===========================

Di seguito sono riportate informazioni utili per l&#39;invio dei connettori AEM e devono essere lette insieme agli articoli sull&#39; [implementazione](implement.md) e la [manutenzione](maintain.md) dei connettori.

I connettori AEM sono elencati in [Adobe Exchange](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace.html).

Nelle precedenti soluzioni AEM, Package Manager era utilizzato per installare i connettori su varie istanze di AEM. Tuttavia, con AEM come servizio cloud, i connettori vengono distribuiti durante il processo CI/CD in Cloud Manager. Affinché i connettori vengano distribuiti, è necessario fare riferimento ai connettori nel file pom.xml del progetto maven.

Esistono diverse opzioni per l’inclusione dei pacchetti in un progetto:

1. Archivio pubblico del partner: un partner ospiterà il pacchetto di contenuti in un archivio Web accessibile al pubblico
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

Se il partner ISV sceglie di distribuire il connettore come file scaricabili, il ISV deve fornire istruzioni su come i file possono essere distribuiti in un archivio locale del file system che deve essere sottoposto a check-in Git nell’ambito del progetto AEM, in modo che Cloud Manager possa risolvere tali dipendenze.
