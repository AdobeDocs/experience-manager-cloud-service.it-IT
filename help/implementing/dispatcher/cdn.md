---
title: CDN in AEM as a Cloud Service
description: CDN in AEM as a Cloud Service
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
source-git-commit: cc9e305d96f1de55a8c3fa450aa41142bb0adfd1
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 8%

---

# CDN in AEM as a Cloud Service {#cdn}


>[!CONTEXTUALHELP]
>id="aemcloud_golive_cdn"
>title="CDN in AEM as a Cloud Service"
>abstract="AEM come Cloud Service viene fornito con una rete CDN integrata. Lo scopo principale è ridurre la latenza distribuendo contenuti memorizzabili nella cache dai nodi CDN al bordo, vicino al browser. È completamente gestita e configurata per garantire prestazioni ottimali alle applicazioni AEM."

AEM come Cloud Service viene fornito con una rete CDN integrata. Il suo scopo principale è ridurre la latenza distribuendo contenuti memorizzabili nella cache dai nodi della CDN al perimetro, vicino al browser. È completamente gestita e configurata per garantire prestazioni ottimali alle applicazioni AEM.

La rete CDN gestita AEM soddisferà i requisiti di prestazioni e sicurezza della maggior parte dei clienti. Per il livello di pubblicazione, i clienti possono facoltativamente indicarlo dal proprio CDN, che dovranno gestire. Questo sarà consentito caso per caso, in base al soddisfacimento di alcuni prerequisiti, tra cui, ma non solo, il cliente con un’integrazione legacy con il proprio fornitore CDN che è difficile abbandonare.

## CDN gestito AEM  {#aem-managed-cdn}

Segui le sezioni seguenti per utilizzare l’interfaccia utente self-service di Cloud Manager per prepararsi alla distribuzione dei contenuti utilizzando la rete CDN standard di AEM:

1. [Gestione dei certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [Gestione dei nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**Limitazione del traffico**

Per impostazione predefinita, per una configurazione AEM CDN gestita, tutto il traffico pubblico può indirizzarsi al servizio di pubblicazione, sia per gli ambienti di produzione che per quelli non di produzione (sviluppo e stage). Se desideri limitare il traffico al servizio di pubblicazione per un dato ambiente (ad esempio, limitando la gestione temporanea per un intervallo di indirizzi IP), puoi farlo in modalità self-service tramite l’interfaccia utente di Cloud Manager.

Fai riferimento a [Gestione degli Elenchi consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) per saperne di più.

>[!CAUTION]
>
>Solo le richieste dagli IP consentiti saranno servite dalla rete CDN gestita di AEM. Se punti la tua CDN alla CDN gestita AEM, assicurati che gli IP della tua CDN siano inclusi nell&#39;inserire nell&#39;elenco Consentiti.

## CDN cliente punta a AEM CDN gestito {#point-to-point-CDN}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_byocdn"
>title="CDN cliente punta a AEM CDN gestito"
>abstract="AEM come Cloud Service offre ai clienti un’opzione per utilizzare la propria rete CDN esistente. Per il livello di pubblicazione, i clienti possono facoltativamente indicarlo dal proprio CDN, che dovranno gestire. Questo sarà consentito caso per caso, in base al soddisfacimento di alcuni prerequisiti, tra cui, ma non solo, il cliente con un’integrazione legacy con il proprio fornitore CDN che è difficile abbandonare."

Se un cliente deve utilizzare il proprio CDN esistente, può gestirlo e indirizzarlo al CDN gestito AEM, purché siano soddisfatte le seguenti condizioni:

* Il cliente deve disporre di un CDN esistente che sarebbe oneroso da sostituire.
* Il cliente deve gestirlo.
* Il cliente deve essere in grado di configurare la CDN in modo che funzioni con AEM as a Cloud Service - vedi le istruzioni di configurazione riportate di seguito.
* Il cliente deve avere esperti CDN tecnici che sono in chiamata in caso di problemi correlati.
* Il cliente deve eseguire e superare con successo un test di carico prima di passare alla produzione.

Istruzioni di configurazione:

1. Posiziona il CDN nell’ingresso della CDN di Adobe come dominio di origine. Esempio, `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.
1. L&#39;SNI deve essere impostato anche sull&#39;ingresso della CDN dell&#39;Adobe
1. Imposta l’intestazione Host sul dominio di origine. Esempio: `Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.
1. Imposta la `X-Forwarded-Host` intestazione con il nome di dominio in modo AEM determinare l&#39;intestazione host. Esempio: `X-Forwarded-Host:example.com`.
1. Imposta `X-AEM-Edge-Key`. Il valore deve provenire dall&#39;Adobe.
   * Questo è necessario in modo che l’Adobe CDN possa convalidare l’origine delle richieste e passare il `X-Forwarded-*` le intestazioni dell&#39;applicazione AEM. Ad esempio:`X-Forwarded-For` viene utilizzato per determinare l&#39;IP client. Quindi, diventa responsabilità del chiamante affidabile (cioè il CDN gestito dal cliente) per garantire la correttezza del `X-Forwarded-*` intestazioni (vedi la nota qui sotto).
   * Facoltativamente, l&#39;accesso all&#39;ingresso della rete CDN di Adobe può essere bloccato quando un `X-AEM-Edge-Key` non è presente. Informa l&#39;Adobe se hai bisogno di accedere direttamente all&#39;ingresso della CDN Adobe (da bloccare).

Prima di accettare il traffico live, è necessario verificare con il supporto clienti di Adobe che il indirizzamento del traffico end-to-end funziona correttamente.

Dopo aver ottenuto `X-AEM-Edge-Key`, puoi verificare che la richiesta sia instradata correttamente come segue:

`https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -H 'X-Forwarded-Host: example.com' -H 'X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>'`

Tieni presente che quando utilizzi la tua CDN, non è necessario installare i domini e i certificati in Cloud Manager. Il routing in Adobe CDN verrà eseguito utilizzando il dominio predefinito `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.

>[!NOTE]
>
>I clienti che gestiscono il proprio CDN devono garantire l’integrità delle intestazioni inviate a AEM CDN. Ad esempio, si consiglia ai clienti di cancellare tutto `X-Forwarded-*` e impostale su valori noti e controllati. Ad esempio: `X-Forwarded-For` deve contenere l&#39;indirizzo IP del cliente, mentre `X-Forwarded-Host` deve contenere l&#39;host del sito.

>[!NOTE]
>
>Gli ambienti di programma sandbox non supportano una rete CDN fornita dal cliente.

C&#39;è potenzialmente un piccolo hit di prestazioni a causa dell&#39;hop aggiuntivo, anche se è probabile che i salti dalla CDN del cliente alla CDN gestita AEM siano efficienti.

Questa configurazione CDN del cliente è supportata per il livello di pubblicazione, ma non davanti al livello di authoring.

## Intestazioni di geolocalizzazione {#geo-headers}

La CDN gestita AEM aggiunge intestazioni a ogni richiesta con:

* codice del paese: `x-aem-client-country`
* Codice continente: `x-aem-client-continent`

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
