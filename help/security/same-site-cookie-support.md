---
title: Supporto per i cookie SameSite per Adobe Experience Manager as a Cloud Service
description: Supporto per i cookie dello stesso sito per Adobe Experience Manager as a Cloud Service.
exl-id: 2cec7202-4450-456f-8e62-b7ed3791505c
source-git-commit: 678e81eb22cc1d7c239ac7a2594b39a3a60c51e2
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 74%

---

# Supporto per i cookie SameSite per Adobe Experience Manager as a Cloud Service {#same-site-cookie-support-for-adobe-experience-manager-as-a-cloud-service}

A partire dalla versione 80, Chrome, e successivamente Safari, hanno introdotto un nuovo modello per la sicurezza dei cookie. Questa modalità è progettata per introdurre controlli di sicurezza riguardo alla disponibilità di cookie per i siti di terze parti, tramite un’impostazione denominata `SameSite`. Per informazioni più dettagliate, consulta questo [articolo](https://web.dev/articles/samesite-cookies-explained).

Il valore predefinito di questa impostazione (`SameSite=Lax`) potrebbe impedire il funzionamento dell’autenticazione tra istanze o servizi AEM. Questo perché i domini o le strutture URL di questi servizi potrebbero non rientrare nei vincoli di questo criterio dei cookie.

Per ovviare a questo problema, imposta l’attributo per cookie SameSite su `None` per il token di accesso.

>[!CAUTION]
>
>L’impostazione `SameSite=None` viene applicata solo se il protocollo è protetto (HTTPS).
>
>Se il protocollo non è protetto (HTTP), l&#39;impostazione viene ignorata e il server visualizza questo messaggio di avviso:
>
>`WARN com.day.crx.security.token.TokenCookie Skip 'SameSite=None'`

Per aggiungere l’impostazione, segui questi passaggi:

1. Installa localmente una versione QuickStart per SDK AEM
1. Passa alla console Web all’indirizzo `http://serveraddress:serverport/system/console/configMgr`
1. Cerca e fai clic sull’**handler di autenticazione token di Adobe Granite**
1. Imposta **l’attributo SameSite per il cookie token di accesso** su `None`, come illustrato nell’immagine seguente
   ![samesite](/help/security/assets/samesite1.png)
1. Fai clic su Salva
1. Genera le configurazioni del formato JSON per questa particolare impostazione seguendo i passaggi descritti in [Generazione di configurazioni OSGi tramite QuickStart per SDK AEM](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart)
1. Applica le impostazioni seguendo i passaggi descritti nella sezione relativa al [formato API di Cloud Manager per l’impostazione delle proprietà](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) della documentazione di OSGi.

Dopo l&#39;aggiornamento di questa impostazione e la disconnessione e la riconnessione degli utenti, `login-token` i cookie hanno `None` set di attributi ed è incluso nelle richieste cross-site.
