---
title: CDN in AEM as a Cloud Service
description: CDN in AEM as a Cloud Service
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 15%

---

# CDN in AEM as a Cloud Service {#cdn}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_cdn"
>title="CDN in AEM as a Cloud Service"
>abstract="AEM as a Cloud Service viene fornito con una rete CDN integrata. Il suo scopo principale è ridurre la latenza distribuendo contenuti memorizzabili nella cache dai nodi della CDN al perimetro, vicino al browser. È completamente gestita e configurata per garantire prestazioni ottimali alle applicazioni AEM."

AEM as a Cloud Service viene fornito con una rete CDN integrata. Il suo scopo principale è ridurre la latenza distribuendo contenuti memorizzabili nella cache dai nodi della CDN al perimetro, vicino al browser. È completamente gestita e configurata per garantire prestazioni ottimali alle applicazioni AEM.

La rete CDN gestita AEM soddisfa la maggior parte dei requisiti di prestazioni e sicurezza dei clienti. Per il livello di pubblicazione, i clienti possono facoltativamente indicarlo dal proprio CDN, che devono gestire. Questo scenario è consentito caso per caso, in base al soddisfacimento di alcuni prerequisiti, tra cui, ma non solo, il cliente con un’integrazione legacy con il proprio fornitore CDN che è difficile abbandonare.

<!-- ERROR: NEITHER URL IS FOUND (HTTP ERROR 404) Also, see the following videos [Cloud 5 AEM CDN Part 1](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part1.html) and [Cloud 5 AEM CDN Part 2](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part2.html) for additional information about CDN in AEM as a Cloud Service. -->

## CDN gestito da AEM  {#aem-managed-cdn}

Segui le sezioni seguenti per utilizzare l’interfaccia utente self-service di Cloud Manager per prepararsi alla distribuzione dei contenuti utilizzando AEM CDN preconfigurato:

