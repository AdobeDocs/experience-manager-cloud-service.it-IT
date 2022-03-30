---
title: Aggiunta di un record TXT
description: Scopri come aggiungere un record TXT per aggiungere un nome di dominio personalizzato in Cloud Manager.
exl-id: d441de29-af41-4d3e-9155-531af9702841
source-git-commit: c80b7288b86ac62da17d5a83ec96cb882e36f687
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 4%

---

# Aggiunta di un record TXT {#adding-txt}

Un record TXT DNS autorizza un dominio ad essere ospitato in un servizio CDN. Devi creare un record TXT DNS nella zona che autorizza Cloud Manager a distribuire il servizio CDN con il dominio personalizzato e associarlo al servizio back-end. Questa associazione è interamente sotto il tuo controllo e autorizza Cloud Manager a distribuire contenuti dal servizio a un dominio. Tale autorizzazione può essere concessa e revocata.

È necessario soddisfare questi requisiti prima di aggiungere un record TXT.

* Devi avere la possibilità di modificare i record DNS per il dominio della tua organizzazione o di contattare la persona appropriata che può farlo.
* Devi identificare l’host o il registrar del dominio se non lo sai già.

Quando avvii la verifica del dominio, Cloud Manager ti dà il nome e il valore TXT da utilizzare per la verifica. Aggiungi un record TXT al server DNS del dominio utilizzando il nome e il valore specificati.

1. Accedi all&#39;host di dominio e trova la sezione record DNS .
1. Aggiungi `_aemverification.[yourdomainname]` come **Nome** e aggiungi il valore TXT esattamente come appare.

Fai riferimento agli esempi in questa tabella.

| Dominio | Nome | Valore TXT |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | Copia l’intero valore visualizzato nell’interfaccia utente di Cloud Manager. Questa funzione è specifica del dominio e dell’ambiente. Esempio:<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
| `www.example.com` | `_aemverification.www.example.com` | Copia l’intero valore visualizzato nell’interfaccia utente di Cloud Manager. Questa funzione è specifica del dominio e dell’ambiente. Esempio:<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

Al termine è possibile verificare il risultato eseguendo il seguente comando

```shell
dig _aemverification.[yourdomainname] -t txt
```

Il risultato atteso deve visualizzare il valore TXT fornito nell’interfaccia utente di Cloud Manager.

Ad esempio, se il dominio è `example.com`, quindi esegui:

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>Sono disponibili [Strumenti di ricerca DNS](https://www.ultratools.com/tools/dnsLookup) disponibile. Google DoH può essere utilizzato per cercare voci di record TXT e identificare se il record TXT è mancante o errato.
