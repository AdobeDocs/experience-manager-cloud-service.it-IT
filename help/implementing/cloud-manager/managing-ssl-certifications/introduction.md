---
title: Introduzione - Gestione dei certificati SSL
description: Introduzione - Gestione dei certificati SSL
translation-type: tm+mt
source-git-commit: 99eb33c3c42094f787d853871aee3a3607856316
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# Introduzione {#introduction}

Cloud Manager offre ai clienti la possibilità di installare i certificati SSL tramite l&#39;interfaccia utente di Cloud Manager. Cloud Manager utilizza un servizio Platform TLS per gestire i certificati SSL e le chiavi private di proprietà dei clienti, solitamente ottenuti da autorità di certificazione di terze parti, ad esempio, Cifra.

## Considerazioni importanti {#important-considerations}


* Cloud Manager non fornisce certificati SSL o chiavi private. Questi devono essere ottenuti da autorità di certificazione di terzi. Per ulteriori informazioni, fare riferimento a [Ottenimento di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md).

* AEM come Cloud Service supporta solo siti `https` sicuri. I clienti con più domini personalizzati non desiderano caricare un certificato ogni volta che aggiungono un dominio. Di conseguenza, tali clienti trarranno vantaggio ottenendo un certificato con più domini.

Cloud Manager supporta i seguenti requisiti di certificato SSL del cliente:

* Un certificato SSL può essere utilizzato da più ambienti, ovvero può essere aggiunto una volta e utilizzato più volte.
* Ogni ambiente Cloud Manager può utilizzare più certificati.
* Una chiave privata può emettere più certificati SSL.
* Ogni certificato contiene in genere più domini.
* Il servizio Platform TLS indirizza le richieste al servizio CDN del cliente in base al certificato SSL utilizzato per terminare e al servizio CDN che ospita tale dominio.

Utilizzando la pagina Certificati SSL dell&#39;interfaccia utente di Cloud Manager, un utente con autorizzazioni può eseguire diverse attività per gestire i certificati SSL per un programma:

* [Aggiunta di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [Visualizzazione, aggiornamento o sostituzione di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/view-update-replace-ssl-certificate.md)
   >[!NOTE]
   >Queste azioni consentono di visualizzare i dettagli o sostituire un certificato che sta per scadere.
* [Eliminazione di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/delete-ssl-certificate.md)