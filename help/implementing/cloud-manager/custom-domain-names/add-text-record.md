---
title: Aggiunta di un record TXT
description: Scopri come aggiungere un record TXT per l’aggiunta di un nome di dominio personalizzato in Cloud Manager.
exl-id: d441de29-af41-4d3e-9155-531af9702841
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 91%

---

# Aggiunta di un record TXT {#adding-txt}

Un record TXT DNS fornisce l’autorizzazione per ospitare un dominio in un servizio CDN. Crea il record TXT DNS nella zona che autorizza Cloud Manager a distribuire il servizio CDN con il dominio personalizzato e associalo al servizio back-end. Questa associazione è interamente sotto il tuo controllo e autorizza Cloud Manager a distribuire contenuti dal servizio a un dominio. Tale autorizzazione può essere concessa e revocata. Il record TXT è specifico del dominio e dell’ambiente di Cloud Manager.

Prima di aggiungere un record TXT è necessario soddisfare i requisiti riportati di seguito.

* È necessario essere in grado di modificare i record DNS per il dominio dell&#39;organizzazione o di contattare la persona appropriata che può farlo.
* Se non disponi ancora di questa informazione, identifica l’host o il registrar del dominio.

Quando avvii la verifica del dominio, Cloud Manager indica il nome e il valore TXT da utilizzare per la verifica. Aggiungi un record TXT al server DNS del dominio con il nome e il valore specificati.

1. Accedi all’host del dominio e individua la sezione relativa ai record DNS.
1. Aggiungi `_aemverification.[yourdomainname]` come valore del **Nome**, quindi aggiungi il valore TXT esattamente come visualizzato.

Consulta gli esempi in questa tabella.

| Dominio | Nome | Valore TXT |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | Copia l’intero valore visualizzato nell’interfaccia utente di Cloud Manager. Il valore è specifico del dominio e dell’ambiente. Esempio:<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
| `www.example.com` | `_aemverification.www.example.com` | Copia l’intero valore visualizzato nell’interfaccia utente di Cloud Manager. Il valore è specifico del dominio e dell’ambiente. Esempio:<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

Al termine dell’operazione puoi verificare il risultato eseguendo il seguente comando:

```shell
dig _aemverification.[yourdomainname] -t txt
```

Il risultato atteso deve visualizzare il valore TXT fornito nell’interfaccia utente di Cloud Manager.

Se ad esempio il dominio è `example.com`, esegui:

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>Ce ne sono diversi [Strumenti di ricerca DNS](https://www.ultratools.com/tools/dnsLookup) disponibile. Puoi utilizzare Google DoH per cercare voci di record TXT e identificare se un record TXT risulta mancante o errato.
