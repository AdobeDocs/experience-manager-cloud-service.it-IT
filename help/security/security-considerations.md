---
title: Considerazioni AEM sulla sicurezza as a Cloud Service
description: Scopri importanti considerazioni sulla sicurezza quando utilizzi AEM as a Cloud Service
hidefromtoc: true
hide: true
source-git-commit: 39ffd826f5d1e9cea2e6a03a74f39c16647b45fa
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Considerazioni AEM sulla sicurezza as a Cloud Service {#security-considerations}

## AEM Trust Store {#aem-trust-store}

Per supportare operazioni di crittografia asimmetriche, AEM memorizza i certificati all’interno dell’archivio dei contenuti in un trust-store globale. I contenuti sono pubblici e, per impostazione predefinita, sono accessibili in modo anonimo da tutti gli utenti delle istanze degli editori.

### Caratteristiche del Trust Store {#truststore-characteristics}

* Il trust-store si trova qui sotto `/etc/truststore` è costituito da un file keystore Java, la password del keystore e i metadati del repository. Tieni presente che sia la password che l’archivio chiavi sono crittografati per motivi tecnici, anche se i certificati contenuti sono accessibili a tutti per impostazione predefinita tramite l’API
* I certificati vengono utilizzati solo per il supporto HTTPS e SAML e l’archivio deve essere creato manualmente per primo
* I clienti possono utilizzarli nel proprio codice tramite [API keystore](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/keystore/KeyStoreService.html#getTrustStore-org.apache.sling.api.resource.ResourceResolver-)
* L’archivio dati attendibili può essere gestito tramite l’interfaccia utente di **Strumenti** - **Sicurezza** - **Archiviazione attendibile** o tramite l&#39;accesso *`https://serveraddress:serverport/libs/granite/security/content/truststore.html`*, come illustrato di seguito:

   ![Gestione dell&#39;archivio fonti attendibili](/help/security/assets/global-trust-store-modified.png)

* L&#39;accesso all&#39;archivio dati attendibili può essere ulteriormente limitato dal controllo dell&#39;accesso all&#39;archivio, a seconda del caso d&#39;uso.

>[!NOTE]
>
>L&#39;Adobe consiglia di utilizzare i controlli di accesso predefiniti per l&#39;archivio fonti attendibili, il che significa che l&#39;accesso rimane accessibile al pubblico. Per la configurazione più sicura, puoi utilizzare un criterio di negazione jcr:all per tutti.

<!--
Commenting out section for now as requested by Lars

## Anonymous Permission Hardening Package {#anonymous-permission-hardening-package}

For more information on the Anonymous Hardening Package, please see the [Security Checklist](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html#anonymous-permission-hardening-package).
-->
