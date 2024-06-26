---
title: Configurare il dominio personalizzato per il livello di pubblicazione
description: Scopri come configurare il dominio personalizzato per il livello di pubblicazione in Adobe Cloud Manager.
source-git-commit: f6c0e8e5c1d7391011ccad5aa2bad4a6ab7d10c3
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 6%

---


# Configurare il dominio personalizzato per il livello di pubblicazione{#configure-custom-domain}

In Adobe Cloud Manager, puoi dare risalto al tuo sito web aggiungendo un dominio personalizzato. Se AEM as a Cloud Service viene fornito con un dominio predefinito, puoi personalizzarlo in base alle tue esigenze.

## Prima di iniziare

* È necessario disporre di un certificato TLS o SSL multi-SAN (Subject Alternative Name).
* Il certificato SSL deve avere SAN distinte rispetto al certificato mappato per il livello di pubblicazione all’interno dello stesso dominio.
* I criteri di certificato devono essere conformi ai criteri di convalida estesa (EV) o di convalida organizzazione (OV) e non ai criteri di convalida del dominio (DV).


## Aggiungi dominio personalizzato

Per configurare un dominio personalizzato per il livello di pubblicazione, effettua le seguenti operazioni:

1. Vai a **[!UICONTROL Adobe Cloud Manager]** > **[!UICONTROL Panoramica del programma]** > **[!UICONTROL Certificati SSL]**e aggiungi il certificato SSL.
   ![immagine](/help/assets/assets/ssl-certificate.png)
Scopri come aggiungere [Certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) in Adobe Cloud Manager.

1. Dopo aver aggiunto il certificato SSL, aggiungi un dominio personalizzato. Clic **[!UICONTROL Impostazioni dominio]** e specifica il dominio personalizzato rispetto al **[!UICONTROL servizio Publish]** opzione.
Ulteriori informazioni su [dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

1. Aggiungi 2 [Record CNAME](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) nel record DNS corrispondente ai domini di pubblicazione.
L’elaborazione della verifica DNS può richiedere alcune ore per via dei ritardi di propagazione del DNS.

1. Segnala un caso di supporto per facilitare la configurazione del dominio personalizzato, garantendo che venga indirizzato al livello di consegna.

>[!NOTE]
>
> Assicurati di aggiungere il dominio personalizzato all’elenco degli URL di reindirizzamento consentiti nel client IMS per il selettore risorse.<br>Coordinati con il rispettivo team di Adobi per eseguire questa attività fornendo la stringa di dominio personalizzata.
