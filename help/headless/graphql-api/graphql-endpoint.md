---
title: Gestire gli endpoint GraphQL in AEM
description: Scopri come gestire gli endpoint GraphQL in Adobe Experience Manager as a Cloud Service per la distribuzione di contenuti headless.
feature: Content Fragments,GraphQL API
exl-id: f7164ae3-4074-4db7-8c43-a79cc2ef00b1
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 90%

---

# Gestire gli endpoint GraphQL in AEM {#graphql-aem-endpoint}

L’endpoint è il percorso utilizzato per accedere a GraphQL per AEM. Utilizzando questo percorso (o la tua app) puoi:

* accedere allo schema GraphQL;
* inviare le query GraphQL;
* ricevere le risposte (alle query GraphQL).

Esistono due tipi di endpoint in AEM:

* Globale
   * Disponibile per tutti i siti.
   * Questo endpoint può utilizzare tutti i modelli per frammenti di contenuto di tutte le configurazioni di Sites (definite nella sezione [Browser configurazioni](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser)).
   * Se esistono modelli per frammenti di contenuto che devono essere condivisi tra le configurazioni di Sites, questi devono essere creati nelle configurazioni globali di Sites.
* Configurazioni di Sites:
   * Corrisponde a una configurazione Sites, come definita nella sezione [Browser configurazioni](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser).
   * Sono specifiche per un determinato sito o progetto.
   * Un endpoint specifico per la configurazione di Sites utilizzerà i modelli di frammento di contenuto di quella specifica configurazione di Sites insieme a quelli della configurazione globale di Sites.

>[!CAUTION]
>
>L’Editor frammento di contenuto può consentire a un frammento di contenuto di una configurazione Sites di fare riferimento a un frammento di contenuto di un’altra configurazione Sites (tramite criteri).
>
>In questo caso, non tutti i contenuti sono recuperabili utilizzando un endpoint specifico per la configurazione Sites.
>
>L’autore del contenuto deve controllare questo scenario; ad esempio, potrebbe essere utile inserire modelli per frammenti di contenuto condivisi nella configurazione globale di Sites.

Il percorso dell’archivio di GraphQL per l’endpoint globale di AEM è:

`/content/cq:graphql/global/endpoint`

Per cui l’app può utilizzare il seguente percorso nell’URL della richiesta:

`/content/_cq_graphql/global/endpoint.json`

Per abilitare un endpoint per GraphQL per AEM è necessario:

* [Abilitare l’endpoint GraphQL](#enabling-graphql-endpoint)
* [Pubblicare l’endpoint GraphQL](#publishing-graphql-endpoint)

## Abilitazione dell’endpoint GraphQL {#enabling-graphql-endpoint}

Per abilitare un endpoint GraphQL è innanzitutto necessario disporre di una configurazione appropriata. Vedi la sezione [Frammenti di contenuto - Browser configurazioni](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser).

>[!CAUTION]
>
>Se l’[utilizzo di modelli per frammenti di contenuto non è stato abilitato](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser), l’opzione **Crea** non sarà disponibile.

Per abilitare l’endpoint corrispondente:

1. Passa a **Strumenti**, **Generale**, quindi seleziona **GraphQL**.
1. Seleziona **Crea**.
1. Il **Crea nuovo endpoint GraphQL** viene visualizzata una finestra di dialogo. Qui potrai definire:
   * **Nome**: nome dell’endpoint; puoi immettere qualsiasi testo.
   * **Utilizza lo schema GraphQL fornito da**: utilizza l’elenco a discesa per selezionare il sito/progetto richiesto.

   >[!NOTE]
   >
   >Nella finestra di dialogo viene visualizzato la seguente avvertenza:
   >
   >* *Se non vengono gestiti con attenzione, gli endpoint GraphQL possono causare problemi di prestazioni e sicurezza dei dati. Dopo aver creato un endpoint, verifica di aver impostato le autorizzazioni appropriate.*

1. Conferma con **Crea**.
1. Il **Passaggi successivi** fornirà un collegamento diretto alla console Sicurezza per verificare che l’endpoint creato disponga delle autorizzazioni appropriate.

   >[!CAUTION]
   >
   >L’endpoint è accessibile a tutti. Questo può creare problemi di sicurezza, soprattutto per le istanze di pubblicazione, in quanto le query GraphQL possono imporre un carico pesante sul server.
   >
   >Puoi impostare sull’endpoint eventuali ACL appropriate al tuo caso d’uso.

## Pubblicazione dell’endpoint GraphQL {#publishing-graphql-endpoint}

Seleziona il nuovo endpoint e scegli **Pubblica** per renderlo completamente disponibile in tutti gli ambienti.

>[!CAUTION]
>
>L’endpoint è accessibile a tutti.
>
>Nelle istanze di pubblicazione questo può rappresentare un problema di sicurezza, in quanto le query GraphQL possono imporre un carico pesante sul server.
>
>Devi configurare sull’endpoint le [ACL appropriate al tuo caso d’uso](/help/headless/security/permissions.md).
