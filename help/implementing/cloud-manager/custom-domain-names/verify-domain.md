---
title: Verifica del dominio
description: Verifica del dominio
translation-type: tm+mt
source-git-commit: d2a98cf340dc755407250a9a9649addb75ad87d2
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---


# Verifica del dominio {#verify-domain-name}

Un record TXT DNS autorizza l&#39;hosting di un dominio in un servizio CDN. Il cliente deve creare un record TXT DNS nella zona che autorizza Cloud Manager a distribuire il servizio CDN con il dominio personalizzato e associarlo al servizio di back-end. Questa associazione è interamente sotto il controllo del cliente e autorizza fortemente Cloud Manager a distribuire il contenuto dal servizio a un dominio. Tale autorizzazione può essere concessa e revocata. Il record TXT è specifico per l&#39;ambiente Domain e Cloud Manager.

1. Accedi al tuo host di dominio e visita la sezione dei record DNS.
1. Copiate e incollate la voce TXT nella zona DNS in cui si trova il dominio personalizzato, esattamente come viene visualizzata. Se avete bisogno di un &quot;nome&quot; per la vostra voce, dategli `@`.

>[!NOTE]
>Diversi strumenti di ricerca DNS come [DNS Lookup Tool](https://www.ultratools.com/tools/dnsLookup), Google DoH possono essere utilizzati per cercare voci di record TXT e identificare se il record TXT è mancante o errato.
