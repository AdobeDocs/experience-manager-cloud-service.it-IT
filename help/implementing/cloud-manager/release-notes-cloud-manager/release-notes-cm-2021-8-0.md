---
title: Note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2021.8.0
description: Note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2021.8.0
feature: Release Information
exl-id: cf1d5c4f-404a-4ced-90f2-273c710adc0f
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 4%

---

# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2021.8.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.8.0.

>[!NOTE]
>Per visualizzare le note sulla versione corrente per Adobe Experience Manager as a Cloud Service, fai clic su [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=it).

## Data di pubblicazione {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.8.0 è il 12 agosto 2021.

### Novità {#what-is-new}

* I clienti del Cloud Service ora possono visualizzare i rapporti SLA (Service Level Agreement) in Cloud Manager. Ciò sarà progressivamente reso disponibile nei prossimi mesi.
Vedi [Generazione rapporti SLA](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html) per saperne di più.

* Tipo e gravità dell&#39;IndexType e `IndexDamAssetLucene` le regole di qualità sono state modificate. Questi sono ora entrambi Bugs of Blocker *serenità*.

* Sono state introdotte nuove regole sulla qualità dell&#39;indice Oak per coprire configurazioni asincrone e tika.

* Aumenta il numero massimo di certificati SSL per programma a 50.

* Funzionalità self-service per consentire agli utenti di creare e gestire più archivi tramite l’interfaccia utente di Cloud Manager.

* SonarQube leggeva inutilmente i dati della cronologia Git. Su basi di codice di grandi dimensioni, ciò potrebbe comportare una multa non necessaria per le prestazioni della build.

* È ora disponibile un’API per annullare la validità della cache di dipendenza Maven per pipeline.

* La versione di AEM Project Archetype utilizzata da Cloud Manager è stata aggiornata alla versione 29.

### Correzioni di bug {#bug-fixes}

* Lo stato Aggiorna disponibile non deve essere visualizzato quando l&#39;ultima versione è inferiore alla versione corrente.

* L&#39;onboarding iniziale non riusciva per le nuove organizzazioni con nomi molto lunghi.

* Talvolta, quando una pipeline viene attivata due volte per qualche motivo, si verifica un errore in una delle esecuzioni con *impossibile aggiornare lo stato di esecuzione della pipeline* errore.
