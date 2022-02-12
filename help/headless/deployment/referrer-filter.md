---
title: Configurazione del filtro referente con AEM Headless
description: Il filtro referente di Adobe Experience Manager consente l’accesso da host di terze parti. È necessaria una configurazione OSGi per il filtro referente per abilitare l’accesso all’endpoint GraphQL per le applicazioni headless.
feature: GraphQL API
source-git-commit: 0cc131209f497241949f8da6e8144dfcaffe7e6e
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---


# Filtro di riferimento {#referrer-filter}

Il filtro referente di Adobe Experience Manager consente l’accesso da host di terze parti. È necessaria una configurazione OSGi per il filtro referente per abilitare l’accesso all’endpoint GraphQL per le applicazioni headless.

A questo scopo, aggiungi una configurazione OSGi appropriata per il filtro referente che:

* specifica un nome host del sito web fidato; o `allow.hosts` o `allow.hosts.regexp`,
* concede l&#39;accesso per questo nome host.

Il nome del file deve essere `org.apache.sling.security.impl.ReferrerFilter.cfg.json`.

Ad esempio, per concedere l’accesso alle richieste con il referente `my.domain` puoi:

```xml
{
    "allow.empty":false,
    "allow.hosts":[
      "my.domain"
    ],
    "allow.hosts.regexp":[
      ""
    ],
    "filter.methods":[
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp":[
      ""
    ]
}
```

>[!CAUTION]
>
>Spetta al cliente:
>
>* concedere solo l&#39;accesso ai domini trusted
>* assicurati che non siano esposte informazioni sensibili
>* non utilizzare un carattere jolly [*] sintassi; entrambi disattiveranno l’accesso autenticato all’endpoint GraphQL e lo esporranno a tutto il mondo.


>[!CAUTION]
>
>Tutti i GraphQL [schemi](#schema-generation) (derivato dai modelli di frammenti di contenuto che sono stati **Abilitato**) sono leggibili attraverso l’endpoint GraphQL .
>
>Ciò significa che devi assicurarti che non siano disponibili dati sensibili, in quanto potrebbero essere trapelati in questo modo; ad esempio, include informazioni che potrebbero essere presenti come nomi di campo nella definizione del modello.
