---
title: Repository del codice sorgente - Servizi cloud
description: Repository del codice sorgente - Servizi cloud
translation-type: tm+mt
source-git-commit: 6f323f33663f83043eb8a15fe00e6ed872c3cac1

---


# Repository del codice sorgente {#source-code-repository}

Il programma Cloud Manager verrà fornito con provisioning automatico con il proprio repository git.

Per poter accedere al repository Git di Cloud Manager, gli utenti dovranno utilizzare un client Git con uno strumento da riga di comando, un client Git visivo indipendente o l&#39;IDE dell&#39;utente come Eclipse, IntelliJ, NetBeans.

Una volta configurato un client Git, potete gestire il repository Git dall’interfaccia utente di Cloud Manager. Per informazioni su come gestire Git utilizzando l’interfaccia utente di Cloud Manager, consulta [Accesso a Git](/help/implementing/cloud-manager/accessing-git.md).

Per iniziare a sviluppare l’applicazione AEM Cloud, è necessario eseguire una copia locale del codice dell’applicazione estraendolo dall’archivio di Cloud Manager in una posizione sul computer locale in cui desiderano creare l’archivio.

```java
$ git clone {URL}
```

> [!NOTE]
> Un utente può estrarre una copia del proprio codice e apportare modifiche nell’archivio del codice locale. Una volta pronti, l&#39;utente può eseguire nuovamente il commit delle modifiche di codice nell&#39;archivio del codice remoto in Cloud Manager.
