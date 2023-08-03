---
title: Invio di un connettore AEM
description: Scopri come distribuire i connettori utilizzando Cloud Manager.
exl-id: 9be1f00e-3666-411c-9001-c047e90b6ee5
source-git-commit: f7ffe727ecc7f1331c1c72229a5d7f940070c011
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 97%

---

Invio di un connettore AEM
===========================

Seguono informazioni utili per l’invio dei connettori AEM, che devono essere lette insieme agli articoli relativi all’[implementazione](implement.md) e alla [manutenzione](maintain.md) dei connettori.

I connettori AEM sono elencati in [Adobe Exchange](https://partners.adobe.com/exchangeprogram/experiencecloud).

Nelle soluzioni AEM precedenti, [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md) è utilizzato per installare i connettori su varie istanze AEM. Tuttavia, con AEM as a Cloud Service, i connettori vengono distribuiti durante il processo CI/CD in Cloud Manager. Per implementare i connettori, è necessario fare riferimento ai connettori nel file pom.xml del progetto maven.

Sono disponibili varie opzioni per l’inclusione dei pacchetti in un progetto:

1. Archivio pubblico del partner: un partner ospiterà il pacchetto di contenuti in un archivio maven accessibile al pubblico
1. Archivio protetto da password del partner: un partner ospiterà il pacchetto di contenuti in un archivio maven protetto da password. Vedi [archivi Maven protetti da password](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/create-application-project/setting-up-project.html?lang=it#password-protected-maven-repositories) per le istruzioni.
1. Artefatto nel pacchetto: in questo caso, il pacchetto del connettore è incluso localmente nel progetto Maven del cliente.

Indipendentemente da dove sono ospitati, i pacchetti devono essere indicati come dipendenze nel pom.xml, come definito dal fornitore.

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

Se il partner ISV sceglie di distribuire il connettore come file scaricabili, il programma ISV dovrebbe fornire istruzioni su come i file possono essere distribuiti in un archivio maven di un file system locale che deve essere inserito in Git come parte del progetto AEM, in modo che Cloud Manager possa risolvere queste dipendenze.
