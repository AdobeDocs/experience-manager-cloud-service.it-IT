---
title: Configurazione del filtro Referrer con AEM Headless
description: Il filtro Referrer di Adobe Experience Manager consente l’accesso da host di terze parti. Per abilitare l’accesso all’endpoint GraphQL per le applicazioni headless è necessaria una configurazione OSGi per il filtro Referrer.
feature: Headless, GraphQL API
exl-id: e2e3d2dc-b839-4811-b5d1-38ed8ec2cc87
solution: Experience Manager
role: Admin, Developer
source-git-commit: 3096436f8057833419249d51cb6c15e6c28e9e13
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 55%

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

## Esempio di configurazione {#example-configuration}

Ad esempio, per concedere l’accesso alle richieste con il Referrer `my.domain` puoi:

>[!CAUTION]
>
>Questo è un esempio di base che potrebbe sovrascrivere la configurazione standard. È necessario assicurarsi che gli aggiornamenti dei prodotti vengano sempre applicati a qualsiasi personalizzazione.

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

## Sicurezza dei dati {#data-security}

>[!CAUTION]
>
>È tua responsabilità affrontare pienamente i seguenti punti.

Per garantire la protezione dei dati, è necessario assicurarsi che:

* l&#39;accesso è **only** concesso ai domini attendibili

* viene utilizzata la sintassi del carattere jolly [`*`] in **not**; questa funzione disattiva l&#39;accesso autenticato all&#39;endpoint GraphQL e la espone a tutto il mondo

* le informazioni riservate sono **mai** esposte; né direttamente né indirettamente:

   * Ad esempio, tutti gli [schemi di GraphQL](/help/headless/graphql-api/content-fragments.md#schema-generation) sono:

      * derivato da modelli per frammenti di contenuto che sono stati **abilitati**

     **e**

      * sono leggibili tramite l’endpoint GraphQL

     Ciò significa che le informazioni presenti come nomi di campo nella definizione del modello possono diventare disponibili.

Devi accertarti che non siano disponibili dati sensibili in alcun modo, quindi tali dettagli devono essere attentamente considerati.
