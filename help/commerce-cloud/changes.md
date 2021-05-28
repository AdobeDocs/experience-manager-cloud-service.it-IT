---
title: Modifiche di rilievo del componente aggiuntivo Commerce Integration Framework (CIF)
description: Modifiche di rilievo di Commerce Integration Framework (CIF) rispetto alle vecchie versioni CIF.
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32,c136763f-56aa-450e-8796-bc84bf6c205d
source-git-commit: ac64ca485391d843c0ebefcf86e80b4015b72b2f
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 5%

---

# Modifiche di rilievo apportate al componente aggiuntivo Commerce Integration Framework (CIF){#notable-changes}

Adobe Experience Manager as a Cloud Service offre nuove funzionalità e possibilità per gestire i progetti AEM. Per ulteriori informazioni su queste funzionalità, segui il collegamento relativo alle [modifiche ad Experience Manager as a Cloud Service](/help/release-notes/aem-cloud-changes.md).

Questo documento evidenzia le importanti differenze tra il componente aggiuntivo Commerce Integration Framework (CIF) e le vecchie versioni CIF, note principalmente come CIF Classic (Quickstart) e CIF Open-source.

## Installazione e aggiornamenti

Il componente aggiuntivo CIF AEM viene installato tramite Cloud Manager. L’installazione richiede un credito CIF, ad eccezione delle sandbox in cui è possibile installare CIF senza crediti. I crediti vengono ricevuti automaticamente tramite il provisioning del componente aggiuntivo CIF nel contratto di AEM.

Il componente aggiuntivo viene aggiornato automaticamente come parte del normale AEM come aggiornamento del Cloud Service.

**Versioni CIF precedenti**

* CIF Classic: Non è necessaria alcuna installazione, CIF faceva parte di Quickstart. Gli aggiornamenti CIF facevano parte degli aggiornamenti AEM o service pack regolari
* CIF Open source per AEM on-premise: Installazione tramite GitHub. Gli aggiornamenti facevano parte del lavoro di aggiornamento/manutenzione manuale.
* CIF Open source per AEM Adobe Managed Services: Installazione tramite Customer Success Manager. Gli aggiornamenti facevano parte del lavoro di aggiornamento/manutenzione manuale.

## Configurazione endpoint

L’endpoint viene configurato e aggiornato tramite l’interfaccia utente di Cloud Manager o la sua CLI.

**Versioni CIF precedenti**

* CIF Classic: Configurazione tramite OSGi in AEM
* CIF Open source: Browser di configurazione CIF

## Implementazione del progetto CIF Venia

Progetto disponibile in [Cloud Manager Git Repository](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) e distribuzione eseguita tramite [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html)

**Versioni CIF precedenti**

* CIF Classic: Tramite installazione del pacchetto AEM
* CIF Open source: Tramite [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=it)

## Dati catalogo prodotti

I dati del catalogo dei prodotti vengono richiesti on-demand tramite chiamate in tempo reale a un endpoint esterno che supporta le API GraphQL richieste. Queste API supportano l’accesso a dati live o in staging in qualsiasi data. Nessuna replica necessaria.

**Versioni CIF precedenti**

* CIF Classic: I dati dei prodotti live e in staging vengono importati e mantenuti in JCR su AEM Author tramite l’importazione completa o delta del prodotto. I dati dei prodotti live vengono replicati in AEM Publish.

## Esperienze del catalogo dei prodotti con rendering AEM

AEM esegue il rendering immediato delle esperienze di catalogo di prodotti utilizzando AEM modelli di catalogo assegnati a prodotti e categorie. Nessuna replica necessaria.

**Versioni CIF precedenti**

* CIF Classic: AEM Author crea una pagina AEM per ogni categoria/prodotto utilizzando lo strumento di blueprint del catalogo. Queste pagine vengono replicate in AEM Publish.

>[!NOTE]
>
>Per ulteriore documentazione su come utilizzare CIF con AEM Managed Service o AEM on-premise, consulta [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
