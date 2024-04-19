---
title: Configurare il dominio personalizzato per il livello di pubblicazione
description: Scopri come configurare il dominio personalizzato per il livello di pubblicazione in Adobe Cloud Manager.
role: null
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 1%

---


# Configurare il dominio personalizzato per il livello di pubblicazione{#configure-custom-domain}

In Adobe Cloud Manager, puoi dare risalto al tuo sito web aggiungendo un dominio personalizzato. Se AEM as a Cloud Service viene fornito con un dominio predefinito, puoi personalizzarlo in base alle tue esigenze.
<!-- For example, AEM sites can use `sites.custom_domain.com`, and the AEM publish domain can be accessed via `assets.custom_domain.com`. Additionally, getting an SSL certificate for assets.pmi.com with a SAN entry for `delivery.custom_domain.com` improves security and trustworthiness. -->

## Prima di iniziare

* È necessario disporre di un certificato TLS o SSL multi-SAN (Subject Alternative Name).
* Il certificato SSL deve avere SAN distinte rispetto al certificato mappato per il livello di pubblicazione all’interno dello stesso dominio.
* I criteri di certificato devono essere conformi ai criteri di convalida estesa (EV) o di convalida organizzazione (OV) e non ai criteri di convalida del dominio (DV).


## Aggiungi dominio personalizzato

Per configurare un dominio personalizzato per il livello di pubblicazione, effettua le seguenti operazioni:

1. Vai a **[!UICONTROL Adobe Cloud Manager]** > **[!UICONTROL Panoramica del programma]** > **[!UICONTROL Certificati SSL]**e aggiungi il certificato SSL.
   ![immagine](/help/assets/assets/ssl-certificate.png)
Scopri come aggiungere [Certificato SSL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate.html?lang=en) in Adobe Cloud Manager.

1. Dopo aver aggiunto il certificato SSL, aggiungi un dominio personalizzato. Clic **[!UICONTROL Impostazioni dominio]** e specifica il dominio personalizzato rispetto al **[!UICONTROL Servizio di pubblicazione]** opzione.
   <br> Ulteriori informazioni su [dominio personalizzato](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name.html?lang=en).

1. Aggiungi 2 record CNAME nel record DNS corrispondenti ai domini di pubblicazione.
   <br> L’elaborazione della verifica DNS può richiedere alcune ore a causa dei ritardi di propagazione DNS.

1. Segnala un caso di supporto per facilitare la configurazione del dominio personalizzato, garantendo che venga indirizzato al livello di consegna.

>[!NOTE]
>
> Assicurati di aggiungere il dominio personalizzato all’elenco degli URL di reindirizzamento consentiti nel client IMS per il selettore risorse.<br>Coordinati con il rispettivo team di Adobi per eseguire questa attività fornendo la stringa di dominio personalizzata.
