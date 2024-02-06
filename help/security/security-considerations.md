---
title: Considerazioni sulla sicurezza di AEM as a Cloud Service
description: Informazioni sulle considerazioni importanti relative alla sicurezza durante l’utilizzo di AEM as a Cloud Service
hidefromtoc: true
hide: true
exl-id: d2dfde05-ce02-478e-8697-b939fb8740c3
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: ht
source-wordcount: '217'
ht-degree: 100%

---

# Considerazioni sulla sicurezza di AEM as a Cloud Service {#security-considerations}

## TrustStore in AEM {#aem-trust-store}

Per supportare operazioni di crittografia asimmetriche, AEM memorizza i certificati all’interno dell’archivio dei contenuti in un TrustStore globale. I contenuti sono pubblici e, per impostazione predefinita, accessibili in modo anonimo da tutti gli utenti delle istanze degli editori.

### Caratteristiche del TrustStore {#truststore-characteristics}

* Il TrustStore si trova sotto `/etc/truststore` ed è costituito da un file Java KeyStore, dalla password dell’archivio chiavi e dai metadati dell’archivio. Sia la password che l’archivio chiavi sono crittografati per motivi tecnici, anche se i certificati contenuti sono accessibili a tutti per impostazione predefinita tramite l’API
* I certificati preconfigurati vengono utilizzati solo per il supporto HTTPS e SAML e l’archivio deve essere creato manualmente prima
* I clienti possono utilizzarlo nel proprio codice tramite l’[API dell’archivio chiavi](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/keystore/KeyStoreService.html#getTrustStore-org.apache.sling.api.resource.ResourceResolver-)
* Il TrustStore può essere gestito tramite l’interfaccia utente in **Strumenti** - **Sicurezza** - **TrustStore** o tramite l’accesso a *`https://serveraddress:serverport/libs/granite/security/content/truststore.html`*, come illustrato di seguito:

  ![Gestione del TrustStore](/help/security/assets/global-trust-store-modified.png)

* L’accesso al TrustStore può essere ulteriormente limitato dal controllo dell’accesso all’archivio, a seconda del caso d’uso.

>[!NOTE]
>
>Adobe consiglia di utilizzare i controlli di accesso predefiniti per il TrustStore, il che significa che rimane pubblicamente accessibile. Per ottenere la configurazione più sicura, puoi utilizzare un criterio di rifiuto jcr:all per tutti.

<!--
Commenting out section for now as requested by Lars

## Anonymous Permission Hardening Package {#anonymous-permission-hardening-package}

For more information on the Anonymous Hardening Package, see [Security Checklist](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html#anonymous-permission-hardening-package).
-->
