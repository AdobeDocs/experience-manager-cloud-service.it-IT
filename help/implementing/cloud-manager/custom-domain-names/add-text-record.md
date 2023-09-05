---
title: Aggiunta di un record TXT
description: Scopri come aggiungere un record TXT per l’aggiunta di un nome di dominio personalizzato in Cloud Manager.
exl-id: d441de29-af41-4d3e-9155-531af9702841
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: ht
source-wordcount: '329'
ht-degree: 100%

---

# Aggiunta di un record TXT {#adding-txt}

Un record TXT DNS fornisce l’autorizzazione per ospitare un dominio in un servizio CDN. Crea il record TXT DNS nella zona che autorizza Cloud Manager a distribuire il servizio CDN con il dominio personalizzato e associalo al servizio back-end. Questa associazione è interamente sotto il tuo controllo e autorizza Cloud Manager a distribuire contenuti dal servizio a un dominio. Tale autorizzazione può essere concessa e revocata. Il record TXT è specifico del dominio e dell’ambiente di Cloud Manager.

Prima di aggiungere un record TXT è necessario soddisfare i requisiti riportati di seguito.

* È necessario disporre dell’autorizzazione per modificare i record DNS del dominio dell’organizzazione o poter contattare la persona designata per l’operazione.
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
>Sono disponibili diversi [strumenti di ricerca DNS](https://www.ultratools.com/tools/dnsLookup). Puoi utilizzare Google DoH per cercare voci di record TXT e identificare se un record TXT risulta mancante o errato.
