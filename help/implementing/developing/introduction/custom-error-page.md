---
title: Pagine di errore personalizzate
description: AEM viene fornito con un gestore di errori standard per la gestione degli errori HTTP, che può essere personalizzato.
exl-id: b74c65d1-8ef5-4ad4-8255-8187f3b1d84c
source-git-commit: db997127c6cbba434b86990852d1ba590d5f12a5
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 2%

---

# Personalizzazione delle pagine di errore {#customizing-error-pages}

AEM viene fornito con un gestore di errori standard per la gestione degli errori HTTP; ad esempio, mostrando:

![Messaggio di errore standard](assets/error-message-standard.png)

Per rispondere agli errori, AEM fornisce un `404.jsp` script sotto `/libs/sling/servlet/errorhandler`.

>[!TIP]
>
>Poiché AEM è basato su Apache Sling, sono disponibili ulteriori informazioni [nella documentazione relativa alla gestione degli errori Apache.](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html)

>[!NOTE]
>
>Su un&#39;istanza dell&#39;autore, [Filtro di debug CQ WCM](/help/implementing/deploying/configuring-osgi.md) è attivato per impostazione predefinita. Questo si traduce sempre nel codice di risposta 200. Il gestore di errori predefinito risponde scrivendo la traccia completa dello stack nella risposta.
>
>In un&#39;istanza di pubblicazione, il filtro di debug CQ WCM è **sempre** disabilitato (anche se configurato come abilitato).

## Come personalizzare le pagine visualizzate dal gestore errori {#how-to-customize-pages-shown-by-the-error-handler}

È possibile sviluppare script personalizzati per personalizzare le pagine mostrate dal gestore di errori quando si verifica un errore. A questo scopo, sfrutterai [Meccanismo di sovrapposizione standard AEM](/help/implementing/developing/introduction/overlays.md) in modo che le pagine personalizzate vengano create in `/apps` e sovrapponi le pagine predefinite sotto `/libs`.

1. Nell’archivio, copia gli script predefiniti:

   * da `/libs/sling/servlet/errorhandler/`
   * a `/apps/sling/servlet/errorhandler/`

   Il percorso di destinazione non esiste per impostazione predefinita, pertanto sarà necessario crearlo per la prima volta.

1. Accedi a `/apps/sling/servlet/errorhandler`. Qui puoi effettuare le seguenti operazioni:

   * modificare lo script esistente appropriato per fornire le informazioni richieste. Oppure
   * crea e modifica un nuovo script per il codice richiesto.

1. Salva le modifiche e verifica.

>[!CAUTION]
>
>La `404.jsp` lo script è stato specificamente progettato per garantire l&#39;AEM dell&#39;autenticazione; in particolare, per consentire l&#39;accesso al sistema in caso di questi errori.
>
>Pertanto, la sostituzione di questo script dovrebbe essere fatto con grande cura.

### Personalizzazione della risposta agli errori HTTP 500 {#customizing-the-response-to-http-errors}

HTTP [Errore server interno 500](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) indica un errore lato server, ad esempio il server che ha riscontrato una condizione imprevista che ha impedito il soddisfacimento della richiesta.

Quando l’elaborazione della richiesta genera un’eccezione, il framework Sling Apache (AEM basato su):

* Registra l&#39;eccezione
* E restituisce il corpo della risposta:
   * Codice di risposta HTTP 500
   * Traccia dello stack di eccezioni

Da [personalizzazione delle pagine mostrate dal gestore di errori](#how-to-customize-pages-shown-by-the-error-handler) a `500.jsp` è possibile creare uno script. Tuttavia, viene utilizzato solo se `HttpServletResponse.sendError(500)` è eseguito esplicitamente; ovvero da un catcher di eccezione.

In caso contrario, il codice di risposta è impostato su 500, ma il `500.jsp` script non eseguito.

Per gestire 500 errori, il nome file dello script del gestore di errori deve essere lo stesso della classe di eccezione (o superclasse). Per gestire tutte queste eccezioni è possibile creare uno script `/apps/sling/servlet/errorhandler/Throwable.jsp` o `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!NOTE]
>
>In AEM come Cloud Service, la rete CDN fornisce una pagina di errore generico ogni volta che viene ricevuto un errore 5XX dal back-end. Per consentire il passaggio della risposta effettiva del backend , devi aggiungere la seguente intestazione alla risposta:
>`x-aem-error-pass: true`
>Questo funzionerà solo per le risposte provenienti da AEM o dal livello Apache/Dispatcher. Altri errori imprevisti provenienti da livelli di infrastruttura intermedi continueranno a visualizzare la pagina di errore generico.

>[!CAUTION]
>
>Su un&#39;istanza dell&#39;autore, [Filtro di debug CQ WCM](/help/implementing/deploying/configuring-osgi.md) è attivato per impostazione predefinita. Questo si traduce sempre nel codice di risposta 200. Il gestore di errori predefinito risponde scrivendo la traccia completa dello stack nella risposta.
>
>Per un gestore di errori personalizzato, sono necessarie le risposte con codice 500, quindi è necessario [CQ WCM Debug Filter deve essere disabilitato.](/help/implementing/deploying/configuring-osgi.md) In questo modo viene restituito il codice di risposta 500, che a sua volta attiva il gestore di errori Sling corretto.
>
>In un&#39;istanza di pubblicazione, il filtro di debug CQ WCM è **sempre** disabilitato (anche se configurato come abilitato).
