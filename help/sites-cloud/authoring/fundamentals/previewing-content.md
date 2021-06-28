---
title: Anteprima del contenuto
description: Scopri come utilizzare il servizio di anteprima AEM per visualizzare in anteprima il contenuto prima di iniziare la pubblicazione.
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: f5e37a4ac8b179ac869609edc87f52858607ad36
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# Anteprima del contenuto {#previewing-content}

>[!NOTE]
>
>La funzione Anteprima fa parte della versione 2021.5.0 e verrà implementata gradualmente nelle prossime settimane.

AEM offre un servizio di anteprima dei siti progettato per consentire agli sviluppatori e agli autori di contenuti di visualizzare in anteprima l’esperienza finale di un sito web prima che raggiunga l’ambiente di pubblicazione ed sia disponibile al pubblico.

Consente di visualizzare in anteprima le esperienze di pagina che non sarebbero altrimenti visibili dall’ambiente di authoring, come le transizioni di pagina e altri contenuti solo lato pubblicazione.

## Pubblicazione del contenuto nell’anteprima {#publishing-content-to-preview}

Puoi pubblicare il contenuto nel servizio di anteprima utilizzando l’interfaccia utente della pubblicazione gestita come segue:

1. Seleziona le pagine da inviare per l’anteprima nella console Sites e fai clic sul pulsante **Gestisci pubblicazione**
1. Nella procedura guidata seguente, seleziona **Anteprima** come destinazione

   ![pubblicazione gestita](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. Fai clic su **Avanti**, quindi su **Pubblica** per confermare.

Per visualizzare il contenuto dell&#39;anteprima, aggiungi **preview** all&#39;URL di pubblicazione dell&#39;istanza di produzione. L’URL deve essere costruito come segue:

```
https://preview-p[programID]-e[environmentID].adobeaemcloud.com/pathtopage.html
```

Per ulteriori informazioni su come ottenere gli URL per i tuoi ambienti, consulta [Gestisci gli ambienti](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/manage-your-environment.html?lang=en) .

Il contenuto può anche essere pubblicato in anteprima utilizzando un [Flusso di lavoro della struttura del contenuto di pubblicazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/replication.html?lang=en#publish-content-tree-workflow) con il parametro agentId impostato per l&#39;anteprima o utilizzando l&#39; [API di replica](/help/operations/replication.md#replication-api) con un AgentFilter configurato per l&#39;anteprima.

## Configurazione delle impostazioni OSGi per il livello di anteprima {#configuring-osgi-settings-for-the-preview-tier}

I valori delle proprietà OSGI del livello di anteprima sono ereditati dal livello di pubblicazione, ma i valori del livello di anteprima possono essere distinti dal livello di pubblicazione utilizzando valori specifici per l’ambiente, impostando il parametro del servizio con il valore &quot;preview&quot;. Prendi l’esempio seguente di una proprietà OSGI che determina l’URL di un endpoint di integrazione:

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

* In [Console per sviluppatori](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools), seleziona **— All Preview —** o un ambiente di produzione che include **prev** nel nome
* Genera le informazioni rilevanti per l’istanza di anteprima
Per ulteriori informazioni su come ottenere gli URL per i tuoi ambienti, consulta [Gestisci gli ambienti](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/manage-your-environment.html?lang=en) .
