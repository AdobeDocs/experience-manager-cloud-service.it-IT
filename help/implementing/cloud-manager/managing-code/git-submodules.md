---
title: Supporto per i sottomoduli Git
description: Scopri come i sottomoduli Git possono essere utilizzati per unire il contenuto di più rami tra archivi Git diversi in fase di creazione.
exl-id: fa5b0f49-4b87-4f39-ad50-7e62094d85f4
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 93%

---

# Supporto dei sottomoduli Git per gli archivi Adobe {#git-submodule-support}

È possibile utilizzare i moduli Git secondari per unire il contenuto di più rami tra archivi Git al momento della generazione.

Quando viene eseguito il processo di build di Cloud Manager, dopo la clonazione dell’archivio configurato per la pipeline e l’estrazione del ramo configurato, se il ramo contiene un file `.gitmodules` nella directory radice il comando viene eseguito.

Il comando seguente estrae ogni modulo secondario nella directory appropriata.

```
$ git submodule update --init
```

Questa tecnica rappresenta una potenziale alternativa alla soluzione descritta nel documento [Utilizzo di più archivi Git di origine](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md) per le organizzazioni che hanno familiarità con l’utilizzo dei moduli Git secondari e non desiderano gestire un processo di unione esterno.

Supponiamo ad esempio la presenza di tre archivi, ciascuno contenente un singolo ramo denominato `main`. Nell’archivio principale, ovvero quello configurato nelle pipeline, il ramo `main` include un file `pom.xml` dove sono riportati i progetti contenuti negli altri due archivi.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
   
    <groupId>customer.group.id</groupId>
    <artifactId>customer-reactor</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
   
    <modules>
        <module>project-a</module>
        <module>project-b</module>
    </modules>
   
</project>
```

A questo punto, si aggiungono i moduli secondari degli altri due archivi.

```shell
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

Questo determina un file `.gitmodules` simile al seguente.

```text
[submodule "project-a"]
    path = project-a
    url = https://git.cloudmanager.adobe.com/ProgramName/projectA/
    branch = main
[submodule "project-b"]
    path = project-b
    url = https://git.cloudmanager.adobe.com/ProgramName/projectB/
    branch = main
```

Per ulteriori informazioni sui moduli Git secondari, consulta il [Manuale di riferimento Git.](https://git-scm.com/book/en/v2/Git-Tools-Submodules)

### Limitazioni e consigli {#limitations-recommendations}

Quando utilizzi i sottomoduli Git con archivi gestiti da Adobe, tieni presente le seguenti limitazioni.

* La sintassi dell’URL Git deve essere esattamente quella descritta nella sezione precedente.
* I moduli secondari sono supportati unicamente nella radice del ramo.
* Per motivi di sicurezza, non incorporare le credenziali negli URL Git.
* Se non diversamente necessario, è consigliabile utilizzare dei moduli secondari superficiali.
   * Per eseguire l’operazione, esegui `git config -f .gitmodules submodule.<submodule path>.shallow true` per ciascun modulo secondario.
* I riferimenti ai moduli Git secondari vengono archiviati in commit Git specifici. Di conseguenza, quando vengono apportate modifiche all’archivio dei sottomoduli, il commit a cui si fa riferimento deve essere aggiornato.
   * Ad esempio, utilizzando `git submodule update --remote`. 

## Supporto dei sottomoduli Git per archivi privati {#private-repositories}

Il supporto dei sottomoduli Git quando si utilizzano [archivi privati](private-repositories.md) è in gran parte lo stesso di quando si utilizzano archivi Adobe.

Tuttavia, dopo aver configurato il file `pom.xml` e aver eseguito i comandi `git submodule`, affinché Cloud Manager possa rilevare la configurazione del sottomodulo è necessario aggiungere un file `.gitmodules` nella directory principale dell’archivio dell’aggregatore.

![File .gitmodules](assets/gitmodules.png)

![Aggregatore](assets/aggregator.png)

### Limitazioni e consigli {#limitations-recommendations-private-repos}

Quando utilizzi dei sottomoduli Git con archivi privati, tieni presente le seguenti limitazioni.

* Gli URL Git per i sottomoduli possono essere in formato HTTPS o SSH, ma devono essere collegati a un archivio github.com
   * L’aggiunta di un sottomodulo dell’archivio Adobe a un archivio di aggregazione GitHub o viceversa non funziona.
* I sottomoduli GitHub devono essere accessibili all’app GitHub Adobe.
* Si applicabili anche le [limitazioni dell’utilizzo dei sottomoduli Git con archivi gestiti da Adobe](#limitations-recommendations).
