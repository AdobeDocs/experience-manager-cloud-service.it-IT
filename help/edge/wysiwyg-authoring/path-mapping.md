---
title: Mappatura percorsi per Edge Delivery Services
description: Scopri come mappare i percorsi di pagina utilizzati nell’istanza di authoring AEM sui percorsi di pagina pubblici utilizzati sul sito web e controllare quali contenuti vengono pubblicati nei Edge Delivery Services.
feature: Edge Delivery Services
role: User
source-git-commit: 51a2b453ccce39cb42c927a088bc088083545542
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---


# Mappatura percorsi per Edge Delivery Services {#path-mapping}

Scopri come mappare i percorsi di pagina utilizzati nell’istanza di authoring AEM sui percorsi di pagina pubblici utilizzati sul sito web e controllare quali contenuti vengono pubblicati nei Edge Delivery Services.

## Panoramica {#overview}

Per poter creare contenuti WYSIWYG utilizzando l’AEM e pubblicarli in Edge Delivery Services, devi impostare la mappatura del percorso del progetto. Questa mappatura ha due scopi.

* Mappa e crea una relazione tra i percorsi di pagina utilizzati nell’istanza di authoring AEM e i percorsi di pagina pubblici utilizzati sul sito web.
* Controlla il contenuto (pagine, fogli, risorse, ecc.) vengono pubblicati in Edge Delivery Services.

La mappatura del percorso deve essere configurata per ogni progetto singolarmente e in base al contenuto e alla struttura URL del progetto. Viene utilizzato dall&#39;AEM durante la pubblicazione dei contenuti e durante la modifica dei contenuti nell&#39;[Editor universale.](/help/sites-cloud/authoring/universal-editor/navigation.md)

## Formato di configurazione {#configuration-format}

Il formato della configurazione di mappatura percorso contiene due sezioni (`mappings` e `includes`) simili all&#39;esempio seguente.

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

La configurazione `mappings` contiene un array di percorsi interni (nell&#39;istanza di authoring AEM) e percorsi URL esterni (nel sito Web pubblico).

Il formato è `<internal paths>:<external path>`. In genere è costituito da un minimo di due voci.

1. La prima voce dell’esempio è la mappatura del percorso delle pagine del sito web.
1. La seconda voce controlla la mappatura di `.helix/config.json` alla pagina del foglio di calcolo corrispondente nell&#39;archivio di creazione AEM.

In questo esempio, tutte le pagine archiviate in `/content/aem-boilerplate/...` saranno accessibili pubblicamente sul sito dei Edge Delivery Services direttamente in `https://main--my-site--org.aem.live/....`.

>[!TIP]
>
>Tutti i dati tabulari gestiti come fogli di calcolo (ad esempio metadati, reindirizzamenti e tassonomia) vengono in genere pubblicati come `.json` URL API sui Edge Delivery Services. A questo scopo, devono essere elencati singolarmente nella configurazione di mappatura.
>
>Per ulteriori informazioni, vedere il documento [Utilizzo di fogli di calcolo per gestire i dati tabulari](/help/edge/wysiwyg-authoring/tabular-data.md).

### include {#includes}

La configurazione `includes` controlla quali percorsi di contenuto vengono effettivamente replicati nei Edge Delivery Services. Può contenere anche qualsiasi array di percorsi e in genere contiene la pagina principale di livello superiore dei siti.

Assets utilizzato nelle pagine di Edge Delivery Services viene in genere pubblicato insieme alla pagina web. Vengono esportati automaticamente dall’istanza di authoring AEM ai Edge Delivery Services.

>[!TIP]
>
>Se si desidera che le risorse vengano pubblicate direttamente nei Edge Delivery Services in un caso d&#39;uso, ad esempio se si desidera che le immagini o i PDF siano accessibili direttamente dagli URL al di fuori del contesto di una pagina, è necessario aggiungere anche i percorsi DAM alla sezione `includes` della configurazione.
>
>Se, ad esempio, una cartella principale di risorse come `/content/dam/my-site/documents` contenente un set di PDF deve essere accessibile al pubblico tramite `/assets/...`, è necessario aggiungere una voce alla sezione `includes` della configurazione.

## Come configurare {#how-to-configure}

Le mappature dei percorsi possono essere configurate in uno dei due modi seguenti, a seconda della configurazione del progetto.

1. Se il progetto è configurato per `aem.live` e utilizza il [servizio di configurazione](https://www.aem.live/docs/config-service-setup) per le configurazioni centralizzate, il mapping dei percorsi per ogni sito viene configurato tramite questo servizio di configurazione.

   * Di seguito è riportato un esempio di richiesta cURL per configurare le mappature dei percorsi.

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/{org}/sites/{site}/public.json \
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

1. Se il progetto non utilizza il servizio di configurazione, la mappatura dei percorsi viene configurata tramite un file paths.json nell’archivio GitHub dei progetti.

   * Vedi [`https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/paths.json`](/https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/paths.json) per un esempio.

In entrambi i casi, una volta configurate le mappature dei percorsi, è possibile controllare la configurazione tramite l&#39;URL di configurazione accessibile al pubblico `https://<branch>--<site>--<org>.aem.page/config.json`.
