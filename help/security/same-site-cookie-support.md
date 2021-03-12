---
title: Supporto per cookie per lo stesso sito per Adobe Experience Manager come Cloud Service
description: Supporto per cookie di sito ISame per Adobe Experience Manager as a Cloud Service
translation-type: tm+mt
source-git-commit: 24f26a5cc77158ea20a09b1f40cf3d849a70591f
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---


# Supporto per lo stesso cookie di sito per Adobe Experience Manager come Cloud Service {#same-site-cookie-support-for-adobe-experience-manager-as-a-cloud-service}

A partire dalla versione 80, Chrome e versioni successive Safari, ha introdotto un nuovo modello per la sicurezza dei cookie. Questa modalità è progettata per introdurre controlli di sicurezza sulla disponibilità di cookie per siti di terze parti, tramite un’impostazione denominata `SameSite`. Per informazioni più dettagliate, consulta questo [articolo](https://web.dev/samesite-cookies-explained/).

Il valore predefinito di questa impostazione (`SameSite=Lax`) potrebbe causare il mancato funzionamento dell&#39;autenticazione tra istanze o servizi AEM. Questo perché i domini o le strutture URL di questi servizi potrebbero non rientrare nei vincoli di questo criterio dei cookie.

Per ovviare a questo problema, è necessario impostare l’attributo per cookie SameSite su `None` per il token di accesso.

Per farlo, segui i passaggi seguenti:

1. Installare localmente una versione dell’SDK Quickstart AEM
1. Vai alla console Web all&#39;indirizzo `http://serveraddress:serverport/system/console/configMgr`
1. Cerca e fai clic su **Adobe Granite Token Authentication Handler**
1. Imposta l&#39;attributo **SameSite per il cookie login-token** su `None`, come illustrato nell&#39;immagine seguente
   ![samesite](/help/security/assets/samesite1.png)
1. Fai clic su Salva
1. Genera le configurazioni del formato JSON per questa particolare impostazione seguendo i passaggi descritti in [Generazione di configurazioni OSGi tramite l&#39;SDK AEM Quickstart](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart)
1. Applica le impostazioni seguendo i passaggi descritti nella documentazione [Formato API Cloud Manager per l&#39;impostazione delle proprietà](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) OSGi .
