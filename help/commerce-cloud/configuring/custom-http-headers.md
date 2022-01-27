---
title: Intestazioni HTTP personalizzate
description: Configurazione di intestazioni HTTP personalizzate
exl-id: 2cef5d4b-45f6-4d72-a24b-67ca53d9057d
source-git-commit: 05a412519a2d2d0cba0a36c658b8fed95e59a0f7
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 3%

---

# Intestazioni HTTP personalizzate {#custom-http-headers}

## Panoramica {#overview}

Per ottenere un maggiore controllo sul back-end, gli autori possono configurare intestazioni HTTP personalizzate che verrebbero inviate al motore di e-commerce, insieme a quelle già inviate da CIF. I casi d’uso comuni includono configurazioni multi-store in cui puoi utilizzare intestazioni HTTP per controllare la risposta del back-end commerce.

>[!NOTE]
>
>Gli sviluppatori possono sempre configurare intestazioni HTTP personalizzate utilizzando la configurazione client GraphQL.

## Configurazione {#configuration}

Per configurare le intestazioni HTTP personalizzate, è innanzitutto necessario definirle. Le intestazioni HTTP personalizzate devono prima essere definite aggiungendole al `com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl` configurazione del servizio utilizzando una configurazione OSGi.

Puoi configurare i valori delle intestazioni HTTP nella pagina Configurazione Cloud Service per il progetto:

1. Vai alla pagina di configurazione del Cloud Service in Strumenti -> Cloud Services -> Configurazione CIF
1. Apri una configurazione esistente o creane una nuova
1. Vai alla scheda &quot;Avanzate&quot; e trova il campo multiplo &quot;Intestazioni HTTP personalizzate&quot;. È possibile selezionare le intestazioni definite in precedenza e assegnare loro valori.

I componenti che utilizzano la configurazione del servizio cloud di cui sopra invieranno queste intestazioni HTTP con ogni richiesta GraphQL.

## Restrizioni {#restrictions}

Il servizio consente di definire i nomi di intestazione, inclusi quelli standard, ma non sarà disponibile per la configurazione. In altre parole, non è possibile ignorare le intestazioni HTTP standard utilizzando questa funzione. È possibile trovare un elenco di nomi di intestazione con restrizioni [qui](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers). Oltre a questi, ci sono altre due intestazioni che non possono essere utilizzate:

* &quot;Store&quot; - utilizzato da CIF per identificare l’archivio Adobe Commerce
* &quot;Preview-Version&quot; - utilizzato da CIF per recuperare i prodotti in staging
