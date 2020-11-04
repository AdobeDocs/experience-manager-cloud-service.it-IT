---
title: Ottenimento di un certificato SSL - Gestione dei certificati SSL
description: Ottenimento di un certificato SSL - Gestione dei certificati SSL
translation-type: tm+mt
source-git-commit: e27e5302802e68dce2a5713626950896bb35420a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# Ottenimento di un certificato SSL {#getting-an-ssl-certificate}

Le aziende utilizzano i certificati SSL per proteggere i propri siti Web e consentire ai clienti di fidarsi di loro. Per utilizzare il protocollo SSL, un server Web richiede l’utilizzo di un certificato SSL. Cloud Manager non fornisce certificati SSL o chiavi private. Questi devono essere ottenuti dalle autorità di certificazione (CA).

Quando un&#39;entità richiede un certificato da un&#39;autorità di certificazione (CA), la CA completa un processo di verifica. Questo può spaziare dalla verifica del controllo dei nomi di dominio alla raccolta di documenti di registrazione aziendali e di contratti di sottoscrizione.

Una volta verificate le informazioni di un&#39;entità, la CA firmerà la propria chiave pubblica utilizzando la chiave privata della CA. Poiché tutte le principali autorità di certificazione dispongono di certificati radice nei browser Web, il certificato dell&#39;entità sarà collegato tramite una *catena di affidabilità* e il browser Web lo riconoscerà come certificato attendibile.

