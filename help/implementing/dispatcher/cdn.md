---
title: CDN in AEM as a Cloud Service
description: CDN in AEM as a Cloud Service
translation-type: tm+mt
source-git-commit: 50c5be6adf265eac9c9c7a7b36d03cb30ba4e5d2
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 4%

---


# CDN in AEM as a Cloud Service {#cdn}

AEM come Cloud Service viene fornito con un CDN incorporato. Il suo scopo principale è ridurre la latenza distribuendo contenuto memorizzabile nella cache dai nodi CDN ai margini, vicino al browser. È completamente gestita e configurata per garantire prestazioni ottimali alle applicazioni AEM.

La rete CDN gestita AEM soddisferà i requisiti di prestazioni e sicurezza della maggior parte dei clienti. Per il livello di pubblicazione, i clienti possono facoltativamente indicarlo dal proprio CDN, che dovranno gestire. Questo sarà consentito caso per caso, in base al soddisfacimento di alcuni prerequisiti, tra cui, ma non solo, il cliente che dispone di un&#39;integrazione legacy con il fornitore CDN difficile da abbandonare.

## CDN gestito AEM  {#aem-managed-cdn}

Per preparare la distribuzione dei contenuti, utilizzate  CDN  Adobe out-of-the-box:

1. Fornite il certificato SSL firmato e la chiave segreta per  Adobe condividendo un collegamento a un modulo protetto contenente queste informazioni. Coordinare con l&#39;assistenza clienti su questa attività.
   **Nota:** Aem come Cloud Service non supporta i certificati convalidati (DV) del dominio. Inoltre, deve essere un certificato TLS X.509 di un&#39;autorità di certificazione (CA) affidabile con una chiave privata RSA a 2048 bit corrispondente.
1. Informare l&#39;assistenza clienti:
   * quale dominio personalizzato deve essere associato a un determinato ambiente, come definito dall&#39;ID del programma e dall&#39;ID dell&#39;ambiente. I domini personalizzati dal lato dell&#39;autore non sono supportati.
   * se è necessaria un&#39;inserire nell&#39;elenco Consentiti IP  per limitare il traffico a un determinato ambiente.
1. Coordinare con l&#39;assistenza clienti la tempistica delle modifiche necessarie ai record DNS. Le istruzioni sono diverse a seconda che sia necessario un record apex:
   * se non è necessario un record apex, i clienti devono impostare il record DNS CNAME in modo che punti il loro FQDN a `cdn.adobeaemcloud.com`.
   * se è necessario un record apex, create un record A che indichi i seguenti IP: 151.101.3.10, 151.101.67.10, 151.101.131.10, 151.101.195.10. I clienti necessitano di un record apex se il nome FQDN desiderato corrisponde alla zona DNS. Questo può essere verificato utilizzando il comando Unix dig per verificare se il valore SOA dell&#39;output corrisponde al dominio. Ad esempio, il comando `dig anything.dev.adobeaemcloud.com` restituisce un SOA (Inizio dell&#39;Autorità, ovvero la zona) di `dev.adobeaemcloud.com` cui non è un record APEX, mentre `dig dev.adobeaemcloud.com` restituisce un SOA di `dev.adobeaemcloud.com` cui è un record apex.
1. Al momento della scadenza dei certificati SSL riceverete una notifica per consentirvi di inviare nuovamente i nuovi certificati SSL.

**Limitazione del traffico**

Per impostazione predefinita, per una configurazione CDN gestita da un Adobe , tutto il traffico pubblico può essere indirizzato al servizio di pubblicazione, sia per gli ambienti di produzione che per quelli non di produzione (sviluppo e fase). Se desiderate limitare il traffico al servizio di pubblicazione per un determinato ambiente (ad esempio, limitando l’area di gestione temporanea per un intervallo di indirizzi IP), per configurare tali restrizioni dovete rivolgervi all’assistenza clienti.

## CDN cliente punta a AEM CDN gestito {#point-to-point-CDN}

Se un cliente deve usare la propria CDN esistente, può gestirla e indicarla  Adobe  CDN gestito, purché siano soddisfatte le seguenti condizioni:

* Il cliente deve disporre di un CDN esistente che potrebbe essere oneroso da sostituire.
* Il cliente deve gestirlo.
* Il cliente deve essere in grado di configurare la CDN in modo che funzioni con AEM come Cloud Service. Consultate le istruzioni di configurazione riportate di seguito.
* Il cliente deve disporre di esperti CDN tecnici che siano in servizio in caso di problemi correlati.
* Il cliente deve eseguire e superare con successo un test di carico prima di andare in produzione.

Istruzioni di configurazione:

1. Impostate l’ `X-Forwarded-Host` intestazione con il nome del dominio.
1. Impostate l&#39;intestazione Host con il dominio di origine, che è  ingresso  CDN della Adobe. Il valore deve provenire  Adobe.
1. Inviate l’intestazione SNI all’origine. Come l&#39;intestazione Host, l&#39;intestazione sni deve essere il dominio di origine.
1. Impostare il `X-Edge-Key`, necessario per indirizzare correttamente il traffico ai server AEM. Il valore deve provenire  Adobe.

Prima di accettare il traffico live, è necessario verificare con  Adobe il corretto funzionamento del ciclo di traffico end-to-end.

È possibile che si verifichi un piccolo hit di prestazioni a causa del hop aggiuntivo, anche se è probabile che il passaggio dalla CDN del cliente a  CDN gestita  Adobe sia efficiente.

Questa configurazione CDN del cliente è supportata per il livello di pubblicazione, ma non davanti al livello di authoring.
