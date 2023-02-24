---
title: Configurazione del filtro Referrer con AEM Headless
description: Il filtro Referrer di Adobe Experience Manager consente l’accesso da host di terze parti. Per abilitare l’accesso all’endpoint GraphQL per le applicazioni headless è necessaria una configurazione OSGi per il filtro Referrer.
feature: GraphQL API
exl-id: e2e3d2dc-b839-4811-b5d1-38ed8ec2cc87
source-git-commit: 076cafe3d096fd7f4c808f1b2553a9ba6b6c1833
workflow-type: ht
source-wordcount: '277'
ht-degree: 100%

---

# Filtro referrer {#referrer-filter}

Il filtro Referrer di Adobe Experience Manager consente l’accesso da host di terze parti.

Per abilitare l’accesso all’endpoint GraphQL per le applicazioni headless su HTTP POST è necessaria una configurazione OSGi per il filtro Referrer. Quando si utilizzano query persistenti headless AEM che accedono a AEM tramite HTTP GET, non è necessaria una configurazione del filtro referrer.

>[!WARNING]
> Il filtro referrer di AEM non è un factory di configurazione OSGi, il che significa che è attiva solo una configurazione alla volta su un servizio AEM. Quando possibile, evita di aggiungere configurazioni personalizzate del filtro referrer, in quanto questo sovrascrive le configurazioni native di AEM e potrebbe interrompere la funzionalità del prodotto.

Ciò avviene tramite una configurazione OSGi appropriata per il filtro Referrer che:

* specifica un nome host fidato del sito web; `allow.hosts` oppure `allow.hosts.regexp`,
* concede l’accesso per questo nome host.

Il nome del file deve essere `org.apache.sling.security.impl.ReferrerFilter.cfg.json`.

Ad esempio, per concedere l’accesso alle richieste con il Referrer `my.domain` puoi:

```xml
{
    "allow.empty": false,
    "allow.hosts": [
      "my.domain"
    ],
    "allow.hosts.regexp": [
      ""
    ],
    "filter.methods": [
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp": [
      ""
    ]
}
```

>[!CAUTION]
>
>Spetta al cliente:
>
>* concedere l’accesso solo ai domini attendibili;
>* assicurarsi che non siano esposte informazioni sensibili;
>* non utilizzare una sintassi con carattere jolly [*]; questa infatti comporterebbe la disattivazione dell’accesso autenticato all’endpoint GraphQL, rendendolo accessibile a chiunque.


>[!CAUTION]
>
>Tutti gli [schemi](#schema-generation) GraphQL (derivati dai modelli per frammenti di contenuto che sono stati **abilitati**) sono leggibili attraverso l’endpoint GraphQL.
>
>Ciò significa che devi assicurarti che non siano disponibili dati sensibili, che in questo modo potrebbero trapelare; ad esempio, informazioni che potrebbero essere presenti come nomi di campo nella definizione del modello.
