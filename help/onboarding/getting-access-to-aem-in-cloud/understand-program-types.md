---
title: Informazioni sui tipi di programma e di programma
description: Informazioni sui tipi di programma e di programma - Cloud Services
translation-type: tm+mt
source-git-commit: 6e8cf08ec3f85437a8472a45895f3818e473e98c
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 2%

---


# Informazioni su programmi e tipi di programmi {#understanding-programs}

In Cloud Manager, l’entità tenant è nella parte superiore che può contenere più programmi. Ogni programma può contenere non più di un ambiente di produzione e più ambienti non di produzione.

Il diagramma seguente mostra la gerarchia delle entità in Cloud Manager.

![immagine](assets/program-types1.png)

## Archivio del codice sorgente {#source-code-repository}

Il programma Cloud Manager viene fornito con provisioning automatico con il proprio archivio Git.

Per consentire a un utente di accedere all’archivio Git di Cloud Manager, gli utenti dovranno utilizzare un client Git con uno strumento a riga di comando, un client Git visivo indipendente o l’IDE dell’utente come Eclipse, IntelliJ, NetBeans.

Una volta configurato un client Git, puoi gestire l’archivio Git dall’interfaccia utente di Cloud Manager. Per informazioni su come gestire Git utilizzando l’interfaccia utente di Cloud Manager, consulta [Accesso a Git](/help/implementing/cloud-manager/accessing-git.md).

Per iniziare a sviluppare l’applicazione AEM Cloud, è necessario creare una copia locale del codice dell’applicazione estraendolo dall’archivio Cloud Manager in una posizione sul computer locale in cui desiderano creare il proprio archivio.

```java
$ git clone {URL}
```

>[!NOTE]
>Un utente può estrarre una copia del proprio codice e apportare modifiche nell&#39;archivio del codice locale. Quando è pronto, l’utente può eseguire nuovamente il commit delle modifiche del codice nell’archivio del codice remoto in Cloud Manager.

## Tipi di programmi {#program-types}

Un utente può creare un programma **Sandbox** o **Produzione**.

* Viene creato un *programma di produzione* per abilitare il traffico live al momento appropriato in futuro.
Per ulteriori informazioni, consulta [Introduzione ai programmi di produzione](/help/onboarding/getting-access-to-aem-in-cloud/introduction-production-programs.md) .


* Un *programma sandbox* viene generalmente creato per scopi di formazione, esecuzione di demo, abilitazione, POC o documentazione. Non è destinato a trasportare traffico live e avrà restrizioni che un programma di produzione non intende. Includerà Sites e Assets e verrà fornito automaticamente con un ramo Git che include codice di esempio, un ambiente di sviluppo e una pipeline non di produzione.
Per ulteriori informazioni, consulta [Introduzione ai programmi sandbox](/help/onboarding/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md) .

