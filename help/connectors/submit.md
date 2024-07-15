---
title: Invio di un connettore AEM
description: Scopri come fare riferimento e distribuire correttamente i connettori nell’as a Cloud Service di Adobe Experience Manager (AEM).
exl-id: 9be1f00e-3666-411c-9001-c047e90b6ee5
feature: Operations
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 32%

---

# Invio di un connettore AEM

Le informazioni fornite di seguito sono utili per l&#39;invio dei connettori Adobe Experience Manager (AEM) e devono essere lette con gli articoli relativi all&#39;[implementazione](implement.md) e alla [manutenzione](maintain.md) dei connettori.

I connettori AEM sono elencati in [Adobe Exchange](https://partners.adobe.com/technologyprogram/experiencecloud.html).

Nelle soluzioni AEM precedenti, [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md) è utilizzato per installare i connettori su varie istanze AEM. Tuttavia, con AEM as a Cloud Service, i connettori vengono distribuiti durante il processo CI/CD in Cloud Manager. Per i connettori da distribuire, è necessario fare riferimento ai connettori nel file pom.xml del progetto maven.

Sono disponibili varie opzioni per l’inclusione dei pacchetti in un progetto:

1. Archivio pubblico del partner: un partner ospiterà il pacchetto di contenuti in un archivio maven accessibile al pubblico
1. Archivio protetto da password del partner: un partner ospiterà il pacchetto di contenuti in un archivio maven protetto da password. Per istruzioni, consulta [archivi Maven protetti da password](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/create-application-project/setting-up-project.html#password-protected-maven-repositories).
1. Artefatto nel pacchetto: in questo caso, il pacchetto del connettore è incluso localmente nel progetto Maven del cliente.

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

Se il partner ISV ospita il connettore su un archivio maven accessibile a Internet (ad esempio, Cloud Manager), il programma ISV deve fornire la configurazione dell&#39;archivio in cui è possibile inserire `pom.xml`. Il motivo è che le dipendenze del connettore (sopra) possono essere risolte in fase di build, sia localmente che da Cloud Manager.

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

Se il partner ISV sceglie di distribuire il connettore come file scaricabili, il programma ISV deve fornire le istruzioni necessarie. L’istruzione deve descrivere come i file possono essere distribuiti in un archivio maven di un file system locale che deve essere archiviato in Git come parte del progetto AEM. In questo modo Cloud Manager può risolvere queste dipendenze.
