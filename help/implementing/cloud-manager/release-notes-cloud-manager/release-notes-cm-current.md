---
title: Note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.8.0
description: Note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.8.0
feature: Informazioni sulla versione
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
source-git-commit: d04194bd83ced844dffc94da35c996d363c5ba30
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 4%

---

# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2021.8.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.8.0.

>[!NOTE]
>Per visualizzare il Cloud Service delle note sulla versione corrente per Adobe Experience Manager, fai clic [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=it).

## Data di rilascio {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.8.0 è il 12 agosto 2021.
La prossima versione è prevista per il 9 settembre 2021.

### Novità {#what-is-new}

* I clienti del Cloud Service ora possono visualizzare i rapporti SLA (Service Level Agreement) in Cloud Manager. Ciò sarà progressivamente reso disponibile nei prossimi mesi.
Per ulteriori informazioni, consulta [Generazione di rapporti SLA](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html) .

* Il tipo e la gravità delle regole di qualità IndexType e `IndexDamAssetLucene` sono stati modificati. Questi sono ora due bug di Blocker *serverity*.

* Sono state introdotte nuove regole sulla qualità dell&#39;indice Oak per coprire configurazioni asincrone e tika.

* Aumenta il numero massimo di certificati SSL per programma a 50.

* Funzionalità self-service per consentire agli utenti di creare e gestire più archivi tramite l’interfaccia utente di Cloud Manager.

* SonarQube leggeva inutilmente i dati della cronologia Git. Su basi di codice di grandi dimensioni, ciò potrebbe comportare una multa non necessaria per le prestazioni della build.

* È ora disponibile un’API per annullare la validità della cache di dipendenza Maven per pipeline.

* La versione di AEM Project Archetype utilizzata da Cloud Manager è stata aggiornata alla versione 29.

### Correzioni di bug {#bug-fixes}

* Lo stato Aggiorna disponibile non deve essere visualizzato quando l&#39;ultima versione è inferiore alla versione corrente.

* L&#39;onboarding iniziale non riusciva per le nuove organizzazioni con nomi molto lunghi.

* Talvolta, quando una pipeline viene attivata due volte per qualche motivo, si verifica un errore di una delle esecuzioni che non riesce con *non è in grado di aggiornare lo stato di esecuzione della pipeline*.


