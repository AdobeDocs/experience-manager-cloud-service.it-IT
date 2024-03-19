---
title: CDN in AEM as a Cloud Service
description: Scopri come utilizzare la rete CDN gestita dall’AEM e come indirizzare la tua rete CDN alla rete CDN gestita dall’AEM.
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
source-git-commit: 43fdf17ab09fd7a974c32cfd716f65072b678726
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 23%

---

# CDN in AEM as a Cloud Service {#cdn}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_cdn"
>title="CDN in AEM as a Cloud Service"
>abstract="AEM as a Cloud Service viene fornito con una rete CDN integrata. Il suo scopo principale è ridurre la latenza distribuendo contenuti memorizzabili nella cache dai nodi della CDN al perimetro, vicino al browser. È completamente gestita e configurata per garantire prestazioni ottimali alle applicazioni AEM."

AEM as a Cloud Service viene fornito con una rete CDN integrata. Il suo scopo principale è ridurre la latenza distribuendo contenuti memorizzabili nella cache dai nodi della CDN al perimetro, vicino al browser. È completamente gestita e configurata per garantire prestazioni ottimali alle applicazioni AEM.

La rete CDN gestita dall&#39;AEM soddisfa i requisiti di prestazioni e sicurezza della maggior parte dei clienti. Per il livello di pubblicazione, i clienti possono facoltativamente puntare a essa dalla propria CDN, che dovranno gestire. Questo scenario viene consentito caso per caso, in base al rispetto di alcuni prerequisiti, come ad esempio la presenza di un’eventuale integrazione precedente del cliente presso il proprio fornitore di CDN che sia difficile da abbandonare.

<!-- ERROR: NEITHER URL IS FOUND (HTTP ERROR 404) Also, see the following videos [Cloud 5 AEM CDN Part 1](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part1.html) and [Cloud 5 AEM CDN Part 2](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part2.html) for additional information about CDN in AEM as a Cloud Service. -->

## CDN gestita da AEM  {#aem-managed-cdn}

Segui le sezioni riportate di seguito per utilizzare l’interfaccia utente self-service di Cloud Manager in preparazione alla distribuzione dei contenuti tramite CDN preconfigurata AEM:

