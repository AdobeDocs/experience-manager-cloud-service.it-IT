---
title: Aggiunta di un record TXT
description: Aggiunta di un nome di dominio personalizzato
translation-type: tm+mt
source-git-commit: b76a22469f248dde316dcaa514a906fe4361afd1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# Aggiunta di un record TXT {#adding-txt}

Un record TXT DNS autorizza l&#39;hosting di un dominio in un servizio CDN. Il cliente deve creare un record TXT DNS nella zona che autorizza Cloud Manager a distribuire il servizio CDN con il dominio personalizzato e associarlo al servizio di back-end. Questa associazione è interamente sotto il controllo del cliente e autorizza fortemente Cloud Manager a distribuire il contenuto dal servizio a un dominio. Tale autorizzazione può essere concessa e revocata.

Prima di creare un record TXT è possibile seguire i passaggi indicati di seguito:

* È possibile modificare i record DNS per il dominio dell&#39;organizzazione o contattare la persona appropriata che può farlo.
* Identificare l’host o il registrar del dominio se non lo si conosce già.

Quando avviate la verifica del dominio, Cloud Manager vi dà il nome e il valore TXT da utilizzare per la verifica. Aggiungi un record TXT al server DNS del dominio utilizzando il nome e il valore specificati.

1. Accedi al tuo host di dominio e visita la sezione dei record DNS.
1. Aggiungete `_aemverification.[yourdomainname]` come nome e aggiungete il valore TXT esattamente come viene visualizzato.
Fare riferimento agli esempi riportati nella tabella seguente.

| Dominio | Nome | Valore TXT |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | Visualizzato nell’interfaccia di Cloud Manager ed è specifico per il dominio e l’ambiente di Cloud Manager |
| `test.example.com` | `_aemverification.test.example.com` | Visualizzato nell’interfaccia di Cloud Manager ed è specifico per il dominio e l’ambiente di Cloud Manager |

Al termine, potete verificare il risultato eseguendo: `dig _aemverification.[yourdomainname] -t txt`.
Il risultato atteso deve visualizzare il valore TXT fornito nell&#39;interfaccia utente di Cloud Manager.

Ad esempio, se il dominio è `example.com`, eseguire: `dig TXT _aemverification.example.com -t txt`.

>[!NOTE]
>Esistono anche vari [strumenti di ricerca DNS](https://www.ultratools.com/tools/dnsLookup), Google DoH può essere utilizzato per cercare le voci dei record TXT e identificare se il record TXT è mancante o errato.

