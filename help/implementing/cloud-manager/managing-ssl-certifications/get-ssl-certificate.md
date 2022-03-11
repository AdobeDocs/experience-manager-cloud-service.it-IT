---
title: Ottenere un certificato SSL - Gestione dei certificati SSL
description: Ottenere un certificato SSL - Gestione dei certificati SSL
exl-id: a3a247e5-164a-4c9c-aeed-bde882635e6f
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---

# Ottenimento di un certificato SSL {#getting-an-ssl-certificate}

Le aziende utilizzano i certificati SSL per proteggere i propri siti web e consentire ai propri clienti di fidarsi di loro. Per utilizzare il protocollo SSL, un server web richiede l’utilizzo di un certificato SSL. Cloud Manager non fornisce certificati SSL o chiavi private. Questi devono essere ottenuti presso le autorità di certificazione (CA).

Quando un’entità richiede un certificato da un’autorità di certificazione, la CA completa un processo di verifica. Questo può variare dalla verifica del controllo dei nomi di dominio alla raccolta dei documenti di registrazione della società e degli accordi di sottoscrizione. Una volta verificate le informazioni di un&#39;entità, la CA firmerà la propria chiave pubblica utilizzando la chiave privata della CA. Poiché tutte le principali autorità di certificazione dispongono di certificati radice nei browser Web, il certificato dell’entità verrà collegato tramite un *catena di affidabilità* e il browser web lo riconoscerà come certificato attendibile.

>[!NOTE]
>AEM as a Cloud Service accetterà solo i certificati OV (Organization Validation) o EV (Extended Validation). I certificati DV (Convalida dominio) o autofirmati non verranno accettati. I certificati OV ed EV forniscono agli utenti informazioni aggiuntive convalidate da CA che possono utilizzare per stabilire se il proprietario di un sito web, il mittente di un&#39;e-mail o il firmatario digitale di un codice eseguibile o di documenti PDF è affidabile. I certificati DV sono comuni e poco costosi. Tuttavia, non consentono la verifica della proprietà.
>Inoltre, qualsiasi certificato deve essere un certificato TLS X.509 di un’autorità di certificazione (CA) affidabile con una chiave privata RSA a 2048 bit corrispondente.