1. [Gestione dei certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [Gestione dei nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**Limitazione del traffico**

Per impostazione predefinita, per una configurazione CDN gestita dall’AEM tutto il traffico pubblico può indirizzarsi al servizio di pubblicazione, sia per gli ambienti di produzione che per quelli non di produzione (sviluppo e stage). Puoi limitare il traffico verso il servizio di pubblicazione per un dato ambiente (ad esempio, limitando la gestione temporanea da un intervallo di indirizzi IP) tramite l’interfaccia utente di Cloud Manager.

Per ulteriori informazioni, vedi [Gestione degli elenchi IP consentiti](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

>[!CAUTION]
>
>Solo le richieste provenienti dagli IP consentiti vengono gestite da CDN gestita dall’AEM. Se punti la tua rete CDN alla rete CDN gestita dall’AEM, assicurati che gli IP della tua rete CDN siano inclusi nel inserisco nell&#39;elenco Consentiti di.

### Configurazione del traffico sulla rete CDN {#cdn-configuring-cloud}

Le regole per configurare il traffico e i filtri CDN possono essere dichiarate in un file di configurazione e distribuite nella CDN utilizzando [Pipeline di configurazione di Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline). Per ulteriori dettagli, consulta [Configurazione del traffico sulla rete CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md) e [Regole del filtro del traffico, incluse le regole WAF](/help/security/traffic-filter-rules-including-waf.md).

### Configurazione delle pagine di errore CDN {#cdn-error-pages}

È possibile configurare una pagina di errore CDN per ignorare la pagina predefinita senza marchio trasmessa al browser nel raro caso in cui non sia possibile raggiungere l’AEM. Per ulteriori dettagli, consulta [Configurazione delle pagine di errore CDN](/help/implementing/dispatcher/cdn-error-pages.md).

## La CDN del cliente punta alla CDN gestita dall’AEM {#point-to-point-CDN}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_byocdn"
>title="CDN del cliente punta alla CDN gestita di AEM"
>abstract="AEM as a Cloud Service offre ai clienti un’opzione per utilizzare la sua rete CDN esistente. Per il livello di pubblicazione, i clienti possono facoltativamente puntare a essa dalla propria CDN, che dovranno gestire. Questo scenario viene consentito caso per caso, in base al rispetto di alcuni prerequisiti, come ad esempio la presenza di un’eventuale integrazione precedente del cliente presso il proprio fornitore di CDN che sia difficile da abbandonare."

Se un cliente deve utilizzare la propria rete CDN esistente, può gestirla e puntarla alla rete CDN gestita dall’AEM, purché siano soddisfatte le seguenti condizioni:

* Il cliente deve disporre di una rete CDN esistente che potrebbe essere onerosa da sostituire.
* Il cliente deve gestirlo.
* Il cliente deve essere in grado di configurare la rete CDN in modo che funzioni con AEM as a Cloud Service; consulta le istruzioni di configurazione riportate di seguito.
* Il cliente deve disporre di esperti CDN tecnici che siano di guardia in caso di problemi correlati.
* Il cliente deve eseguire e superare con successo un test di carico prima di passare alla produzione.

Istruzioni di configurazione:

1. Puntare la CDN all’ingresso della CDN Adobe come dominio di origine. Esempio: `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.
1. Impostare SNI sull&#39;ingresso della rete CDN in Adobe.
1. Imposta l’intestazione Host sul dominio di origine. Ad esempio: `Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.
1. Imposta il `X-Forwarded-Host` con il nome di dominio in modo che l’AEM possa determinare l’intestazione dell’host. Ad esempio: `X-Forwarded-Host:example.com`.
1. Imposta `X-AEM-Edge-Key`. Il valore deve provenire da Adobe.

   * Necessario affinché il CDN Adobe possa convalidare l’origine delle richieste e trasmettere `X-Forwarded-*` intestazioni per l’applicazione AEM. Ad esempio:`X-Forwarded-For` viene utilizzato per determinare l’IP del client. Pertanto, è responsabilità del chiamante fidato (ovvero, la rete CDN gestita dal cliente) garantire la correttezza del `X-Forwarded-*` intestazioni (vedi la nota seguente).
   * Facoltativamente, l’accesso alla rete CDN Adobe può essere bloccato quando un utente `X-AEM-Edge-Key` non è presente. Informa l’Adobe se hai bisogno di accedere direttamente all’ingresso della rete CDN di Adobe (da bloccare).

Consulta la [Esempio di configurazioni fornitore CDN](#sample-configurations) sezione per esempi di configurazione dei principali fornitori CDN.

Prima di accettare il traffico in tempo reale, è necessario verificare con l’Assistenza clienti di Adobe che il routing del traffico end-to-end funzioni correttamente.

Dopo aver ottenuto il `X-AEM-Edge-Key`, puoi verificare che la richiesta sia indirizzata correttamente come segue.

In Linux®:

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -H "X-Forwarded-Host: example.com" -H "X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>"
```

In Windows:

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com --header "X-Forwarded-Host: example.com" --header "X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>"
```

>[!NOTE]
>
>Quando utilizzi una tua rete CDN, non è necessario installare domini e certificati in Cloud Manager. Il routing nella rete CDN Adobe viene eseguito utilizzando il dominio predefinito `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com` da inviare nella richiesta `Host` intestazione. Sovrascrittura della richiesta `Host` Se l’intestazione presenta un nome di dominio personalizzato, la richiesta potrebbe essere instradata in modo errato dal CDN Adobe.


>[!NOTE]
>
>I clienti che gestiscono la propria rete CDN devono garantire l’integrità delle intestazioni inviate tramite la rete CDN dell’AEM. Ad esempio, si consiglia ai clienti di cancellare tutto `X-Forwarded-*` e impostarle su valori noti e controllati. Ad esempio: `X-Forwarded-For` deve contenere l’indirizzo IP del client, mentre `X-Forwarded-Host` deve contenere l’host del sito.

>[!NOTE]
>
>Gli ambienti dei programmi sandbox non supportano una rete CDN fornita dal cliente.

L’hop aggiuntivo tra la rete CDN del cliente e la rete CDN dell’AEM è necessario solo in caso di errore della cache. Utilizzando le strategie di ottimizzazione della cache descritte in questo articolo, l’aggiunta di una rete CDN del cliente dovrebbe introdurre solo una latenza trascurabile.

Questa configurazione CDN del cliente è supportata per il livello di pubblicazione, ma non prima del livello di authoring.

### Esempio di configurazioni fornitore CDN {#sample-configurations}

Di seguito sono riportati diversi esempi di configurazione di diversi fornitori CDN leader.

**Akamai**

![Akamai1](assets/akamai1.png "Akamai")
![Akamai2](assets/akamai2.png "Akamai")

**Amazon CloudFront**

![CloudFront1](assets/cloudfront1.png "Amazon CloudFront")
![CloudFront2](assets/cloudfront2.png "Amazon CloudFront")

**Nuvola**

![Cloudflare1](assets/cloudflare1.png "Nuvola")
![Cloudflare2](assets/cloudflare2.png "Nuvola")

## Intestazioni di geolocalizzazione {#geo-headers}

Il CDN gestito da AEM aggiunge intestazioni a ogni richiesta con:

* codice paese: `x-aem-client-country`
* Codice continente: `x-aem-client-continent`

>[!NOTE]
>
>Se è presente una rete CDN gestita dal cliente, queste intestazioni riflettono la posizione del server proxy CDN del cliente anziché il client effettivo. Pertanto, per la rete CDN gestita dal cliente, le intestazioni di geolocalizzazione devono essere gestite dalla rete CDN del cliente.

I valori per i codici dei paesi sono i codici Alpha-2 descritti [qui](https://en.wikipedia.org/wiki/ISO_3166-1).

I valori per i codici continente sono:

* AF Africa
* AN Antartide
* AS Asia
* Europa UE
* NA Nord America
* OC Oceania
* SA Sud America

Queste informazioni possono essere utili per casi d’uso come il reindirizzamento a un URL diverso in base all’origine (paese) della richiesta. Utilizza l’intestazione Vary per memorizzare nella cache le risposte che dipendono dalle informazioni geografiche. Ad esempio, i reindirizzamenti a una pagina di destinazione di un paese specifico devono sempre contenere `Vary: x-aem-client-country`. Se necessario, puoi utilizzare `Cache-Control: private` per impedire il caching. Vedi anche [Memorizzazione in cache](/help/implementing/dispatcher/caching.md#html-text).
