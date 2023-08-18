---
title: 'Query persistenti GraphQL: abilitazione della memorizzazione nella cache in Dispatcher'
description: Dispatcher è un livello di memorizzazione in cache e sicurezza davanti agli ambienti di pubblicazione Adobe Experience Manager. Puoi abilitare la memorizzazione nella cache per le query persistenti in AEM Headless.
feature: Dispatcher, GraphQL API
source-git-commit: 0066bfba3a403791c6a35b1280ae04b576315566
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 6%

---


# Query persistenti GraphQL: abilitazione della memorizzazione nella cache in Dispatcher {#graphql-persisted-queries-enabling-caching-dispatcher}

>[!CAUTION]
>
>Se il caching in Dispatcher è abilitato, il [Filtro CORS](/help/headless/deployment/cross-origin-resource-sharing.md) non è necessario, e tale sezione può essere ignorata.

La memorizzazione nella cache delle query persistenti non è abilitata per impostazione predefinita in Dispatcher. L’abilitazione predefinita non è possibile perché i clienti che utilizzano CORS (Cross-Origin Resource Sharing) con più origini devono rivedere, e possibilmente aggiornare, la propria configurazione di Dispatcher.

>[!NOTE]
>
>Il Dispatcher non memorizza in cache `Vary` intestazione.
>
>La memorizzazione nella cache di altre intestazioni relative a CORS può essere abilitata in Dispatcher, ma potrebbe non essere sufficiente in presenza di più origini CORS.

>[!NOTE]
>
>Per la documentazione dettagliata sul Dispatcher, vedi [Guida di Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=it).

## Abilita la memorizzazione nella cache delle query persistenti {#enable-caching-persisted-queries}

Per abilitare la memorizzazione nella cache delle query persistenti, definisci la variabile di Dispatcher `CACHE_GRAPHQL_PERSISTED_QUERIES`:

1. Aggiungi la variabile al file di Dispatcher `global.vars`:

   ```xml
   Define CACHE_GRAPHQL_PERSISTED_QUERIES
   ```

>[!NOTE]
>
>Per adeguarsi al [Requisiti di Dispatcher per i documenti che possono essere memorizzati in cache](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/troubleshooting/dispatcher-faq.html#how-does-the-dispatcher-return-documents%3F), Dispatcher aggiunge il suffisso `.json` a tutti gli URL di query persistenti, in modo che il risultato possa essere memorizzato nella cache.
>
>Questo suffisso viene aggiunto da una regola di riscrittura, una volta abilitata la memorizzazione in cache delle query persistenti.

## Configurazione CORS in Dispatcher {#cors-configuration-in-dispatcher}

I clienti che utilizzano richieste CORS potrebbero dover rivedere e aggiornare la configurazione CORS in Dispatcher.

* Il `Origin` l’intestazione non deve essere passata a AEM publish tramite Dispatcher:
   * Controlla la `clientheaders.any` file.
* Al contrario, le richieste CORS devono essere valutate per le origini consentite a livello di Dispatcher. Questo approccio assicura inoltre che le intestazioni relative a CORS siano impostate correttamente, in un’unica posizione, in tutti i casi.
   * Tale configurazione deve essere aggiunta al `vhost` file. Di seguito è riportato un esempio di configurazione; per semplicità, è stata fornita solo la parte CORS. Puoi adattarlo ai tuoi casi d’uso specifici.

  ```xml
  <VirtualHost *:80>
     ServerName "publish"
  
     # ...
  
     <IfModule mod_headers.c>
         Header add X-Vhost "publish"
  
          ################## Start of the CORS specific configuration ##################
  
          SetEnvIfExpr "req_novary('Origin') == ''"  CORSType=none CORSProcessing=false
          SetEnvIfExpr "req_novary('Origin') != ''"  CORSType=cors CORSProcessing=true CORSTrusted=false
  
          SetEnvIfExpr "req_novary('Access-Control-Request-Method') == '' && %{REQUEST_METHOD} == 'OPTIONS' && req_novary('Origin') != ''  " CORSType=invalidpreflight CORSProcessing=false
          SetEnvIfExpr "req_novary('Access-Control-Request-Method') != '' && %{REQUEST_METHOD} == 'OPTIONS' && req_novary('Origin') != ''  " CORSType=preflight CORSProcessing=true CORSTrusted=false
          SetEnvIfExpr "req_novary('Origin') -strcmatch 'https://%{HTTP_HOST}*'"  CORSType=samedomain CORSProcessing=false
  
          # For requests that require CORS processing, check if the Origin can be trusted
          SetEnvIfExpr "%{HTTP_HOST} =~ /(.*)/ " ParsedHost=$1
  
          ################## Adapt the regex to match CORS origin for your environment
          SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*.your-domain.tld(:\d+)?$)#" CORSTrusted=true
  
          # Extract the Origin header 
          SetEnvIfNoCase ^Origin$ ^https://(.*)$ CORSTrustedOrigin=https://$1
  
          # Flush If already set
          Header unset Access-Control-Allow-Origin
          Header unset Access-Control-Allow-Credentials
  
          # Trusted
          Header always set Access-Control-Allow-Credentials "true" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Origin "%{CORSTrustedOrigin}e" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Methods "GET" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Max-Age 1800 "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Headers "Origin, Accept, X-Requested-With, Content-Type, Access-Control-Request-Method, Access-Control-Request-Headers" "expr=reqenv('CORSTrusted') == 'true'"
  
          # Non-CORS or Not Trusted
          Header unset Access-Control-Allow-Credentials "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Allow-Origin "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Allow-Methods "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Max-Age "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
  
          # Always vary on origin, even if its not there.
          Header merge Vary Origin
  
          # CORS - send 204 for CORS requests which are not trusted
          RewriteCond expr "reqenv('CORSProcessing') == 'true' && reqenv('CORSTrusted') == 'false'"
          RewriteRule "^(.*)" - [R=204,L]
  
          ################## End of the CORS specific configuration ##################
  
     </IfModule>
  
     <Directory />
  
         # ...
  
     </Directory>
  
     # ...
  
  </VirtualHost>
  ```
