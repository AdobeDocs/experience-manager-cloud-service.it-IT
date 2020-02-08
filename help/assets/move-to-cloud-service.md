---
title: Migrazione al servizio cloud da Adobe Experience Manager 6.x
description: Migrazione al servizio cloud da Adobe Experience Manager 6.x
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Passa a Risorse Adobe Experience Manager come servizio cloud {#move-to-assets-cloud-service}

<!-- About the need to move from previous AEM deployment to a cloud service deployment. And how does Adobe help do it OOTB?
-->

## Lo strumento di migrazione {#migration-tool}

<!-- 
Link back to information about the tool in the Experience Manager as a Cloud Service docs if the tool works the same for Sites and Assets. Document the Assets-specific information here.

* What is the migration tool called? Is there a branding term for it?
* How much do we want to elaborate about the Pattern Detector rules? Is there a branding term for it?
* Before migrating using the tool, is any prepping required?
* See CQ-4271901

-->

Lo strumento di migrazione consente di ottenere quanto segue:

* Convertite i modelli di flusso di lavoro esistenti in profili di elaborazione compatibili con il servizio di elaborazione risorse.
* Rimuovete i passaggi non supportati dai modelli di workflow.
* Disattiva gli avviatori del flusso di lavoro.
* Unisci le configurazioni, dopo la conferma/convalida dell&#39;utente, nel codice sorgente esistente.

Lo strumento di migrazione crea profili di elaborazione in un modulo Paradiso che gli utenti possono utilizzare nei due modi seguenti:

* Unisci in uno dei loro progetti esistenti.
* Aggiungete il modulo come nuovo sottomodulo.

Lo strumento di migrazione fornisce un rapporto sulle modifiche apportate e informazioni sulle modifiche.

<!--  

What is the output of the tool, besides migrated content.

Give details about reports and logs of the tool. 

* How to access the report, including required permissions.
* How to read/interpret the report.
* Location of logs. How to read the logs.
* What common errors to look for. Troubleshooting for these errors.

-->

## Migrazione del contenuto a una nuova distribuzione {#content-migration-across-deployments}
