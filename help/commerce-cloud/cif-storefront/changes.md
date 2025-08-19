---
title: Modifiche di rilievo del componente aggiuntivo Commerce integration framework (CIF)
description: Modifiche di rilievo apportate a Commerce integration framework (CIF) rispetto alle versioni precedenti di CIF.
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
feature: Commerce Integration Framework
role: Admin
source-git-commit: 856442039fcd25ec675a6258d182f7a35f590c3c
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---


# Modifiche di rilievo apportate al componente aggiuntivo Commerce integration framework (CIF) {#notable-changes}

Adobe Experience Manager as a Cloud Service offre molte nuove funzioni e possibilità per gestire i progetti AEM. Per ulteriori informazioni su queste funzionalità, segui il collegamento per [modifiche a Experience Manager as a Cloud Service.](/help/release-notes/aem-cloud-changes.md)

Questo documento evidenzia le differenze importanti tra il componente aggiuntivo Commerce integration framework (CIF) e le versioni precedenti di CIF, note come CIF Classic (Quickstart) e CIF Open-source.

## Installazione e aggiornamenti

Il componente aggiuntivo AEM CIF viene installato tramite Cloud Manager. L’installazione richiede un credito CIF, ad eccezione delle sandbox in cui CIF può essere installato senza crediti. I crediti vengono ricevuti automaticamente tramite il provisioning del componente aggiuntivo CIF nel contratto AEM.

Il componente aggiuntivo viene aggiornato automaticamente come parte del normale aggiornamento di AEM as a Cloud Service.

### Versioni precedenti di CIF {#previous-versions-installation}

* CIF Classic: non è necessaria alcuna installazione, CIF faceva parte di Quickstart. Gli aggiornamenti di CIF facevano parte dei normali aggiornamenti di AEM o service pack
* CIF Open-source per AEM on-premise: installazione tramite GitHub. Gli aggiornamenti facevano parte del lavoro di aggiornamento/manutenzione manuale.
* CIF Open-source per AEM Adobe Managed Services: installazione tramite il team dell’account Adobe. Gli aggiornamenti facevano parte del lavoro di aggiornamento/manutenzione manuale.

## Configurazione endpoint {#endpoint-configuration}

L’endpoint viene configurato e aggiornato tramite l’interfaccia utente di Cloud Manager o la relativa CLI.

### Versioni precedenti di CIF {#previous-versions-endpoint}

* CIF Classic: tramite la configurazione OSGi in AEM
* CIF Open-source: tramite browser configurazioni CIF

## Implementazione del progetto CIF Venia {#venia-project}

Progetto disponibile in [Archivio Git Cloud Manager](/help/implementing/cloud-manager/managing-code/integrating-with-git.md) e distribuzione eseguita tramite [Cloud Manager.](/help/implementing/deploying/overview.md)

### Versioni precedenti di CIF {#previous-versions-venia}

* CIF Classic: tramite l’installazione del pacchetto di AEM
* CIF Open-source: Tramite [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=it)

## Dati catalogo prodotti {#product-catalog-data}

I dati del catalogo dei prodotti vengono richiesti on-demand tramite chiamate in tempo reale a un endpoint esterno che supporta le API GraphQL richieste. Queste API supportano l’accesso a dati live o in staging in qualsiasi data. Nessuna replica necessaria.

### Versioni precedenti di CIF {#previous-versions-catalog}

* CIF Classic: i dati di prodotto live e in staging vengono importati e mantenuti in JCR su AEM Author tramite l’importazione di prodotti completa o delta. I dati dei prodotti live vengono replicati in AEM Publish.

## Esperienze nel catalogo dei prodotti con AEM Rendering {#catalog-experiences}

AEM esegue il rendering istantaneo delle esperienze del catalogo dei prodotti utilizzando i modelli di catalogo AEM assegnati a prodotti e categorie. Nessuna replica necessaria.

### Versioni precedenti di CIF {#previous-cif-versions}

* CIF Classic: AEM Author crea una pagina AEM per ogni categoria/prodotto utilizzando lo strumento blueprint del catalogo. Queste pagine vengono replicate in AEM Publish.

>[!NOTE]
>
>Per ulteriore documentazione su come utilizzare CIF con AEM Managed Service o AEM On-Premise, vedi [Commerce integration framework.](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
