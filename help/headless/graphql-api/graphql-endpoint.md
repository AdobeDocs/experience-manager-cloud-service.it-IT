---
title: Gestire gli endpoint GraphQL in AEM
description: Scopri come gestire gli endpoint GraphQL in Adobe Experience Manager as a Cloud Service per la distribuzione di contenuti headless.
feature: Content Fragments,GraphQL API
source-git-commit: 4e37db128aa31d6e8e950be0d077eae921a27468
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 5%

---


# Gestire gli endpoint GraphQL in AEM {#graphql-aem-endpoint}

L’endpoint è il percorso utilizzato per accedere a GraphQL per AEM. Utilizzando questo percorso (o la tua app) puoi:

* accedere allo schema GraphQL,
* invia le query GraphQL,
* ricevere le risposte (alle query GraphQL).

Esistono due tipi di endpoint in AEM:

* Globale
   * Disponibile per tutti i siti.
   * Questo endpoint può utilizzare tutti i modelli di frammenti di contenuto di tutte le configurazioni di Sites (definite nella sezione [Browser di configurazione](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)).
   * Se esistono modelli di frammento di contenuto che devono essere condivisi tra le configurazioni di Sites, questi devono essere creati nelle configurazioni di Sites globali.
* Configurazioni siti:
   * Corrisponde a una configurazione Sites, come definita nella [Browser di configurazione](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser).
   * Specifico per un sito/progetto specifico.
   * Un endpoint specifico per la configurazione di Sites utilizzerà i modelli di frammento di contenuto di quella specifica configurazione di Sites insieme a quelli della configurazione di Sites globale.

>[!CAUTION]
>
>L’Editor frammento di contenuto può consentire a un frammento di contenuto di una configurazione Sites di fare riferimento a un frammento di contenuto di un’altra configurazione Sites (tramite criteri).
>
>In questo caso non tutti i contenuti saranno recuperabili utilizzando un endpoint specifico per la configurazione di Sites.
>
>L’autore del contenuto deve controllare questo scenario; ad esempio, potrebbe essere utile considerare l’idea di inserire modelli di frammenti di contenuto condivisi nella configurazione Siti globali .

Il percorso dell&#39;archivio di GraphQL per AEM endpoint globale è:

`/content/cq:graphql/global/endpoint`

Per cui l’app può utilizzare il seguente percorso nell’URL della richiesta:

`/content/_cq_graphql/global/endpoint.json`

Per abilitare un endpoint per GraphQL per AEM è necessario:

* [Abilita l&#39;endpoint GraphQL](#enabling-graphql-endpoint)
* [Pubblica l’endpoint GraphQL](#publishing-graphql-endpoint)

## Abilitazione dell’endpoint GraphQL {#enabling-graphql-endpoint}

Per abilitare un endpoint GraphQL è innanzitutto necessario disporre di una configurazione appropriata. Vedi [Frammenti di contenuto - Browser di configurazione](/help/assets/content-fragments/content-fragments-configuration-browser.md).

>[!CAUTION]
>
>Se la [l’utilizzo di modelli di frammento di contenuto non è stato abilitato](/help/assets/content-fragments/content-fragments-configuration-browser.md), **Crea** l’opzione non sarà disponibile.

Per abilitare l&#39;endpoint corrispondente:

1. Passa a **Strumenti**, **Risorse**, quindi seleziona **GraphQL**.
1. Seleziona **Crea**.
1. La **Crea nuovo endpoint GraphQL** si aprirà la finestra di dialogo . Qui puoi specificare:
   * **Nome**: nome del punto finale; puoi immettere qualsiasi testo.
   * **Utilizza lo schema GraphQL fornito da**: utilizza il menu a discesa per selezionare il sito o il progetto richiesto.

   >[!NOTE]
   >
   >Nella finestra di dialogo viene visualizzato il seguente avviso:
   >
   >* *Se non vengono gestiti correttamente, gli endpoint GraphQL possono introdurre problemi di prestazioni e sicurezza dei dati. Dopo aver creato un endpoint, assicurati di impostare le autorizzazioni appropriate.*


1. Conferma con **Crea**.
1. La **Passaggi successivi** La finestra di dialogo fornisce un collegamento diretto alla console Sicurezza per garantire che l’endpoint appena creato disponga delle autorizzazioni appropriate.

   >[!CAUTION]
   >
   >L’endpoint è accessibile a tutti. Questo può creare problemi di sicurezza, soprattutto per le istanze di pubblicazione, in quanto le query GraphQL possono imporre un carico pesante sul server.
   >
   >Puoi impostare ACL, appropriati al tuo caso d&#39;uso, sull&#39;endpoint.

## Pubblicazione dell’endpoint GraphQL {#publishing-graphql-endpoint}

Seleziona il nuovo endpoint e **Pubblica** per renderlo completamente disponibile in tutti gli ambienti.

>[!CAUTION]
>
>L’endpoint è accessibile a tutti.
>
>Nelle istanze di pubblicazione questo può rappresentare un problema di sicurezza, in quanto le query GraphQL possono imporre un carico pesante sul server.
>
>Devi configurare [ACL appropriati al tuo caso d&#39;uso](/help/headless/security/permissions.md) sull&#39;endpoint.