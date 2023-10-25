---
title: Introduzione alla gestione dei certificati SSL
description: Scopri gli strumenti self-service offerti da Cloud Manager per l’installazione dei certificati SSL.
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 100%

---


# Introduzione alla gestione dei certificati SSL{#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="Gestione dei certificati SSL"
>abstract="Scopri gli strumenti self-service di Cloud Manager per l’installazione e la gestione dei certificati SSL al fine di proteggere il sito per gli utenti. Cloud Manager si avvale di un servizio di piattaforma TLS per gestire i certificati SSL e le chiavi private di proprietà dei clienti ottenuti da autorità di certificazione terze."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates.html?lang=it" text="Visualizzazione, aggiornamento e sostituzione di un certificato SSL"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates.html?lang=it" text="Controllo dello stato di un certificato SSL"

Cloud Manager offre strumenti self-service per installare e gestire i certificati SSL al fine di proteggere il sito per l’utenza. Cloud Manager si avvale di un servizio di piattaforma TLS per gestire i certificati SSL e le chiavi private di proprietà della clientela ottenuti da autorità di certificazione terze come Let’s Encrypt.

## Introduzione ai certificati {#certificates}

Le aziende utilizzano i certificati SSL per proteggere i siti web e guadagnare la fiducia della clientela. Per utilizzare il protocollo SSL, un server web richiede l’utilizzo di un certificato SSL.

Quando un’entità richiede un certificato da un’autorità di certificazione, quest’ultima svolge un processo di verifica. Tale processo può includere la verifica del controllo dei nomi di dominio e la raccolta dei documenti di registrazione dell’azienda e degli accordi di sottoscrizione. Dopo aver verificato le informazioni di un’entità, l’autorità di certificazione firma la chiave pubblica mediante la propria chiave privata. Poiché tutte le principali autorità di certificazione dispongono di certificati radice nei browser web, il certificato dell’entità verrà collegato tramite una *catena di affidabilità* e verrà riconosciuto dal browser web come attendibile.

>[!IMPORTANT]
>
>Cloud Manager non fornisce certificati SSL o chiavi private. Devono essere ottenuti dalle autorità di certificazione (CA).

## Funzioni di gestione SSL di Cloud Manager {#features}

Cloud Manager supporta le seguenti opzioni di utilizzo dei certificati SSL personalizzati del cliente.

* Un certificato SSL può essere utilizzato da più ambienti. Questo significa che può essere aggiunto e utilizzato più volte.
* Ogni ambiente di Cloud Manager può utilizzare più certificati.
* Una chiave privata può emettere più certificati SSL.
* In genere, ogni certificato contiene più domini.
* Il servizio di piattaforma TLS indirizza le richieste al servizio CDN del cliente in base al certificato SSL utilizzato per terminare l’operazione e al servizio CDN che ospita tale dominio.
* Per i domini, AEM as a Cloud Service accetta certificati SSL con caratteri jolly.

## Consigli {#recommendations}

AEM as a Cloud Service supporta solo siti `https` sicuri.

* I clienti con più domini personalizzati non devono caricare un certificato ogni volta che aggiungono un dominio.
* Per questi clienti è vantaggioso disporre di un solo certificato con più domini.

## Requisiti {#requirements}

* AEM as a Cloud Service accetta solo i certificati conformi ai criteri OV (convalida organizzazione) o EV (convalida estesa).
* Tutti i certificati devono essere TLS X.509 e provenire da un’autorità di certificazione (CA) attendibile con corrispondente chiave privata RSA a 2048 bit.
* Il criterio DV (convalida dominio) non è accettato.
* I certificati autofirmati non sono accettati.

I certificati OV ed EV forniscono agli utenti informazioni aggiuntive convalidate dall’autorità di certificazione che possono essere utilizzate per stabilire se il proprietario di un sito web, il mittente di un’e-mail o il firmatario digitale di un codice eseguibile o di documenti PDF è affidabile. I certificati DV non consentono tale verifica della proprietà.

## Limitazioni {#limitations}

In qualsiasi momento, Cloud Manager consente l’installazione di un massimo di 50 certificati SSL. Possono essere associati a uno o più ambienti nel programma e includere anche eventuali certificati scaduti.

Se hai raggiunto il limite, rivedi i certificati e considera se:

* Eliminare eventuali certificati scaduti.
* Raggruppare più domini nello stesso certificato, poiché un certificato può coprire più domini (fino a 100 SAN).

## Ulteriori informazioni {#learn-more}

Un utente con le autorizzazioni necessarie può utilizzare Cloud Manager per gestire i certificati SSL di un programma. Per ulteriori informazioni sull’utilizzo di queste funzioni, consulta i seguenti documenti.

* [Aggiunta di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [Visualizzazione, aggiornamento o sostituzione di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
* [Eliminazione di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
