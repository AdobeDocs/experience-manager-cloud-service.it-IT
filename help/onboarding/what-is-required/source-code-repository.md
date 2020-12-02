---
title: Repository del codice di origine - Cloud Services
description: Repository del codice di origine - Cloud Services
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---


# Archivio del codice sorgente {#source-code-repository}

Il programma Cloud Manager verrà fornito con provisioning automatico con il proprio repository git.

Per poter accedere al repository Git di Cloud Manager, gli utenti dovranno utilizzare un client Git con uno strumento da riga di comando, un client Git visivo indipendente o l&#39;IDE dell&#39;utente come Eclipse, IntelliJ, NetBeans.

Una volta configurato un client Git, potete gestire il repository Git dall’interfaccia utente di Cloud Manager. Per informazioni su come gestire Git utilizzando l&#39;interfaccia utente di Cloud Manager, fare riferimento a [Accesso a Git](/help/implementing/cloud-manager/accessing-git.md).

Per iniziare a sviluppare l&#39;applicazione AEM Cloud, è necessario eseguire una copia locale del codice dell&#39;applicazione estraendolo dall&#39;archivio di Cloud Manager in una posizione sul computer locale in cui desiderano creare l&#39;archivio.

```java
$ git clone {URL}
```

>[!NOTE]
>
>Un utente può estrarre una copia del proprio codice e apportare modifiche nell’archivio del codice locale. Una volta pronti, l&#39;utente può eseguire nuovamente il commit delle modifiche di codice nell&#39;archivio del codice remoto in Cloud Manager.
