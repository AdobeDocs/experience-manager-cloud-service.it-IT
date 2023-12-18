---
title: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione di manutenzione corrente di [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: db0f60537a65c426dae88b5440622c9034c736e2
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 32%

---

# Note sulla versione di manutenzione {#maintenance-release-notes}

La sezione seguente illustra le note di rilascio tecnico per la versione di manutenzione corrente di Experience Manager as a Cloud Service.

## Versione 14697 {#release-14697}

Di seguito sono riepilogati i miglioramenti continui relativi alla versione di manutenzione 14697, rilasciata pubblicamente l’martedì 18 dicembre 2023. Sostituisce i 14538 di rilascio che avevano un problema. La versione di manutenzione precedente era 14227.

2023.12.0 Feature Activation fornisce il set completo di funzioni per questa versione di manutenzione. Per ulteriori informazioni, consulta la [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it).

### Miglioramenti {#enhancements-14697}

* GRANITE-46723: User Sync - Migrazione SAML dalla sincronizzazione predefinita alla sincronizzazione basata su IDP.
* OAK-10311: replica: ottimizzazione del confronto dei BLOB per ridurre il tempo di replica di grandi batch di risorse in AEM.
* OAK-10511: replica: riduzione dei round-trip in rete per ridurre i tempi di replica di risorse di grandi dimensioni in AEM.
* GRANITE-48334: Publishers - Script di raccolta mancante per RUM.

### Problemi risolti {#fixed-issues-14697}

* CQ-4354867: il riferimento a ToggleCondition fa riferimento a un campo inesistente in InstanceActionServlet.
* CQ-4349948: localizzazione delle stringhe &quot;Profile Properties&quot; (Proprietà profilo) in Modifica impostazioni utente nella sezione Strumenti → Sicurezza → utenti.
* GRANITE-44541: localizzazione delle finestre di dialogo di errore sull’aggiunta della schermata File di chiave privata di Modifica utente > Registro chiavi in Strumenti → Sicurezza → utenti.
* GRANITE-45341: localizzazione delle stringhe di esito positivo/negativo per attivare/disattivare l’azione dell’utente in Strumenti → Sicurezza → Utenti.
* GRANITE-46650: localizzazione del messaggio di errore &quot;Mancata corrispondenza ID utente/password&quot;. string (Stringa) in Strumenti → Sicurezza → Finestra di dialogo per creazione utenti.
* GRANITE-47764: aggiornamento a Sling Models API 1.5.0: l’inserimento di una variabile statica in un modello Sling causerà errori di compilazione (SLING-11507).
* GRANITE-48452: invio di clientlibs vuote con codice di stato 200.
* GRANITE-48410: ResourceResolver non è chiuso.
* ASSETS-31297: impedisce l’eliminazione della risorsa copiata da elementi multimediali dinamici.
* ASSETS-30811: Aggiornamenti di riferimento per Blocktag Service associato.
* GRANITE-46418: Aggiornare gli eventi Sling in AEM: GaugeSupport ha una ricorsione infinita in registerWithSuffix (SLING-11918).

### Problemi noti {#known-issues-14697}

Nessuno.

### Tecnologie incorporate {#embedded-tech-14697}

| Tecnologia | Versione | Collegamento |
|---|---|---|
| AEM OAK | 1,58-T20231123092841-619e1bd | [API Oak 1.58.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.58.0/index.html) |
| API SLING AEM | Versione 2.27.2 | [API Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versione 1.4.20-1.4.0 | [Specifiche HTML Template Language](https://github.com/adobe/htl-spec) |
| Componenti core AEM | Versione 2.23.4 | [Componenti core WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
