---
title: CDN in AEM as a Cloud Service
description: CDN in AEM come Cloud Service
translation-type: tm+mt
source-git-commit: 852a4742a17065b9d38bd78d1e68a92854001842
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 5%

---


# CDN in AEM as a Cloud Service {#cdn}

AEM come Cloud Service viene fornito con un CDN incorporato. Il suo scopo principale è ridurre la latenza distribuendo contenuto memorizzabile nella cache dai nodi CDN ai margini, vicino al browser. È completamente gestita e configurata per garantire prestazioni ottimali alle applicazioni AEM.

La rete CDN gestita AEM soddisferà i requisiti di prestazioni e sicurezza della maggior parte dei clienti. Per il livello di pubblicazione, i clienti possono facoltativamente indicarlo dal proprio CDN, che dovranno gestire. Questo sarà consentito caso per caso, in base al soddisfacimento di alcuni prerequisiti, tra cui, ma non solo, il cliente che dispone di un&#39;integrazione legacy con il fornitore CDN difficile da abbandonare.

## AEM CDN gestito {#aem-managed-cdn}

Seguite le sezioni seguenti per utilizzare l’interfaccia utente self-service di Cloud Manager per prepararsi alla distribuzione dei contenuti utilizzando la rete CDN standard di AEM:

1. [Gestione dei certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [Gestione dei nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**Limitazione del traffico**

Per impostazione predefinita, per una configurazione AEM CDN gestita, tutto il traffico pubblico può essere indirizzato al servizio di pubblicazione, sia per gli ambienti di produzione che per quelli non di produzione (sviluppo e fase). Se desiderate limitare il traffico al servizio di pubblicazione per un determinato ambiente (ad esempio, limitando l’area di gestione temporanea di un intervallo di indirizzi IP) potete farlo in modo autonomo tramite l’interfaccia utente di Cloud Manager.

Per ulteriori informazioni, fare riferimento a [Gestione dei Elenchi consentiti di  IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

>[!CAUTION]
>
>Solo le richieste dagli IP consentiti verranno servite dalla rete CDN gestita di AEM. Se punti la tua CDN alla AEM CDN gestita, accertati che gli IP della CDN siano inclusi nel inserire nell&#39;elenco Consentiti di .

## CDN cliente punta a AEM CDN gestito {#point-to-point-CDN}

Se un cliente deve usare la propria CDN esistente, può gestirla e indicarla alla CDN gestita AEM, purché siano soddisfatte le seguenti condizioni:

* Il cliente deve disporre di un CDN esistente che potrebbe essere oneroso da sostituire.
* Il cliente deve gestirlo.
* Il cliente deve essere in grado di configurare la CDN in modo che funzioni con AEM come Cloud Service. Consultate le istruzioni di configurazione riportate di seguito.
* Il cliente deve disporre di esperti CDN tecnici che siano in servizio in caso di problemi correlati.
* Il cliente deve eseguire e superare con successo un test di carico prima di andare in produzione.

Istruzioni di configurazione:

1. Impostate l&#39;intestazione `X-Forwarded-Host` con il nome del dominio.
1. Impostate l&#39;intestazione Host con il dominio di origine, che è l&#39;ingresso AEM CDN. Il valore deve provenire  Adobe.
1. Inviate l’intestazione SNI all’origine. Come l&#39;intestazione Host, l&#39;intestazione sni deve essere il dominio di origine.
1. Impostare la `X-Edge-Key` o la `X-AEM-Edge-Key` (se la rete CDN elimina X-Edge-*), necessaria per indirizzare correttamente il traffico ai server AEM. Il valore deve provenire  Adobe. Informare  Adobe se si desidera accedere direttamente all&#39;ingresso  CDN del Adobe (da bloccare quando `X-Edge-Key` non è presente).

Prima di accettare il traffico live, è necessario verificare con  Adobe il corretto funzionamento del ciclo di traffico end-to-end.

È possibile che si verifichi un piccolo hit di prestazioni a causa del hop aggiuntivo, anche se è probabile che il passaggio dalla CDN cliente alla CDN gestita AEM sia efficiente.

Questa configurazione CDN del cliente è supportata per il livello di pubblicazione, ma non davanti al livello di authoring.

## Intestazioni di geolocalizzazione {#geo-headers}

AEM CDN gestito aggiungerà intestazioni a ogni richiesta con:

* codice del paese: `x-aem-client-country`
* Codice continente: `x-aem-client-continent`

I valori per i codici paese sono i codici alfa-2 descritti [here](https://en.wikipedia.org/wiki/ISO_3166-1).

I valori per i codici continente sono:

* AF Africa
* AN Antarctica
* AS Asia
* Europa
* NA America del Nord
* OC Oceania
* SA Sud America

Queste informazioni possono essere utili per casi di utilizzo, ad esempio per reindirizzare un URL diverso in base all’origine (paese) della richiesta. Utilizzate l&#39;intestazione Vary per memorizzare nella cache le risposte che dipendono dalle informazioni geografiche. Ad esempio, i reindirizzamenti a una specifica pagina di destinazione del paese devono sempre contenere `Vary: x-aem-client-country`. Se necessario, è possibile utilizzare `Cache-Control: private` per impedire il caching. Vedere anche [Caching](/help/implementing/dispatcher/caching.md#html-text).
