---
title: Modifiche di rilievo del componente aggiuntivo Commerce Integration Framework (CIF)
description: Modifiche di rilievo apportate a Commerce Integration Framework (CIF) rispetto alle versioni CIF precedenti.
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 3%

---

# Modifiche di rilievo apportate al componente aggiuntivo Commerce Integration Framework (CIF){#notable-changes}

Adobe Experience Manager as a Cloud Service offre molte nuove funzioni e possibilità per gestire i progetti AEM. Per ulteriori informazioni su queste funzionalità, segui il collegamento [modifiche all&#39;Experience Manager as a Cloud Service](/help/release-notes/aem-cloud-changes.md).

In questo documento vengono evidenziate le differenze importanti tra il componente aggiuntivo Commerce Integration Framework (CIF) e le versioni CIF precedenti, note come CIF Classic (Quickstart) e CIF Open-source.

## Installazione e aggiornamenti

Il componente aggiuntivo AEM CIF viene installato tramite Cloud Manager. L’installazione richiede un credito CIF, ad eccezione delle sandbox in cui CIF può essere installato senza crediti. I crediti vengono ricevuti automaticamente tramite la fornitura del componente aggiuntivo CIF nel contratto AEM.

Il componente aggiuntivo viene aggiornato automaticamente come parte del normale aggiornamento as a Cloud Service dell’AEM.

**Versioni CIF precedenti**

* CIF Classic: non è necessaria alcuna installazione, CIF faceva parte di Quickstart. Gli aggiornamenti CIF facevano parte dei normali aggiornamenti AEM o service pack
* CIF Open-source per AEM on-premise: installazione tramite GitHub. Gli aggiornamenti facevano parte del lavoro di aggiornamento/manutenzione manuale.
* CIF Open-source per AEM Adobe Managed Services: installazione tramite il team dell’account Adobe. Gli aggiornamenti facevano parte del lavoro di aggiornamento/manutenzione manuale.

## Configurazione endpoint

L’endpoint viene configurato e aggiornato tramite l’interfaccia utente di Cloud Manager o la relativa CLI.

**Versioni CIF precedenti**

* CIF Classic: tramite configurazione OSGi in AEM
* CIF Open-source: tramite browser di configurazione CIF

## Implementazione del progetto CIF Venia

Progetto disponibile in [Archivio Git di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/integrating-with-git.html) e l’implementazione avviene tramite [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html?lang=it)

**Versioni CIF precedenti**

* CIF Classic: tramite l’installazione del pacchetto AEM
* CIF Open-source: Via [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=it)

## Dati catalogo prodotti

I dati del catalogo dei prodotti vengono richiesti on-demand tramite chiamate in tempo reale a un endpoint esterno che supporta le API GraphQL richieste. Queste API supportano l’accesso a dati live o in staging in qualsiasi data. Nessuna replica necessaria.

**Versioni CIF precedenti**

* CIF Classic: i dati di prodotto live e in staging vengono importati e mantenuti in JCR su AEM Author tramite l’importazione di prodotti completa o delta. I dati dei prodotti live vengono replicati in AEM Publish.

## Esperienze nel catalogo dei prodotti con rendering AEM

L’AEM esegue il rendering istantaneo delle esperienze del catalogo dei prodotti utilizzando i modelli di catalogo AEM assegnati a prodotti e categorie. Nessuna replica necessaria.

**Versioni CIF precedenti**

* CIF Classic: AEM Author crea una pagina AEM per ogni categoria/prodotto utilizzando lo strumento blueprint del catalogo. Queste pagine vengono replicate in AEM Publish.

>[!NOTE]
>
>Per ulteriore documentazione su come utilizzare CIF con AEM Managed Service o AEM On-Premise, consulta [Framework di integrazione Commerce](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
