---
title: Modifiche di rilievo apportate al componente aggiuntivo Commerce integration framework (CIF)
description: Modifiche di rilievo della Commerce integration framework (CIF) rispetto alle versioni precedenti dell’CIF.
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
feature: Commerce Integration Framework
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# Modifiche di rilievo apportate al componente aggiuntivo Commerce integration framework (CIF){#notable-changes}

Adobe Experience Manager as a Cloud Service offre molte nuove funzioni e possibilità per gestire i progetti AEM. Per ulteriori informazioni su queste funzionalità, segui il collegamento [modifiche all&#39;Experience Manager as a Cloud Service](/help/release-notes/aem-cloud-changes.md).

Questo documento evidenzia le importanti differenze tra il componente aggiuntivo Commerce integration framework (CIF) e le versioni precedenti dell’CIF, note come CIF Classic (Quickstart) e CIF Open-source.

## Installazione e aggiornamenti

Il componente aggiuntivo AEM CIF viene installato tramite Cloud Manager. L’installazione richiede un credito CIF, ad eccezione delle sandbox in cui l’CIF può essere installato senza crediti. I crediti vengono ricevuti automaticamente tramite la fornitura del componente aggiuntivo CIF nel contratto AEM.

Il componente aggiuntivo viene aggiornato automaticamente come parte del normale aggiornamento as a Cloud Service dell’AEM.

**Versioni precedenti dell’CIF**

* CIF Classic: nessuna installazione necessaria, CIF faceva parte di Quickstart. Gli aggiornamenti CIF facevano parte degli aggiornamenti regolari dell’AEM o dei service pack
* CIF open-source per AEM on-premise: installazione tramite GitHub. Gli aggiornamenti facevano parte del lavoro di aggiornamento/manutenzione manuale.
* CIF Open-source per AEM Adobe Managed Services: installazione tramite il Adobe Account Team. Gli aggiornamenti facevano parte del lavoro di aggiornamento/manutenzione manuale.

## Configurazione endpoint

L’endpoint viene configurato e aggiornato tramite l’interfaccia utente di Cloud Manager o la relativa CLI.

**Versioni precedenti dell’CIF**

* CIF Classic: tramite configurazione OSGi nell’AEM
* CIF open-source: tramite il browser configurazioni CIF

## Implementazione del progetto CIF Venia

Progetto disponibile in [Archivio Git di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/integrating-with-git.html) e l’implementazione avviene tramite [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html)

**Versioni precedenti dell’CIF**

* CIF Classic: tramite l’installazione del pacchetto AEM
* CIF open-source: via [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=it)

## Dati catalogo prodotti

I dati del catalogo dei prodotti vengono richiesti on-demand tramite chiamate in tempo reale a un endpoint esterno che supporta le API GraphQL richieste. Queste API supportano l’accesso a dati live o in staging in qualsiasi data. Nessuna replica necessaria.

**Versioni precedenti dell’CIF**

* CIF Classic: i dati di prodotto live e in staging vengono importati e mantenuti in JCR su AEM Author tramite l’importazione di prodotti completa o delta. I dati dei prodotti live vengono replicati nel Publish AEM.

## Esperienze nel catalogo dei prodotti con rendering AEM

L’AEM esegue il rendering istantaneo delle esperienze del catalogo dei prodotti utilizzando i modelli di catalogo AEM assegnati a prodotti e categorie. Nessuna replica necessaria.

**Versioni precedenti dell’CIF**

* CIF Classic: l’autore AEM crea una pagina AEM per ogni categoria/prodotto utilizzando lo strumento blueprint del catalogo. Queste pagine vengono replicate in AEM Publish.

>[!NOTE]
>
>Per ulteriore documentazione su come utilizzare l’CIF con il Managed Service dell’AEM o con l’AEM on-premise, consulta [Commerce integration framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
