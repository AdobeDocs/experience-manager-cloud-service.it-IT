---
title: Mappatura percorsi per Edge Delivery Services
description: Scopri come mappare i percorsi di pagina utilizzati nell’istanza di authoring AEM sui percorsi di pagina pubblici utilizzati sul sito web e come controllare quali contenuti vengono pubblicati in Edge Delivery Services.
feature: Edge Delivery Services
role: User
exl-id: 3d68135d-e84c-4bf4-93d1-38a0be70ce4a
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 100%

---

# Mappatura percorsi per Edge Delivery Services {#path-mapping}

Scopri come mappare i percorsi di pagina utilizzati nell’istanza di authoring AEM sui percorsi di pagina pubblici utilizzati sul sito web e come controllare quali contenuti vengono pubblicati in Edge Delivery Services.

## Panoramica {#overview}

Per poter creare contenuti WYSIWYG utilizzando AEM e pubblicarli in Edge Delivery Services, è necessario impostare la mappatura del percorso del progetto. Questa mappatura ha due scopi.

* Mappa e crea una relazione tra i percorsi di pagina utilizzati nell’istanza di authoring AEM e i percorsi di pagina pubblici utilizzati sul sito web.
* Controlla quali contenuti (pagine, fogli, risorse, ecc.) vengono pubblicati in Edge Delivery Services.

La mappatura del percorso deve essere configurata per ogni progetto singolarmente e in base al contenuto e alla struttura dell’URL del progetto. Viene utilizzata da AEM durante la pubblicazione e durante la modifica dei contenuti nell’[editor universale](/help/sites-cloud/authoring/universal-editor/navigation.md).

## Formato di configurazione {#configuration-format}

Il formato di configurazione della mappatura del percorso contiene due sezioni (`mappings` e `includes`) simili all’esempio seguente.

```json
{
  "mappings": [
    "/content/aem-boilerplate/:/",
    "/content/aem-boilerplate/configuration:/.helix/config.json"
  ],
  "includes:" [
    "/content/aem-boilerplate/"
  ]
}
```

### mappature {#mappings}

La configurazione `mappings` contiene un array di percorsi interni (nell’istanza di authoring AEM) e percorsi URL esterni (nel sito web pubblico).

Il formato è `<internal paths>:<external path>`. In genere è costituito da un minimo di due voci.

1. La prima voce dell’esempio è la mappatura del percorso delle pagine del sito web.
1. La seconda voce controlla la mappatura di `.helix/config.json` alla pagina del foglio di calcolo corrispondente nell’archivio di authoring AEM.

In questo esempio, tutte le pagine archiviate in `/content/aem-boilerplate/...` saranno accessibili pubblicamente sul sito Edge Delivery Services direttamente in `https://main--my-site--org.aem.live/....`.

>[!TIP]
>
>Tutti i dati tabulari gestiti come fogli di calcolo (ad esempio metadati, reindirizzamenti e tassonomia) vengono in genere pubblicati come URL API `.json` su Edge Delivery Services. A questo scopo, devono essere elencati singolarmente nella configurazione di mappatura.
>
>Per ulteriori informazioni, vedere il documento [Utilizzo di fogli di calcolo per gestire i dati tabulari](/help/edge/wysiwyg-authoring/tabular-data.md).

### include {#includes}

La configurazione `includes` controlla quali percorsi di contenuto vengono effettivamente replicati in Edge Delivery Services. Può contenere anche qualsiasi array di percorsi e in genere contiene la pagina principale di livello superiore dei siti.

Le risorse utilizzate nelle pagine di Edge Delivery Services vengono in genere pubblicate insieme alla pagina web. Vengono esportate automaticamente dall’istanza di authoring AEM a Edge Delivery Services.

>[!TIP]
>
>Se nel tuo caso d’uso desideri che le risorse vengano pubblicate direttamente in Edge Delivery Services, ad esempio perché le immagini o i PDF possano essere accessibili direttamente dagli URL al di fuori del contesto di una pagina, è necessario aggiungere anche i percorsi DAM alla sezione `includes` della configurazione.
>
>Se, ad esempio, una cartella principale di risorse come `/content/dam/my-site/documents` contenente un set di PDF deve essere accessibile al pubblico tramite `/assets/...`, è necessario aggiungere una voce alla sezione `includes` della configurazione.

## Come configurare {#how-to-configure}

Le mappature dei percorsi possono essere configurate in uno dei due modi seguenti, a seconda della configurazione del progetto.

1. Se il progetto è configurato per `aem.live` e utilizza il [servizio di configurazione](https://www.aem.live/docs/config-service-setup) centralizzato, la mappatura dei percorsi per ogni sito viene configurato tramite questo servizio.

   * Di seguito è riportato un esempio di richiesta cURL per configurare le mappature dei percorsi.

   ```text
   curl --request POST \
     --url https://admin.aem.page/config/{org}/sites/{site}/public.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: ......' \
     --data '{
       "paths": {
       "mappings": [
         "/content/aem-boilerplate/:/",
         "/content/aem-boilerplate/configuration:/.helix/config.json"
       ],
       "includes": [
         "/content/aem-boilerplate/"
       ]
   }
   }'
   ```

1. Se il progetto non utilizza il servizio di configurazione, il mapping dei percorsi viene configurato tramite un file `paths.json` nell’archivio GitHub dei progetti.

   * Vedi [`https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/paths.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/paths.json) per un esempio.

In entrambi i casi, una volta configurate le mappature dei percorsi, è possibile controllare la configurazione tramite l’URL di configurazione `https://<branch>--<site>--<org>.aem.page/config.json` accessibile al pubblico.
