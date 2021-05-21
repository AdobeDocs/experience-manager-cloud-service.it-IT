---
title: Introduzione - Gestione dei certificati SSL
description: Introduzione - Gestione dei certificati SSL
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
source-git-commit: 8e09031d1cf17bda9d4eb379f84462b2d29e1aa5
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Introduzione {#introduction}

Cloud Manager offre ai clienti la funzionalità self-service per installare i certificati SSL tramite l’interfaccia utente di Cloud Manager. Cloud Manager utilizza un servizio Platform TLS per gestire i certificati SSL e le chiavi private di proprietà dei clienti e generalmente ottenuti da autorità di certificazione di terze parti, ad esempio *Cifra*.

## Considerazioni importanti {#important-considerations}

* Cloud Manager non fornisce certificati SSL o chiavi private. Tali informazioni devono essere ottenute presso autorità di certificazione di terzi. Per ulteriori informazioni, consulta [Ottenere un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md) .

* AEM come Cloud Service supporta solo siti `https` sicuri. I clienti con più domini personalizzati non dovranno caricare un certificato ogni volta che aggiungono un dominio. Pertanto, tali clienti trarranno vantaggio ottenendo un certificato con più domini.

* AEM come Cloud Service accetterà solo i certificati OV (Organization Validation) o EV (Extended Validation). I certificati DV (Convalida del dominio) non verranno accettati. Inoltre, qualsiasi certificato deve essere un certificato TLS X.509 di un’autorità di certificazione (CA) affidabile con una chiave privata RSA a 2048 bit corrispondente.

* AEM come Cloud Service accetterà i certificati SSL con caratteri jolly per un dominio.

Cloud Manager supporta i seguenti requisiti di certificato SSL del cliente:

* Un certificato SSL può essere utilizzato da più ambienti, ovvero aggiungi una volta e utilizza più volte.
* Ogni ambiente Cloud Manager può utilizzare più certificati.
* Una chiave privata può emettere più certificati SSL.
* In genere, ogni certificato contiene più domini.
* Il servizio Platform TLS indirizza le richieste al servizio CDN del cliente in base al certificato SSL utilizzato per terminare e al servizio CDN che ospita tale dominio.

Utilizzando la pagina Certificati SSL dell’interfaccia utente di Cloud Manager, un utente con autorizzazioni può eseguire diverse attività per gestire i certificati SSL per un programma:

* [Aggiunta di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [Visualizzazione, aggiornamento o sostituzione di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/view-update-replace-ssl-certificate.md)
   >[!NOTE]
   >Queste azioni ti consentono di visualizzare i dettagli o sostituire un certificato che sta per scadere.
* [Eliminazione di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/delete-ssl-certificate.md)
