---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager] as a Cloud Service.
source-git-commit: 4aa4954f214545dcd768fdf955f1fc2f776da939
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 34%

---


# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note tecniche sulla versione per la versione di manutenzione corrente dell’Experience Manager as a Cloud Service.

## Versione 11835 {#release-11835}

Di seguito sono riepilogati i continui miglioramenti della versione di manutenzione 11835, rilasciata pubblicamente il 19 aprile 2023. Questa versione di manutenzione è un aggiornamento della versione di manutenzione precedente, la 11382.

L’abilitazione delle funzioni per questa versione di manutenzione ti darà accesso al set di funzioni completo. Consulta le [note sulla versione corrente](/help/release-notes/release-notes-cloud/release-notes-current.md) per ottenere informazioni dettagliate.

### Problemi risolti {#fixed-issues-11835}

- SITES-12573 - Le query GraphQL che utilizzano variabili all&#39;interno di un filtro avranno esito negativo se non viene specificata una variabile. Non effettuare l&#39;aggiornamento a questa versione utilizza GraphQL con AEM as a Cloud Service.
- SKYOPS-51970 - È stata identificata la regressione della versione FACT utilizzata nel passaggio buildImage, che porta a una mappatura utente non corrispondente.
- GRANITE-44542 - Sono stati segnalati problemi per i clienti che non hanno specificato un tipo di nodo del pacchetto (fornendo un .content.xml con jcr:primaryType) per le cartelle incluse nel filtro del pacchetto. Questo ha causato la gestione di queste cartelle come nt:folder, creando problemi in vari casi.
- SKYOPS-56928 - La regressione HTTPD di Apache potrebbe causare errori 404. Se si verificano tali problemi, per motivi di sicurezza, si consiglia di eseguire il rollback alla versione precedente ed evitare l’esecuzione di una pipeline durante tale periodo di tempo.

### Tecnologie incorporate {#embedded-tech-11835}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [API Oak API 1.44.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| API SLING AEM | Versione 2.27.0 | [API Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versione 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | Versione 2.21.2 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
