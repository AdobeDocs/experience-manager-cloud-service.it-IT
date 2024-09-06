---
title: Aggiunta di un record TXT
description: Scopri come aggiungere un record TXT per verificare la proprietà di un dominio personalizzato da utilizzare con Cloud Manager.
exl-id: d441de29-af41-4d3e-9155-531af9702841
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 28%

---


# Aggiunta di un record TXT {#adding-txt}

Scopri come aggiungere un record TXT per verificare la proprietà di un dominio personalizzato da utilizzare con Cloud Manager.

## Cos’è un record TXT? {#what-is}

Un record di testo (noto anche come record TXT) è un tipo di record di risorse nel DNS (Domain Name System). Consente di associare testo arbitrario a un nome host, ad esempio informazioni leggibili dall&#39;utente su un nome host, ad esempio informazioni sul server o sulla rete.

Cloud Manager utilizza un record TXT specifico per autorizzare un dominio ad essere ospitato in un servizio CDN. È necessario creare un record TXT DNS nella zona che autorizza Cloud Manager a distribuire il servizio CDN con il dominio personalizzato e associarlo al servizio back-end. Questa associazione è interamente sotto il tuo controllo e autorizza Cloud Manager a distribuire contenuti dal servizio a un dominio. Tale autorizzazione può essere concessa e revocata. Il record TXT è specifico del dominio e dell’ambiente Cloud Manager.

## Requisiti {#requirements}

Prima di aggiungere un record TXT è necessario soddisfare i requisiti riportati di seguito.

* Se non disponi ancora di questa informazione, identifica l’host o il registrar del dominio.
* È necessario essere in grado di modificare i record DNS per il dominio dell&#39;organizzazione o di contattare la persona appropriata che può farlo.
* È innanzitutto necessario aggiungere un nome di dominio personalizzato come descritto nel documento [Aggiunta di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

## Aggiunta di un record TXT per la verifica {#verification}

Un record TXT viene aggiunto come parte della verifica di un nome di dominio personalizzato da utilizzare con Cloud Manager.

1. È innanzitutto necessario aggiungere un nome di dominio personalizzato come descritto nel documento [Aggiunta di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

1. Nella scheda **Verifica** della finestra di dialogo **Aggiungi nome di dominio**, Cloud Manager visualizza il nome e il valore TXT da utilizzare per la verifica. Copia questo valore.

   ![Verifica del nome di dominio](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

1. Accedi all’host del dominio e individua la sezione relativa ai record DNS.

1. Aggiungi `_aemverification.[yourdomainname]` come **Nome** del valore e aggiungi il valore TXT esattamente come visualizzato nella finestra di dialogo **Aggiungi nome di dominio**.

   * Vedi gli [esempi nella sezione seguente](#examples).

1. Salva il record TXT nell’host del dominio.

## Esempi di record TXT {#examples}

| Dominio | Nome | Valore TXT |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | Copia l’intero valore visualizzato nell’interfaccia utente di Cloud Manager. Il valore è specifico del dominio e dell’ambiente. Esempio:<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
| `www.example.com` | `_aemverification.www.example.com` | Copia l’intero valore visualizzato nell’interfaccia utente di Cloud Manager. Il valore è specifico del dominio e dell’ambiente. Esempio:<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

## Verifica record TXT {#verify}

Al termine dell’operazione, puoi verificare il risultato eseguendo il seguente comando.

```shell
dig _aemverification.[yourdomainname] -t txt
```

Il risultato previsto deve visualizzare il valore TXT fornito nella scheda **Verifica** della finestra di dialogo **Aggiungi nome dominio** dell&#39;interfaccia utente di Cloud Manager.

Se ad esempio il dominio è `example.com`, esegui:

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>Sono disponibili diversi [strumenti di ricerca DNS](https://www.ultratools.com/tools/dnsLookup). Puoi utilizzare Google DoH per cercare voci di record TXT e identificare se un record TXT risulta mancante o errato.

>[!NOTE]
>
>L’elaborazione della verifica DNS può richiedere alcune ore per via dei ritardi di propagazione del DNS.
>
>Cloud Manager verificherà la proprietà del dominio e aggiornerà lo stato riportato nella tabella Impostazioni dominio. Per ulteriori dettagli, consulta [Verifica dello stato del nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

## Passaggi successivi {#next-steps}

Dopo aver creato la voce TXT, puoi verificare lo stato del nome di dominio. Procedi al documento [Verifica dello stato del nome di dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) per continuare la configurazione del nome di dominio personalizzato.

>[!TIP]
>
>È possibile impostare contemporaneamente la voce TXT e il CNAME o un record sul server DNS di riferimento, risparmiando tempo.
>
>Se desideri eseguire questa operazione, controlla innanzitutto l&#39;intero processo di configurazione di un nome di dominio personalizzato come descritto nel documento [Introduzione ai nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/introduction.md), prendendo nota del documento [help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) e aggiornando le impostazioni DNS in modo appropriato.