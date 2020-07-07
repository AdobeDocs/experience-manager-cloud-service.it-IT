---
title: Repository del codice sorgente - Servizi cloud
description: Repository del codice sorgente - Servizi cloud
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---


# Archivio del codice sorgente {#source-code-repository}

Il programma Cloud Manager verrà fornito con provisioning automatico con il proprio repository git.

Per poter accedere al repository Git di Cloud Manager, gli utenti dovranno utilizzare un client Git con uno strumento da riga di comando, un client Git visivo indipendente o l&#39;IDE dell&#39;utente come Eclipse, IntelliJ, NetBeans.

Once a Git client is set up, you can manage your git repository from the Cloud Manager UI. Per informazioni su come gestire Git utilizzando l’interfaccia utente di Cloud Manager, consulta [Accesso a Git](/help/implementing/cloud-manager/accessing-git.md).

Per iniziare a sviluppare l’applicazione AEM Cloud, è necessario eseguire una copia locale del codice dell’applicazione estraendolo dall’archivio di Cloud Manager in una posizione sul computer locale in cui desiderano creare l’archivio.

```java
$ git clone {URL}
```

>[!NOTE]
>
>Un utente può estrarre una copia del proprio codice e apportare modifiche nell’archivio del codice locale. When ready, the user can commit their code changes back to the remote code repository in Cloud Manager.
