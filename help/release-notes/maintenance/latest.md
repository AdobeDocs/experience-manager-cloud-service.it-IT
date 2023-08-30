---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 22ed74b307b9eb4c6c2f72ac2a34e2ab6d30a85c
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 45%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 13239 {#release-13239}

Di seguito sono riepilogati i continui miglioramenti per la versione di manutenzione 13239, rilasciata pubblicamente il 29 agosto 2023. Questa versione di manutenzione sostituisce le 13206 sulla versione.

L’attivazione delle funzioni 2023.9.0 fornirà il set completo di funzioni per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it).

### Miglioramenti {#enhancements-13239}

- GRANITE-46784: Aggiungi l’opzione per disabilitare BearerAuthenticationHandler
- GRANITE-36205: Aggiornare la versione interna di oak all’ultima versione
- GRANITE-47059: rimuovere il bundle SSL di Granite Jetty
- ASSETS-26713: Collegamento esterno all’interfaccia touch per il nuovo dashboard dell’interfaccia utente di Experience, aggiornamento dell’integrazione unificata-shell e dell’ottimizzazione dell’interfaccia utente
- SKYOPS-63302: aggiornare com.adobe.granite:com.adobe.granite.auth.saml alla versione 1.0.54
- GRANITE-46634: Aggiornamento al client di eventi 1.4.0
- GRANITE-46788: Aggiornamento librerie Apache Commons
- GRANITE-29211: Aggiornare gli utensili a Sling Feature Model 2.0
- GRANITE-46705: Aggiornamento ad Apache Felix Http Jetty 4.1.14
- GRANITE-46631: Aggiornamento della versione di Jackrabbit al 2.20.11
- SKYOPS-61895: Aggiornamento a Jackrabbit Filevault 3.7.0

### Problemi risolti {#fixed-issues-13239}

- SKYOPS-63290: Corretta evoluzione dei bucket
- SKYOPS-54607: calcolo del carico del server Ratelimiter non corretto per una richiesta non riuscita
- ASSETS-27648: ContentModelIT non riesce a leggere i file di esclusione da altri bundle
- GRANITE-43744: Sling Authenticator non funziona correttamente in caso di configurazione errata con requisiti di autenticazione e percorso personalizzato
- GRANITE-46419: problema di integrazione AEM con Auth0 Idp
- GRANITE-46292: la configurazione Okta SAML non funziona dopo l’aggiornamento di AEM Cloud

### Problemi noti {#known-issues-13239}

Nessuno.

### Tecnologie incorporate {#embedded-tech-13239}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM OAK | 1,54-T20230817132355-3800a65 | [API Oak API 1.54.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.54.0/index.html) |
| API SLING AEM | Versione 2.27.2 | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versione 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | Versione 2.23.2 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
