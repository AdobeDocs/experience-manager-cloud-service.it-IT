---
title: Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2021.10.0
description: Note sulla versione per Cloud Manager in AEM versione as a Cloud Service 2021.10.0
feature: Release Information
exl-id: null
source-git-commit: c7cee58a465887b15994a963448fcba8d546673a
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 6%

---


# Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2021.10.0 {#release-notes}

Questa pagina illustra le note sulla versione per gli strumenti di migrazione in AEM as a Cloud Service 2021.10.0.

>[!NOTE]
>Per visualizzare le note sulla versione corrente per Adobe Experience Manager as a Cloud Service, fai clic su [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=it).

## Strumento Content Transfer (Trasferimento contenuti)  {#ctt-release}

### Data di pubblicazione {#release-date-ctt-latest}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.6.0 è il 4 ottobre 2021.

### Novità {#what-is-new-ctt-oct}

* Strumento di mappatura utenti migliorato con un’esperienza utente semplificata, incluse le seguenti funzioni elencate di seguito. Per ulteriori informazioni, consulta [Utilizzo dello strumento di mappatura utente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html).
   * Verificare la connessione all&#39;API User Management prima di eseguire User Mapping
   * Salta con attenzione gli errori e continua con l’attività Mappatura utente
   * La mappatura utente non ha più esito negativo se **Token di accesso** scade dopo 24 ore. La mappatura utente può essere rieseguita dal punto in cui è stata arrestata per ultima.

* Per aumentare la robustezza dello strumento Content Transfer (Trasferimento contenuti), il contenuto può essere acquisito sia nell’istanza Author che nell’istanza Publish alla volta. Vedi [Guida introduttiva allo strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) per ulteriori dettagli.

* Quando sono incluse le versioni, il percorso `/var/audit` è incluso automaticamente per la migrazione degli eventi di controllo.


## Cloud Acceleration Manager {#cam-release}

### Data di pubblicazione {#release-date-cam}

La data di rilascio di Cloud Acceleration Manager è il 25 ottobre 2021.

### Novità {#what-is-new-cam}

Cloud Acceleration Manager offre ora agli utenti la possibilità di visualizzare i rapporti BPA storici in un rapporto Trendline. Con questo rapporto, gli utenti possono visualizzare i progressi che stanno facendo in una rappresentazione grafica di facile utilizzo. Fai riferimento a [Utilizzo della linea di tendenza della vista](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#trendline-view-cam) per ulteriori dettagli.

### Data di pubblicazione {#release-date-october-cam}

La data di rilascio di Cloud Acceleration Manager è il 4 ottobre 2021.

### Novità {#what-is-new-cam-oct}

Cloud Acceleration Manager offre agli utenti la possibilità di visualizzare i rapporti BPA in un&#39;anteprima stampabile, consentendo di stampare o stampare facilmente i rapporti in PDF per facilitarne la condivisione. Fai riferimento ai passaggi 6 e 7 in [Utilizzo della scheda di analisi delle best practice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis).

## Analisi delle best practice {#best-practices-analyzer}

### Data di pubblicazione {#release-date-bpa-latest}

La data di rilascio di Best Practices Analyzer v2.1.20 è il 5 ottobre 2021.

### Novità {#what-is-new-bpa-oct}

* Possibilità di rilevare e segnalare la lunghezza del nome del nodo.

* Capacità di rilevare e segnalare la dimensione totale dell&#39;indice.

* Possibilità di rilevare e segnalare le risorse per le quali manca il rendering originale.