---
title: CDN in AEM as a Cloud Service
description: CDN in AEM come Cloud Service
translation-type: tm+mt
source-git-commit: 6c9a0779cfb9c3c2088a17e67437c76b589276f0
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 4%

---


# CDN in AEM as a Cloud Service {#cdn}

AEM come Cloud Service viene fornito con una rete CDN integrata. Lo scopo principale è ridurre la latenza distribuendo contenuti memorizzabili nella cache dai nodi CDN al bordo, vicino al browser. È completamente gestita e configurata per garantire prestazioni ottimali alle applicazioni AEM.

La rete CDN gestita AEM soddisferà i requisiti di prestazioni e sicurezza della maggior parte dei clienti. Per il livello di pubblicazione, i clienti possono facoltativamente indicarlo dal proprio CDN, che dovranno gestire. Questo sarà consentito caso per caso, in base al soddisfacimento di alcuni prerequisiti, tra cui, ma non solo, il cliente con un’integrazione legacy con il proprio fornitore CDN che è difficile abbandonare.

## CDN gestito AEM {#aem-managed-cdn}

Segui le sezioni seguenti per utilizzare l’interfaccia utente self-service di Cloud Manager per prepararsi alla distribuzione dei contenuti utilizzando la rete CDN standard di AEM:

1. [Gestione dei certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [Gestione dei nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**Limitazione del traffico**

Per impostazione predefinita, per una configurazione AEM CDN gestita, tutto il traffico pubblico può indirizzarsi al servizio di pubblicazione, sia per gli ambienti di produzione che per quelli non di produzione (sviluppo e stage). Se desideri limitare il traffico al servizio di pubblicazione per un dato ambiente (ad esempio, limitando la gestione temporanea per un intervallo di indirizzi IP), puoi farlo in modalità self-service tramite l’interfaccia utente di Cloud Manager.

Per ulteriori informazioni, consulta [Gestione degli Elenchi consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) .

>[!CAUTION]
>
>Solo le richieste dagli IP consentiti saranno servite dalla rete CDN gestita di AEM. Se punti la tua CDN alla AEM CDN gestita, assicurati che gli IP della tua CDN siano inclusi nell&#39;inserire nell&#39;elenco Consentiti.

## CDN del cliente punta a AEM CDN gestito {#point-to-point-CDN}

Se un cliente deve utilizzare il proprio CDN esistente, può gestirlo e indirizzarlo al CDN gestito AEM, purché siano soddisfatte le seguenti condizioni:

* Il cliente deve disporre di un CDN esistente che sarebbe oneroso da sostituire.
* Il cliente deve gestirlo.
* Il cliente deve essere in grado di configurare la rete CDN in modo che funzioni con AEM come Cloud Service - vedi le istruzioni di configurazione riportate di seguito.
* Il cliente deve avere esperti CDN tecnici che sono in chiamata in caso di problemi correlati.
* Il cliente deve eseguire e superare con successo un test di carico prima di passare alla produzione.

Istruzioni di configurazione:

1. Imposta l&#39;intestazione `X-Forwarded-Host` con il nome di dominio.
1. Imposta l’intestazione Host con il dominio di origine, che è l’ingresso della CDN AEM. Il valore deve provenire dall&#39;Adobe.
1. Invia l’intestazione SNI all’origine. Come l’intestazione Host , l’intestazione sni deve essere il dominio di origine.
1. Imposta il `X-Edge-Key` o il `X-AEM-Edge-Key` (se il CDN elimina X-Edge-*), necessario per indirizzare correttamente il traffico ai server AEM. Il valore deve provenire dall&#39;Adobe. Informare l&#39;Adobe se si desidera l&#39;accesso diretto all&#39;ingresso della rete CDN di Adobe (da bloccare quando `X-Edge-Key` non è presente).

Prima di accettare il traffico in tempo reale, è necessario verificare con l’Adobe del supporto clienti che l’indirizzamento del traffico end-to-end funziona correttamente.

>[!NOTE]
>
>I clienti che gestiscono il proprio CDN devono garantire l’integrità delle intestazioni inviate a AEM CDN. Ad esempio, si consiglia ai clienti di cancellare tutte le intestazioni `X-Forwarded-*` e impostarle su valori noti e controllati. Ad esempio, `X-Forwarded-For` deve contenere l&#39;indirizzo IP del client, mentre `X-Forwarded-Host` deve contenere l&#39;host del sito.

C&#39;è potenzialmente un piccolo hit di prestazioni a causa dell&#39;hop aggiuntivo, anche se è probabile che i salti dalla CDN del cliente alla CDN gestita AEM siano efficienti.

Questa configurazione CDN del cliente è supportata per il livello di pubblicazione, ma non davanti al livello di authoring.

## Intestazioni di geolocalizzazione {#geo-headers}

La CDN gestita AEM aggiungerà intestazioni a ogni richiesta con:

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

Queste informazioni possono essere utili per i casi d’uso, ad esempio per reindirizzare a un URL diverso in base all’origine (paese) della richiesta. Utilizza l’intestazione Vary per memorizzare nella cache le risposte che dipendono dalle informazioni geografiche. Ad esempio, i reindirizzamenti a una pagina di destinazione specifica di un paese devono sempre contenere `Vary: x-aem-client-country`. Se necessario, è possibile utilizzare `Cache-Control: private` per impedire la memorizzazione in cache. Vedere anche [Memorizzazione in cache](/help/implementing/dispatcher/caching.md#html-text).
