---
title: Archivio del codice sorgente - Cloud Services
description: Archivio del codice sorgente - Cloud Services
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---


# Archivio del codice sorgente {#source-code-repository}

Il programma Cloud Manager viene fornito con provisioning automatico con il proprio archivio Git.

Per consentire a un utente di accedere all’archivio Git di Cloud Manager, gli utenti dovranno utilizzare un client Git con uno strumento a riga di comando, un client Git visivo indipendente o l’IDE dell’utente come Eclipse, IntelliJ, NetBeans.

Una volta configurato un client Git, puoi gestire l’archivio Git dall’interfaccia utente di Cloud Manager. Per informazioni su come gestire Git utilizzando l’interfaccia utente di Cloud Manager, consulta [Accesso a Git](/help/implementing/cloud-manager/accessing-git.md).

Per iniziare a sviluppare l’applicazione AEM Cloud, è necessario creare una copia locale del codice dell’applicazione estraendolo dall’archivio Cloud Manager in una posizione sul computer locale in cui desiderano creare il proprio archivio.

```java
$ git clone {URL}
```

>[!NOTE]
>
>Un utente può estrarre una copia del proprio codice e apportare modifiche nell&#39;archivio del codice locale. Quando è pronto, l’utente può eseguire nuovamente il commit delle modifiche del codice nell’archivio del codice remoto in Cloud Manager.
