---
title: Aggiunta di un record TXT
description: Aggiunta di un nome di dominio personalizzato
exl-id: d441de29-af41-4d3e-9155-531af9702841
translation-type: tm+mt
source-git-commit: 4903f97c1bf0e7c8e96d604feb005d9611a7d9bb
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# Aggiunta di un record TXT {#adding-txt}

Un record TXT DNS autorizza un dominio ad essere ospitato in un servizio CDN. Il cliente deve creare un record TXT DNS nella zona che autorizza Cloud Manager a distribuire il servizio CDN con il dominio personalizzato e associarlo al servizio back-end. Questa associazione è interamente sotto il controllo del cliente e autorizza fortemente Cloud Manager a distribuire contenuti dal servizio a un dominio. Tale autorizzazione può essere concessa e revocata.

Prima di creare un record TXT, è possibile seguire i passaggi seguenti:

* Avere la possibilità di modificare i record DNS per il dominio della tua organizzazione o contattare la persona appropriata in grado di farlo.
* Identifica l&#39;host di dominio o il registrar se non lo sai già.

Quando avvii la verifica del dominio, Cloud Manager ti dà il nome e il valore TXT da utilizzare per la verifica. Aggiungi un record TXT al server DNS del tuo dominio utilizzando il Nome e il Valore specificati.

1. Accedi al tuo host di dominio e visita la sezione Record DNS .
1. Aggiungi `_aemverification.[yourdomainname]` come Nome e aggiungi il valore TXT esattamente come viene visualizzato.
Fai riferimento agli esempi nella tabella seguente.

| Dominio | Nome | Valore TXT |
|--- |--- |---|
| `example.com` | `_aemverification` | Visualizzato nell’interfaccia utente di Cloud Manager ed è specifico per il dominio e l’ambiente Cloud Manager |
| `test.example.com` | `_aemverification` | Visualizzato nell’interfaccia utente di Cloud Manager ed è specifico per il dominio e l’ambiente Cloud Manager |

Al termine, puoi verificare il risultato eseguendo: `dig _aemverification.[yourdomainname] -t txt`.
Il risultato atteso deve visualizzare il valore TXT fornito nell’interfaccia utente di Cloud Manager.

Ad esempio, se il dominio è `example.com`, esegui: `dig TXT _aemverification.example.com -t txt`.

>[!NOTE]
>Esistono anche vari [strumenti di ricerca DNS](https://www.ultratools.com/tools/dnsLookup), Google DoH può essere utilizzato per cercare voci di record TXT e identificare se il record TXT è mancante o errato.