1. [Gestione dei certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [Gestione dei nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**Limitazione del traffico**

Per impostazione predefinita, per una configurazione CDN gestita da AEM, tutto il traffico pubblico può indirizzarsi al servizio di pubblicazione, sia per gli ambienti di produzione che per quelli non di produzione (sviluppo e stage). Puoi limitare il traffico al servizio di pubblicazione per un dato ambiente (ad esempio, limitando la gestione temporanea per un intervallo di indirizzi IP) tramite l’interfaccia utente di Cloud Manager.

Per ulteriori informazioni, consulta [Gestione degli elenchi IP consentiti](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

>[!CAUTION]
>
>Solo le richieste dagli IP consentiti vengono servite da AEM CDN gestito. Se punti la tua CDN alla CDN gestita da AEM, assicurati che gli IP della tua CDN siano inclusi nell&#39;inserire nell&#39;elenco Consentiti.

## CDN del cliente punta a CDN gestito da AEM {#point-to-point-CDN}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_byocdn"
>title="CDN del cliente punta alla CDN gestita di AEM"
>abstract="AEM as a Cloud Service offre ai clienti un’opzione per utilizzare la sua rete CDN esistente. Per il livello di pubblicazione, i clienti possono facoltativamente indicarlo dal proprio CDN, che devono gestire. Questo scenario è consentito caso per caso, in base al soddisfacimento di alcuni prerequisiti, tra cui, ma non solo, il cliente con un’integrazione legacy con il proprio fornitore CDN che è difficile abbandonare."

Se un cliente deve utilizzare il proprio CDN esistente, può gestirlo e indirizzarlo al CDN gestito da AEM, purché siano soddisfatte le seguenti condizioni:

* Il cliente deve disporre di un CDN esistente che sarebbe oneroso da sostituire.
* Il cliente deve gestirlo.
* Il cliente deve essere in grado di configurare la CDN in modo che funzioni con AEM as a Cloud Service - vedi le istruzioni di configurazione riportate di seguito.
* Il cliente deve avere esperti CDN tecnici che sono in chiamata in caso di problemi relativi al caso si presentano.
* Il cliente deve eseguire e superare con successo un test di carico prima di passare alla produzione.

Istruzioni di configurazione:

1. Posiziona il CDN nell’ingresso della CDN di Adobe come dominio di origine. Esempio: `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.
1. Impostare SNI sull&#39;ingresso della CDN di Adobe.
1. Imposta l’intestazione Host sul dominio di origine. Esempio: `Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.
1. Imposta la `X-Forwarded-Host` intestazione con il nome di dominio in modo AEM determinare l&#39;intestazione host. Esempio: `X-Forwarded-Host:example.com`.
1. Imposta `X-AEM-Edge-Key`. Il valore deve provenire dall&#39;Adobe.

   * Necessario in modo che l’Adobe CDN possa convalidare l’origine delle richieste e passare il `X-Forwarded-*` le intestazioni dell&#39;applicazione AEM. Ad esempio:`X-Forwarded-For` viene utilizzato per determinare l&#39;IP client. Quindi, diventa responsabilità del chiamante affidabile (cioè, il CDN gestito dal cliente) per garantire la correttezza del `X-Forwarded-*` intestazioni (vedi la nota qui sotto).
   * Facoltativamente, l&#39;accesso all&#39;ingresso della rete CDN di Adobe può essere bloccato quando un `X-AEM-Edge-Key` non è presente. Informare l&#39;Adobe se hai bisogno dell&#39;accesso diretto all&#39;ingresso della rete CDN di Adobe (da bloccare).

Consulta la sezione [Configurazioni fornitore CDN di esempio](#sample-configurations) sezione per esempi di configurazione da parte dei principali fornitori CDN.

Prima di accettare il traffico live, è necessario verificare con il supporto clienti di Adobe che il indirizzamento del traffico end-to-end funziona correttamente.

Dopo aver ottenuto `X-AEM-Edge-Key`, puoi verificare che la richiesta sia instradata correttamente come segue.

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
>Quando utilizzi una tua CDN, non devi installare domini e certificati in Cloud Manager. Il routing nella rete CDN di Adobe viene eseguito utilizzando il dominio predefinito `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com` da inviare nella richiesta `Host` intestazione. Sovrascrittura della richiesta `Host` intestazione con un nome di dominio personalizzato può causare l’instradamento errato della richiesta da parte della CDN di Adobe.


>[!NOTE]
>
>I clienti che gestiscono il proprio CDN devono garantire l’integrità delle intestazioni inviate a AEM CDN. Ad esempio, si consiglia ai clienti di cancellare tutto `X-Forwarded-*` e impostale su valori noti e controllati. Ad esempio: `X-Forwarded-For` deve contenere l&#39;indirizzo IP del cliente, mentre `X-Forwarded-Host` deve contenere l&#39;host del sito.

>[!NOTE]
>
>Gli ambienti di programma sandbox non supportano una rete CDN fornita dal cliente.

L’hop aggiuntivo tra la CDN del cliente e la CDN AEM è necessario solo in presenza di una perdita di cache. Utilizzando le strategie di ottimizzazione della cache descritte in questo articolo, l’aggiunta di un CDN cliente dovrebbe introdurre solo una latenza trascurabile.

Questa configurazione CDN del cliente è supportata per il livello di pubblicazione, ma non davanti al livello di authoring.

### Configurazioni fornitore CDN di esempio {#sample-configurations}

Di seguito sono riportati diversi esempi di configurazione forniti da diversi importanti fornitori CDN.

**Akamai**

![Akamai1](assets/akamai1.png "Akamai")
![Akamai2](assets/akamai2.png "Akamai")

**Amazon CloudFront**

![CloudFront1](assets/cloudfront1.png "Amazon CloudFront")
![CloudFront2](assets/cloudfront2.png "Amazon CloudFront")

**Cloudflare**

![Cloudflare1](assets/cloudflare1.png "Cloudflare")
![Cloudflare2](assets/cloudflare2.png "Cloudflare")

## Intestazioni di geolocalizzazione {#geo-headers}

La rete CDN gestita AEM aggiunge intestazioni a ogni richiesta con:

* codice del paese: `x-aem-client-country`
* Codice continente: `x-aem-client-continent`

>[!NOTE]
>
>Se è presente una rete CDN gestita dal cliente, queste intestazioni riflettono la posizione del server proxy CDN dei clienti anziché il client effettivo. Pertanto, per la CDN gestita dal cliente, le intestazioni di geolocalizzazione devono essere gestite dalla CDN dei clienti.

I valori per i codici paese sono i codici alfa-2 descritti [qui](https://en.wikipedia.org/wiki/ISO_3166-1).

I valori per i codici continente sono:

* AF Africa
* AN Antartide
* AS Asia
* Europa
* NA America del Nord
* OC Oceania
* SA Sud America

Queste informazioni possono essere utili per i casi d’uso, ad esempio per reindirizzare a un URL diverso in base all’origine (paese) della richiesta. Utilizza l’intestazione Vary per memorizzare nella cache le risposte che dipendono dalle informazioni geografiche. Ad esempio, i reindirizzamenti a una pagina di destinazione specifica di un paese devono sempre contenere `Vary: x-aem-client-country`. Se necessario, puoi utilizzare `Cache-Control: private` per evitare la memorizzazione in cache. Vedi anche [Memorizzazione in cache](/help/implementing/dispatcher/caching.md#html-text).
