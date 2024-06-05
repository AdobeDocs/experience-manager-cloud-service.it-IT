---
title: Panoramica di Content Transformer
description: Scopri come rilevare e risolvere i problemi relativi al contenuto segnalati da BPA utilizzando Content Transformer.
exl-id: aa3397ff-3dd6-4c67-9064-cb9b19bf1c73
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 3%

---

# Panoramica {#overview-ct}

Il Content Transformer (CT) è uno strumento sviluppato da Adobe che può essere utilizzato per rilevare e correggere automaticamente i problemi relativi al contenuto segnalati da [Best Practices Analyzer (BPA)](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) prima della migrazione dei contenuti dall’implementazione AEM corrente (on-premise o Managed Services) all’AEM as a Cloud Service.

Il Content Transformer può aiutare a risolvere i problemi che rientrano nelle seguenti categorie [Categorie di pattern BPA](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html?lang=it) (mostrato nella tabella seguente) consentendo agli utenti di eseguire azioni in blocco, ad esempio spostare o eliminare. Questo consente di ridurre notevolmente i tempi e la complessità associata a un progetto di migrazione.

## Categorie di modelli coperte da Content Transformer e soluzioni suggerite {#pattern-categories-and-benefits}

| Codice pattern | Tipo/sottotipo sospetto | Potenziale correzione prima della migrazione del contenuto a AEM as a Cloud Service |
|--------------|--------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| ACV | missing.jcrcontent <br> missing.original.rendition <br> metadata.descendants.viola | Sposta queste risorse in una posizione diversa o eliminale per assicurarti che non vengano migrate all’as a Cloud Service AEM. |
| CAV | content.area.violation | Sposta temporaneamente i percorsi in `/etc/packages/content-transformation/paths` per garantire che non vengano trasferiti a AEM as a Cloud Service. |
| DOPI | deprecated.ordered.index | Rimuovi gli indici obsoleti. |
| OAUI | non.migrated.oauth.users | Rimuovi questi utenti per assicurarti che non vengano trasferiti ad AEM as a Cloud Service. |
| PCX | page.complex.medium <br> page.complex.high | Elimina le pagine o gli elementi figlio o spostali in un percorso diverso per assicurarti che non vengano migrati all’AEM as a Cloud Service. |
| REP | forward.replication <br> reverse.replication <br> standard.replication.agent.modification <br> custom.replication.agent.detection | Rimuovi gli agenti di replica creati. <br> OPPURE <br> Rimuovi le proprietà modificate/aggiunte. |
| URS | clientlibs.location <br> file.location <br> node.location <br> workflow.location | Passa alla posizione corretta per evitare problemi durante la migrazione. |
| URS | node.size | Spostare temporaneamente i nodi in`/etc/packages/content-transformation/paths` per garantire che non vengano trasferiti a AEM as a Cloud Service. |

## Vantaggi offerti da Content Transformer {#benefits}

Content Transformer offre i seguenti vantaggi:

* Fail-safe: un pacchetto viene creato da Content Transformer ogni volta che apporta modifiche all’archivio per risolvere i problemi. Se necessario, puoi ripristinare lo stato precedente installando il pacchetto.
* Facile da usare: Content Transformer è stato integrato con lo strumento Content Transfer ed è dotato di una semplice interfaccia utente intuitiva.
* Risparmio di tempo: quando si dispone di un numero elevato di problemi di contenuto che rientrano in una categoria di pattern, è possibile risolverli tutti con diversi clic utilizzando Content Transformer.
