---
title: Verifica del dominio
description: Verifica del dominio
source-git-commit: d2a98cf340dc755407250a9a9649addb75ad87d2
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---


# Verifica del dominio {#verify-domain-name}

Un record TXT DNS autorizza un dominio ad essere ospitato in un servizio CDN. Il cliente deve creare un record TXT DNS nella zona che autorizza Cloud Manager a distribuire il servizio CDN con il dominio personalizzato e associarlo al servizio back-end. Questa associazione è interamente sotto il controllo del cliente e autorizza fortemente Cloud Manager a distribuire contenuti dal servizio a un dominio. Tale autorizzazione può essere concessa e revocata. Il record TXT è specifico per l’ambiente Domain e Cloud Manager.

1. Accedi al tuo host di dominio e visita la sezione Record DNS .
1. Copia e incolla la voce TXT nella tua zona DNS in cui si trova il dominio personalizzato, esattamente come appare. Se hai bisogno di un &quot;nome&quot; per la tua voce, dagli `@`.

>[!NOTE]
>Vari strumenti di ricerca DNS come [Strumento di ricerca DNS](https://www.ultratools.com/tools/dnsLookup), Google DoH può essere utilizzato per cercare voci di record TXT e identificare se il record TXT è mancante o errato.
