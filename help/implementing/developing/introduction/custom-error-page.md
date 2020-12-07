---
title: Pagine di errore personalizzate
description: AEM viene fornito un gestore di errori standard per la gestione degli errori HTTP, che può essere personalizzato.
translation-type: tm+mt
source-git-commit: d7e9bdee83f1b85436185ca57420ee178268cb33
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---


# Personalizzazione delle pagine di errore {#customizing-error-pages}

AEM viene fornito con un gestore di errori standard per la gestione degli errori HTTP; ad esempio, mostrando:

![Messaggio di errore standard](assets/error-message-standard.png)

Per rispondere agli errori, AEM uno script `404.jsp` in `/libs/sling/servlet/errorhandler`.

>[!TIP]
>
>Poiché AEM è basato su Apache Sling, ulteriori informazioni sono disponibili [nella documentazione relativa alla gestione degli errori Apache.](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html)

>[!NOTE]
>
>In un&#39;istanza di creazione, il [filtro di debug CQ WCM](/help/implementing/deploying/configuring-osgi.md) è abilitato per impostazione predefinita. Questo restituisce sempre il codice di risposta 200. Il gestore errori predefinito risponde scrivendo la traccia dello stack completa nella risposta.
>
>In un&#39;istanza di pubblicazione, il filtro di debug CQ WCM è sempre disabilitato (anche se configurato come abilitato).****

## Come personalizzare le pagine visualizzate dal gestore errori {#how-to-customize-pages-shown-by-the-error-handler}

È possibile sviluppare script personalizzati per personalizzare le pagine mostrate dal gestore errori quando si verifica un errore. A tal fine, si utilizzerà il meccanismo di sovrapposizione [AEM standard](/help/implementing/developing/introduction/overlays.md) in modo che le pagine personalizzate vengano create sotto `/apps` e si sovrappongano alle pagine predefinite sotto `/libs`.

1. Nell&#39;archivio, copiare gli script predefiniti:

   * da `/libs/sling/servlet/errorhandler/`
   * a `/apps/sling/servlet/errorhandler/`

   Il percorso di destinazione non esiste per impostazione predefinita, pertanto sarà necessario crearlo al primo tentativo.

1. Accedi a `/apps/sling/servlet/errorhandler`. Potete effettuare le seguenti operazioni:

   * modificare lo script esistente appropriato per fornire le informazioni richieste. Oppure
   * creare e modificare un nuovo script per il codice richiesto.

1. Salvate le modifiche e verificate il comportamento.

>[!CAUTION]
>
>Lo script `404.jsp` è stato progettato specificamente per AEM l&#39;autenticazione; in particolare, per consentire l&#39;accesso al sistema in caso di tali errori.
>
>Pertanto, la sostituzione di questo script dovrebbe essere fatta con grande attenzione.

### Personalizzazione della risposta agli errori HTTP 500 {#customizing-the-response-to-http-errors}

L&#39;errore HTTP [500 Internal Server Error](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) indica un errore sul lato server, ad esempio se il server si trova in una condizione imprevista che gli ha impedito di soddisfare la richiesta.

Quando l&#39;elaborazione della richiesta genera un&#39;eccezione, il framework Apache Sling (AEM basato su):

* Registra l&#39;eccezione
* E restituisce il risultato nel corpo della risposta:
   * Codice di risposta HTTP 500
   * Traccia dello stack di eccezioni

Per [personalizzare le pagine visualizzate dal gestore di errori](#how-to-customize-pages-shown-by-the-error-handler) è possibile creare uno script `500.jsp`. Tuttavia, viene utilizzato solo se `HttpServletResponse.sendError(500)` viene eseguito in modo esplicito; ovvero da un rilevatore di eccezioni.

In caso contrario, il codice di risposta è impostato su 500, ma lo script `500.jsp` non viene eseguito.

Per gestire 500 errori, il nome file dello script del gestore di errori deve essere uguale alla classe di eccezione (o superclasse). Per gestire tutte queste eccezioni è possibile creare uno script `/apps/sling/servlet/errorhandler/Throwable.jsp` o `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!CAUTION]
>
>In un&#39;istanza di creazione, il [filtro di debug CQ WCM](/help/implementing/deploying/configuring-osgi.md) è abilitato per impostazione predefinita. Questo restituisce sempre il codice di risposta 200. Il gestore errori predefinito risponde scrivendo la traccia dello stack completa nella risposta.
>
>Per un gestore di errori personalizzato, sono necessarie risposte con codice 500, pertanto è necessario disabilitare il filtro di debug [CQ WCM.](/help/implementing/deploying/configuring-osgi.md) In questo modo viene restituito il codice di risposta 500, che a sua volta attiva il gestore errori Sling corretto.
>
>In un&#39;istanza di pubblicazione, il filtro di debug CQ WCM è sempre disabilitato (anche se configurato come abilitato).****
