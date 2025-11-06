---
title: Supporto per i sottomoduli Git
description: Scopri come i moduli Git secondari possono essere utilizzati per unire il contenuto di più rami tra archivi Git diversi al momento della creazione.
exl-id: fa5b0f49-4b87-4f39-ad50-7e62094d85f4
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 24%

---

# Supporto dei moduli Git secondari per gli archivi Adobe {#git-submodule-support}

I moduli Git secondari possono essere utilizzati per unire il contenuto di più rami tra archivi Git al momento della creazione.

Quando il processo di build di Cloud Manager viene eseguito, clona l’archivio della pipeline ed estrae il ramo. Se nella directory principale del ramo è presente un file `.gitmodules`, viene eseguito il comando corrispondente.

Il comando seguente estrae ogni sottomodulo nella directory appropriata.

```
$ git submodule update --init
```

Questa tecnica offre un&#39;alternativa alla soluzione descritta in [Utilizzo di più archivi Git di Source](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md). È ideale per le organizzazioni che hanno familiarità con i moduli Git secondari e preferiscono non gestire un processo di unione esterno.

Ad esempio, supponiamo che ci siano tre archivi. Ogni repository contiene un singolo ramo denominato `main`. Nell&#39;archivio principale, ovvero quello configurato nelle pipeline, il ramo `main` ha un file `pom.xml` che dichiara i progetti contenuti negli altri due archivi:

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

Aggiungi quindi i sottomoduli per gli altri due archivi:

```shell
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

Il risultato è un file `.gitmodules` simile al seguente:

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

Per ulteriori informazioni sui sottomoduli Git, vedere anche il [Manuale di riferimento Git](https://git-scm.com/book/en/v2/Git-Tools-Submodules).

## Note sull’utilizzo degli archivi Adobe {#usage-notes-recommendations-adobe-repos}

* La sintassi dell’URL Git deve essere esattamente quella descritta nella sezione precedente.
* I moduli secondari sono supportati unicamente nella radice del ramo.
* Per motivi di sicurezza, non incorporare le credenziali negli URL Git.
* Se non diversamente necessario, Adobe consiglia di utilizzare i sottomoduli superficiali eseguendo quanto segue:
  `git config -f .gitmodules submodule.<submodule path>.shallow true` per ogni sottomodulo.
* I riferimenti ai moduli secondari vengono memorizzati in commit Git specifici. Di conseguenza, quando vengono apportate modifiche all’archivio dei sottomoduli, il commit a cui si fa riferimento deve essere aggiornato.
Ad esempio, utilizzando quanto segue:

  `git submodule update --remote`

## Supporto dei moduli Git secondari per archivi privati {#private-repositories}

Il supporto per i moduli Git secondari in [archivi privati](private-repositories.md) è generalmente simile al loro utilizzo con gli archivi Adobe.

Tuttavia, dopo aver configurato il file `pom.xml` e aver eseguito i comandi `git submodule`, è necessario aggiungere un file `.gitmodules` alla directory radice dell&#39;archivio di aggregazione affinché Cloud Manager riconosca la configurazione del sottomodulo.

![File .gitmodules](assets/gitmodules.png)

![Aggregatore](assets/aggregator.png)

### Note sull’utilizzo {#usage-notes-recommendations-private-repos}

* Gli URL Git del sottomodulo possono essere in formato HTTPS o SSH, ma devono puntare a un archivio GitHub.com. L’aggiunta di un sottomodulo dell’archivio Adobe a un archivio di aggregazione GitHub o viceversa non è supportata.
* I sottomoduli GitHub devono essere accessibili dall’app GitHub di Adobe.
* Si applicano anche le [limitazioni all’utilizzo dei moduli Git secondari con archivi gestiti da Adobe](#usage-notes-recommendations-adobe-repos).
