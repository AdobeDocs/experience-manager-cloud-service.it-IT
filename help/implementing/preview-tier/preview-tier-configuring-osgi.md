---
title: Configurazione delle impostazioni OSGi per il livello di anteprima
description: Scopri come utilizzare il servizio di anteprima AEM per visualizzare in anteprima i contenuti prima della pubblicazione.
exl-id: 1200bb17-8a3c-4e41-85f4-ed2334b61f69
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 89%

---

# Configurazione delle impostazioni OSGi per il livello di anteprima {#configure-osgi-preview-tier}

AEM offre un servizio di anteprima Sites che consente agli sviluppatori e agli autori di contenuti di visualizzare in anteprima l’esperienza finale di un sito web prima che raggiunga l’ambiente di pubblicazione e sia disponibile pubblicamente.

Consente di visualizzare in anteprima una serie di esperienze che non sarebbero altrimenti visibili dall’ambiente di authoring. Ad esempio, transizioni di pagina, frammenti di esperienza e altro contenuto solo lato pubblicazione.

I valori delle proprietà OSGi del livello di anteprima vengono ereditati dal livello di pubblicazione. Tuttavia, i valori del livello di anteprima possono essere distinti dal livello di pubblicazione impostando il parametro `service` al valore `preview`.

>[!NOTE]
>
>Per ulteriori dettagli sugli ambienti di anteprima, vedi [Gestisci ambienti](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

## Configurazione delle impostazioni OSGi per il livello di anteprima {#configuring-osgi-settings-for-the-preview-tier}

L’esempio seguente di una proprietà OSGi determina l’URL di un endpoint di integrazione.

```
[
{
"name":"INTEGRATION_URL",
"type":"string",
"value":"http://s2.integrationvendor.com",
"service": "preview"
}
]
```

Per ulteriori informazioni, consulta [questa sezione](/help/implementing/deploying/configuring-osgi.md#author-vs-publish-configuration) della documentazione di configurazione OSGi.

## Eseguire il debug dell’anteprima tramite la Console per sviluppatori {#debugging-preview-using-the-developer-console}

Segui questi passaggi per eseguire il debug del livello di anteprima utilizzando la Console per sviluppatori:

* Nella [Console per sviluppatori](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools), seleziona **-- Tutte le anteprime --** oppure un ambiente di produzione che includa **prev** nel nome
* Genera le informazioni rilevanti per l’istanza di anteprima 
Per ulteriori informazioni su come ottenere gli URL per i tuoi ambienti, consulta [Gestione degli ambienti](/help/implementing/cloud-manager/manage-environments.md).
