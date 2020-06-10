---
title: CDN in AEM come servizio cloud
description: CDN in AEM come servizio cloud
translation-type: tm+mt
source-git-commit: 9d99a7513a3a912b37ceff327e58a962cc17c627
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 2%

---


# CDN in AEM come servizio cloud {#cdn}

AEM as Cloud Service viene fornito con un CDN integrato. Il suo scopo principale è ridurre la latenza distribuendo contenuto memorizzabile nella cache dai nodi CDN ai margini, vicino al browser. È completamente gestita e configurata per garantire prestazioni ottimali alle applicazioni AEM.

In totale, AEM offre due opzioni:

1. CDN gestito AEM - CDN out-of-the-box di AEM. Si tratta di un’opzione strettamente integrata e non richiede ingenti investimenti da parte dei clienti per supportare l’integrazione CDN con AEM.
1. La CDN gestita dal cliente punta alla CDN gestita da AEM - il cliente punta il proprio CDN alla CDN out-of-the-box di AEM. Il cliente dovrà comunque gestire il proprio CDN, ma gli investimenti nell’integrazione con AEM sono modesti.

La prima opzione deve soddisfare la maggior parte dei requisiti di prestazioni e sicurezza del cliente. Inoltre, richiede il minimo sforzo da parte dei clienti.

La seconda opzione è consentita caso per caso. La decisione si basa sul soddisfacimento di alcuni prerequisiti, tra cui, a titolo esemplificativo, l’integrazione con il fornitore CDN di un cliente precedente, difficilmente abbandonabile.

Presentato di seguito è una matrice decisionale per confrontare le due opzioni. Ulteriori informazioni sono disponibili nelle sezioni che seguono.

| Dettagli | CDN gestito AEM | CDN gestito dal cliente indicherà AEM CDN |
|---|---|---|
| **Sforzo dei clienti** | Nessuno, è completamente integrato. Dovete solo puntare CNAME alla CDN gestita AEM. | Investimenti moderati da parte dei clienti. Il cliente deve gestire il proprio CDN. |
| **Prerequisiti** | Nessuno | CDN esistente da sostituire. Deve dimostrare l&#39;esito positivo del test di carico prima di iniziare a vivere. |
| **Competenze CDN** | Nessuno | Richiede almeno una risorsa di progettazione part-time con conoscenze CDN dettagliate in grado di configurare il CDN del cliente. |
| **Sicurezza** | Gestito da Adobe. | Gestito da Adobe (e facoltativamente dal cliente con una propria CDN). |
| **Spettacolo** | Ottimizzato da Adobe. | Potrà beneficiare di alcune funzionalità CDN di AEM, ma potrebbe verificarsi un piccolo hit di prestazioni a causa del hop aggiuntivo. **Nota**: È probabile che i punti di assistenza dalla CDN del cliente alla CDN out-of-the-box di Adobe siano efficienti). |
| **Caching** | Supporta le intestazioni della cache applicate al dispatcher. | Supporta le intestazioni della cache applicate al dispatcher. |
| **Funzionalità di compressione immagini e video** | Può essere utilizzato con Adobe Dynamic Media. | Può essere utilizzato con Adobe Dynamic Media o con una soluzione CDN gestita dai clienti. |

## CDN gestito AEM  {#aem-managed-cdn}

Per preparare la distribuzione dei contenuti, utilizzate la rete CDN standard di Adobe:

1. Fornirai ad Adobe il certificato SSL firmato e la chiave segreta condividendo un collegamento a un modulo protetto contenente tali informazioni. Coordinare con l&#39;assistenza clienti su questa attività.
   **Nota:** Aem come servizio Cloud non supporta i certificati convalidati (DV) del dominio.
1. È necessario informare l&#39;assistenza clienti:
   * quale dominio personalizzato deve essere associato a un determinato ambiente, come definito dall&#39;ID del programma e dall&#39;ID dell&#39;ambiente. I domini personalizzati dal lato dell&#39;autore non sono supportati.
   * se è necessaria una whitelist IP per limitare il traffico a un determinato ambiente.
1. È necessario coordinare con il supporto clienti la tempistica delle modifiche necessarie ai record DNS. Le istruzioni sono diverse a seconda che sia necessario un record apex:
   * se non è necessario un record apex, i clienti devono impostare il record DNS CNAME in modo che punti il loro FQDN a `cdn.adobeaemcloud.com`.
   * se è necessario un record apex, create un record A che indichi i seguenti IP: 151.101.3.10, 151.101.67.10, 151.101.131.10, 151.101.195.10. I clienti necessitano di un record apex se il nome FQDN desiderato corrisponde alla zona DNS. Questo può essere verificato utilizzando il comando Unix dig per verificare se il valore SOA dell&#39;output corrisponde al dominio. Ad esempio, il comando `dig anything.dev.adobeaemcloud.com` restituisce un SOA (Inizio dell&#39;Autorità, ovvero la zona) di `dev.adobeaemcloud.com` cui non è un record APEX, mentre `dig dev.adobeaemcloud.com` restituisce un SOA di `dev.adobeaemcloud.com` cui è un record apex.
1. Al momento della scadenza dei certificati SSL riceverete una notifica per consentirvi di inviare nuovamente i nuovi certificati SSL.

**Limitazione del traffico**

Per impostazione predefinita, per una configurazione CDN gestita da Adobe, tutto il traffico pubblico può essere indirizzato al servizio di pubblicazione, sia per gli ambienti di produzione che per quelli non di produzione (sviluppo e fase). Se desiderate limitare il traffico al servizio di pubblicazione per un determinato ambiente (ad esempio, limitando l’area di gestione temporanea per un intervallo di indirizzi IP), per configurare tali restrizioni dovete rivolgervi all’assistenza clienti.

## CDN cliente punta a CDN gestito AEM {#point-to-point-CDN}

Supportato se desiderate utilizzare il vostro CDN esistente, ma non potete soddisfare i requisiti di un CDN gestito dal cliente. In questo caso, gestite la vostra rete CDN, ma indicate la rete CDN gestita da Adobe.

Attenzione:

1. È necessario disporre di un CDN esistente.
1. Deve gestirla.
1. È necessario essere in grado di configurare la CDN in modo che funzioni con Aem come servizio cloud. Consultate le istruzioni di configurazione riportate di seguito.
1. È necessario disporre di esperti CDN tecnici in fase di chiamata in caso di problemi correlati.
1. È necessario eseguire e superare con successo un test di carico prima di passare alla produzione.

Istruzioni di configurazione:

1. Impostate l’ `X-Forwarded-Host` intestazione con il nome del dominio.
1. Impostate l&#39;intestazione Host con il dominio di origine, che è l&#39;ingresso CDN di Adobe. Il valore deve provenire da Adobe.
1. Inviate l’intestazione SNI all’origine. Come l&#39;intestazione Host, l&#39;intestazione sni deve essere il dominio di origine.
1. Impostate il `X-Edge-Key`, necessario per indirizzare correttamente il traffico ai server AEM. Il valore deve provenire da Adobe.

Prima di accettare il traffico live, è necessario verificare con l&#39;assistenza clienti Adobe che il ciclo di traffico end-to-end funziona correttamente.
