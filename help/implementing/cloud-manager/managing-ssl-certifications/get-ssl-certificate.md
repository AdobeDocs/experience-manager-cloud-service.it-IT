---
title: Ottenimento di un certificato SSL - Gestione dei certificati SSL
description: Ottenimento di un certificato SSL - Gestione dei certificati SSL
translation-type: tm+mt
source-git-commit: 40119f7b3bdf36af668b79afbcb2802a0b2a6033
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Ottenimento di un certificato SSL {#getting-an-ssl-certificate}

Le aziende utilizzano i certificati SSL per proteggere i propri siti Web e consentire ai clienti di fidarsi di loro. Per utilizzare il protocollo SSL, un server Web richiede l’utilizzo di un certificato SSL. Cloud Manager non fornisce certificati SSL o chiavi private. Questi devono essere ottenuti dalle autorità di certificazione (CA).

Quando un&#39;entità richiede un certificato da un&#39;autorità di certificazione, la CA completa un processo di verifica. Questo può spaziare dalla verifica del controllo dei nomi di dominio alla raccolta di documenti di registrazione aziendali e di contratti di sottoscrizione. Una volta verificate le informazioni di un&#39;entità, la CA firmerà la propria chiave pubblica utilizzando la chiave privata della CA. Poiché tutte le principali autorità di certificazione dispongono di certificati radice nei browser Web, il certificato dell&#39;entità sarà collegato tramite una *catena di affidabilità* e il browser Web lo riconoscerà come certificato attendibile.

>[!NOTE]
>AEM come Cloud Service accetta solo i certificati OV(Organization Validation) o EV(Extended Validation). I certificati DV(Domain Validation) o autofirmati non saranno accettati. I certificati OV e EV forniscono agli utenti informazioni aggiuntive convalidate da CA che possono utilizzare per stabilire se il proprietario di un sito Web, il mittente di un&#39;e-mail o il firmatario digitale di un codice eseguibile o di documenti PDF è affidabile. I certificati DV sono comuni e poco costosi. Tuttavia, non consentono la verifica della proprietà.
>Inoltre, qualsiasi certificato deve essere un certificato TLS X.509 di un&#39;autorità di certificazione (CA) affidabile con una chiave privata RSA a 2048 bit corrispondente.

