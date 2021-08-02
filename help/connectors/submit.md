---
title: Invio di un connettore AEM
description: Invio di un connettore AEM
exl-id: 9be1f00e-3666-411c-9001-c047e90b6ee5
source-git-commit: 4b6d02bc93a904c8ca666d027923fa5df88d1934
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 11%

---

Invio di un connettore AEM
===========================

Seguono informazioni utili per l’invio dei connettori AEM, che devono essere lette insieme agli articoli relativi all’[implementazione](implement.md) e alla [manutenzione](maintain.md) dei connettori.

I connettori AEM sono elencati in [Adobe Exchange](https://partners.adobe.com/exchangeprogram/experiencecloud).

Nelle soluzioni AEM precedenti, Gestione pacchetti era utilizzato per installare connettori su varie istanze AEM. Tuttavia, con AEM come Cloud Service, i connettori vengono distribuiti durante il processo CI/CD in Cloud Manager. Per implementare i connettori, è necessario fare riferimento ai connettori nel file pom.xml del progetto maven.

Sono disponibili varie opzioni per l’inclusione dei pacchetti in un progetto:

1. Archivio pubblico del partner : un partner ospiterà il pacchetto di contenuti in un archivio maven accessibile al pubblico
1. Archivio protetto da password del partner : un partner ospiterà il pacchetto di contenuti in un archivio maven protetto da password. Per istruzioni, consulta [archivi Maven protetti da password](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/create-application-project/setting-up-project.html?lang=en#password-protected-maven-repositories) .
1. Artefatto nel pacchetto : in questo caso, il pacchetto del connettore è incluso localmente nel progetto Maven del cliente.

Indipendentemente da dove sono ospitati, i pacchetti devono essere indicati come dipendenze nel pom.xml, come fornito dal fornitore.

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

Se il partner ISV ospita il connettore su un archivio maven accessibile a Internet (ad esempio, con accesso a Cloud Manager), il programma ISV deve fornire la configurazione dell’archivio in cui è possibile inserire il file pom.xml, in modo che le dipendenze del connettore (sopra) possano essere risolte in fase di creazione (sia localmente che da Cloud Manager).

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

Se il partner ISV sceglie di distribuire il connettore come file scaricabili, il programma ISV dovrebbe fornire istruzioni su come i file possono essere distribuiti in un archivio maven di un file system locale che deve essere sottoposto a Check-In come parte del progetto AEM, in modo che Cloud Manager possa risolvere queste dipendenze.
