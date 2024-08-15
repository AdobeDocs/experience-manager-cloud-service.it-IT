---
title: Navigazione al provider di servizi Screens
description: Questa pagina descrive come accedere a Screens Services Provider.
exl-id: 9eff6fe8-41d4-4cf3-b412-847850c4e09c
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 4%

---

# Navigazione al provider di servizi Screens {#setup-screens-services-provider}

## Introduzione {#introduction}

**Provider di servizi Screens**, consente all&#39;autore, agli sviluppatori e agli amministratori dei contenuti di gestire visualizzazioni e lettori per la riproduzione dei contenuti una volta aggiunti ai canali. Una volta ottenuto l’accesso ad AEM Cloud Service, gli utenti dovrebbero poter accedere al provider di servizi Screens.

In questa sezione viene descritto come configurare il provider di servizi Screens.


## Obiettivo {#objective}

Nella sezione seguente viene illustrato come configurare e configurare il provider di servizi Screens.

## Procedura per configurare il provider di servizi Screens {#screens-services-provider}

Per configurare il provider di servizi Screens, attenersi alla procedura descritta di seguito.

1. Passare a [Provider servizi Screens](https://experience.adobe.com/screens).

   >[!CAUTION]
   >Se hai accesso a più organizzazioni, assicurati di aver effettuato l’accesso a quella corretta. Per cambiare organizzazione, fai clic sul nome dell’organizzazione nell’angolo in alto a destra della schermata e scegli l’organizzazione a cui desideri accedere.

1. Fai clic sull’icona a forma di ingranaggio accanto a Progetto (angolo superiore sinistro)

   ![immagine](/help/screens-cloud/assets/configure/configure-screens0.png)

1. Immettete i dettagli riportati di seguito nella finestra di dialogo Modifica impostazioni.
   * **URL Publish** - URL di pubblicazione AEM (ad esempio, `https://publish-p12345-e12345.adobeaemcloud.com`)
   * **Url autore** - URL autore AEM (ad esempio, `https://author-p12345-e12345.adobeaemcloud.com`)

   >[!NOTE]
   >Assicurati di creare e pubblicare almeno un canale schermo AEM prima di configurare l’AEM in Screens Service Provider. Per creare un canale, passa a /screens.html sul provider di contenuti.

   ![immagine](/help/screens-cloud/assets/configure/configure-screens4.png)

1. Fai clic su **Salva** per connetterti al provider di contenuti Screens.

1. Se hai configurato l’istanza di pubblicazione dell’AEM in modo da consentire l’accesso solo a indirizzi IP attendibili tramite la funzione di Inserisce nell&#39;elenco Consentiti dei IP di Cloud Manager, devi configurare un’intestazione con un valore chiave nella finestra di dialogo delle impostazioni, come illustrato di seguito.
Anche gli IP che devono essere inseriti nella whitelist devono essere spostati nel file di configurazione e [non applicati](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list) dalle impostazioni di Cloud Manager.

   ![immagine](/help/screens-cloud/assets/configure/configure-screens20b.png)
La stessa chiave deve essere configurata nella configurazione CDN dell’AEM.  È consigliabile non inserire il valore dell&#39;intestazione direttamente in GITHub e utilizzare un [riferimento segreto](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-credentials-authentication#rotating-secrets).
Di seguito è riportato un esempio di configurazione [CDN](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/traffic-filter-rules-including-waf):

   ```kind: "CDN"
       version: "1"
       metadata:
         envTypes: ["dev", "stage", "prod"]
       data:
         trafficFilters:
           rules:
             - name: "block-request-from-not-allowed-ips"
               when:
                 allOf:
                   - reqProperty: clientIp
                     notIn: ["101.41.112.0/24"]
                    reqProperty: tier
                     equals: publish
               action: block
             - name: "allow-requests-with-header"
               when:
                 allOf:
                   - reqProperty: tier
                     equals: publish
                   - reqProperty: path
                     equals: /screens/channels.json
                   - reqHeader: x-screens-allowlist-key
                     equals: $\
       {CDN_HEADER_KEY}
               action:
                 type: allow
   ```

1. Seleziona **Canali** dalla barra di navigazione a sinistra e fai clic su **apri nel provider di contenuti**.

   ![immagine](/help/screens-cloud/assets/configure/configure-screens1.png)

1. Il provider di contenuti Screens si apre in un’altra scheda che consente di creare il contenuto.

   ![immagine](/help/screens-cloud/assets/configure/configure-screens2.png)





## Passaggio successivo {#whats-next}

Dopo aver appreso come configurare il provider di servizi Screens, passare a [Utilizzo del provider di contenuti Screens](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html#screens-content-provider) per ulteriori dettagli.
