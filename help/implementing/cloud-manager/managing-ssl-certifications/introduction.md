---
title: Introduzione alla gestione dei certificati SSL
description: Scopri come Cloud Manager offre gli strumenti self-service per installare i certificati SSL.
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
source-git-commit: 898f7bc46a3f1b0ac93ee43fbf7b60a11682a073
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 1%

---


# Introduzione alla gestione dei certificati SSL{#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="Gestire i certificati SSL"
>abstract="Scopri come Cloud Manager offre strumenti self-service per installare e gestire i certificati SSL al fine di proteggere il sito per i tuoi utenti. Cloud Manager utilizza un servizio Platform TLS per gestire i certificati SSL e le chiavi private di proprietà dei clienti e ottenuti da autorità di certificazione di terze parti."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates.html" text="Visualizzare, aggiornare e sostituire un certificato SSL"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates.html" text="Controllare lo stato di un certificato SSL"

Cloud Manager offre strumenti self-service per installare e gestire i certificati SSL al fine di proteggere il sito per gli utenti. Cloud Manager utilizza un servizio Platform TLS per gestire i certificati SSL e le chiavi private di proprietà dei clienti e ottenuti da autorità di certificazione di terze parti, come Let’s Encrypt.

## Introduzione ai certificati {#certificates}

Le aziende utilizzano i certificati SSL per proteggere i propri siti web e consentire ai propri clienti di fidarsi di loro. Per utilizzare il protocollo SSL, un server web richiede l’utilizzo di un certificato SSL.

Quando un’entità richiede un certificato da un’autorità di certificazione, la CA completa un processo di verifica. Questo può variare dalla verifica del controllo dei nomi di dominio alla raccolta dei documenti di registrazione della società e degli accordi di sottoscrizione. Una volta verificate le informazioni di un&#39;entità, la CA firmerà la propria chiave pubblica utilizzando la chiave privata della CA. Poiché tutte le principali autorità di certificazione dispongono di certificati radice nei browser Web, il certificato dell’entità verrà collegato tramite un *catena di affidabilità* e il browser web lo riconoscerà come certificato attendibile.

>[!IMPORTANT]
>
>Cloud Manager non fornisce certificati SSL o chiavi private. Questi devono essere ottenuti presso le autorità di certificazione (CA).

## Funzioni di gestione SSL di Cloud Manager {#features}

Cloud Manager supporta le seguenti opzioni di utilizzo del certificato SSL del cliente.

* Un certificato SSL può essere utilizzato da più ambienti. Ad esempio, può essere aggiunto una volta e utilizzato più volte.
* Ogni ambiente Cloud Manager può utilizzare più certificati.
* Una chiave privata può emettere più certificati SSL.
* In genere, ogni certificato contiene più domini.
* Il servizio Platform TLS indirizza le richieste al servizio CDN del cliente in base al certificato SSL utilizzato per terminare e al servizio CDN che ospita tale dominio.
* AEM as a Cloud Service accetta certificati SSL con caratteri jolly per un dominio.

## Consigli {#recommendations}

AEM as a Cloud Service supporta solo la protezione `https` siti.

* I clienti con più domini personalizzati non dovranno caricare un certificato ogni volta che aggiungono un dominio.
* Tali clienti trarranno vantaggio ottenendo un certificato con più domini.

## Requisiti {#requirements}

* AEM as a Cloud Service accetterà solo i certificati conformi ai criteri OV (Organization Validation) o EV (Extended Validation).
* Qualsiasi certificato deve essere un certificato TLS X.509 di un’autorità di certificazione (CA) attendibile con una chiave privata RSA a 2048 bit corrispondente.
* Criterio di convalida del dominio DV non accettato.
* I certificati autofirmati non sono accettati.

I certificati OV ed EV forniscono agli utenti informazioni aggiuntive convalidate da CA che possono essere utilizzate per stabilire se il proprietario di un sito web, il mittente di un&#39;e-mail o il firmatario digitale di un codice eseguibile o di documenti PDF è affidabile. I certificati DV non consentono tale verifica della proprietà.

## Limitazioni  {#limitations}

In qualsiasi momento, Cloud Manager consentirà l’installazione di un massimo di 50 certificati SSL. Questi possono essere associati a uno o più ambienti nel programma e includere anche eventuali certificati scaduti.

Se hai raggiunto il limite, rivedi i certificati e prendi in considerazione:

* Eliminazione di eventuali certificati scaduti.
* Raggruppamento di più domini nello stesso certificato in quanto un certificato può coprire più domini (fino a 100 SAN).

## Ulteriori informazioni {#learn-more}

Un utente con le autorizzazioni necessarie può utilizzare Cloud Manager per gestire i certificati SSL per un programma. Per ulteriori informazioni sull’utilizzo di queste funzioni, consulta i seguenti documenti.

* [Aggiunta di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [Visualizzazione, aggiornamento o sostituzione di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
* [Eliminazione di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
