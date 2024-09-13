---
title: Introduzione ai certificati SSL
description: Scopri gli strumenti self-service offerti da Cloud Manager per l’installazione dei certificati SSL.
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: d2f05915c0bf0af073db7f070b83f13aeae55252
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 33%

---


# Introduzione ai certificati SSL{#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="Gestire i certificati SSL"
>abstract="Scopri gli strumenti self-service di Cloud Manager per l’installazione e la gestione dei certificati SSL al fine di proteggere il sito per gli utenti. Cloud Manager si avvale di un servizio di piattaforma TLS per gestire i certificati SSL e le chiavi private di proprietà dei clienti ottenuti da autorità di certificazione terze."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="Visualizzazione, aggiornamento e sostituzione di un certificato SSL"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="Controllo dello stato di un certificato SSL"


Cloud Manager offre strumenti self-service per installare e gestire i certificati SSL (Secure Socket Layer), garantendo la sicurezza del sito per gli utenti. Sono supportati i due casi d’uso seguenti:

<!-- CQDOC-21758, #1 -->

| | Caso d’uso | Descrizione |
| --- | --- | --- |
| 1 | **Adobe certificato gestito (DV)** | Cloud Manager consente agli utenti di configurare un certificato DV (Domain Validation) proveniente da Adobe per la configurazione rapida del dominio. I certificati DV rappresentano il livello di base della certificazione SSL e vengono spesso utilizzati per scopi di test o per proteggere i siti Web con crittografia di base. I certificati DV sono disponibili sia nei [programmi di produzione che nei programmi sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md). Dopo la creazione del certificato DV, Adobe lo rinnova automaticamente ogni tre mesi, a meno che non venga eliminato. |
| 2 | **Certificato gestito dal cliente (OV/EV)** | Cloud Manager utilizza un servizio di piattaforma TLS (Transport Layer Security) per gestire i certificati SSL di proprietà del cliente e le chiavi private di autorità di certificazione terze, ad esempio *Crittografa*. |

>[!NOTE]
>
>Ai clienti non è consentito caricare certificati DV (convalida dominio).


## Introduzione ai certificati SSL {#certificates}

Aziende e organizzazioni utilizzano i certificati SSL per proteggere i propri siti web e consentire ai clienti di fidarsi di essi. Per utilizzare il protocollo SSL, un server web richiede l’utilizzo di un certificato SSL.

Quando un’entità, ad esempio un’organizzazione o un’azienda, richiede un certificato a un’autorità di certificazione (CA), questa completa un processo di verifica. Questo processo può spaziare dalla verifica del controllo dei nomi di dominio alla raccolta dei documenti di registrazione dell’azienda e degli accordi di sottoscrizione. Dopo aver verificato le informazioni di un’entità, l’autorità di certificazione firma la propria chiave pubblica utilizzando la chiave privata dell’autorità di certificazione. Poiché tutte le principali autorità di certificazione dispongono di certificati radice nei browser Web, il certificato dell&#39;entità è collegato tramite una *catena di attendibilità* e il browser Web lo riconosce come attendibile.

>[!IMPORTANT]
>
>Cloud Manager non fornisce certificati SSL o chiavi private. Questi elementi devono essere ottenuti da un&#39;Autorità di certificazione, un&#39;organizzazione di terze parti affidabile. Alcune Autorità di certificazione note includono *DigiCert*, *Crittografiamo*, *GlobalSign*, *Entrust* e *Verisign*.

Cloud Manager supporta le seguenti opzioni di utilizzo dei certificati SSL personalizzati del cliente.

* Più ambienti possono utilizzare un certificato SSL. In altre parole, può essere aggiunto una volta, ma utilizzato più volte.
* Ogni ambiente di Cloud Manager può utilizzare più certificati.
* Una chiave privata può emettere più certificati SSL.
* In genere, ogni certificato contiene più domini.
* Il servizio di piattaforma TLS indirizza le richieste al servizio CDN del cliente in base al certificato SSL utilizzato per terminare l’operazione e al servizio CDN che ospita tale dominio.
* Per i domini, AEM as a Cloud Service accetta certificati SSL con caratteri jolly.

AEM as a Cloud Service supporta solo siti `https` sicuri. I clienti con più domini personalizzati non desiderano caricare un certificato ogni volta che aggiungono un dominio. Per questi clienti è vantaggioso disporre di un solo certificato con più domini.

## Requisiti del certificato SSL {#requirements}

* AEM as a Cloud Service accetta certificati conformi ai criteri OV (convalida organizzazione), EV (convalida estesa) o DV (convalida dominio). <!-- CQDOC-21758, #2 -->
* Qualsiasi certificato deve essere un certificato TLS X.509 di un’autorità di certificazione attendibile con una chiave privata RSA a 2048 bit corrispondente.
* I certificati autofirmati non sono accettati.

I certificati OV ed EV offrono informazioni convalidate dalla CA. Tali informazioni aiutano gli utenti a valutare se il proprietario del sito web, il mittente dell’e-mail o il firmatario digitale dei documenti di codice o PDF possa essere considerato attendibile. I certificati DV non consentono tale verifica della proprietà.

### Formato del certificato SSL gestito dal cliente {#certificate-format}

<!-- CQDOC-21758, #3 -->

Per poter essere installati con Cloud Manager, i file del certificato SSL devono essere in formato PEM. Le estensioni comuni dei file in formato PEM includono `.pem,`. .`crt`, `.cer` e `.cert`.

Converti i certificati in formato diverso da PEM con i seguenti comandi `openssl`.

* Conversione da PFX a PEM

  ```shell
  openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes
  ```

* Conversione da P7B a PEM

  ```shell
  openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer
  ```

* Conversione da DER a PEM

  ```shell
  openssl x509 -inform der -in certificate.cer -out certificate.pem
  ```

## Limitazione del numero di certificati SSL installati {#limitations}

In qualsiasi momento, Cloud Manager consente un massimo di 50 certificati SSL installati. Questi certificati possono essere associati a uno o più ambienti nel programma e includere anche eventuali certificati scaduti.

Se hai raggiunto il limite, rivedi i certificati e prendi in considerazione l’eliminazione di eventuali certificati scaduti. Oppure, raggruppa più domini nello stesso certificato poiché un certificato può coprire più domini (fino a 100 SAN).

## Ulteriori informazioni {#learn-more}

Un utente con le autorizzazioni necessarie può utilizzare Cloud Manager per gestire i certificati SSL di un programma. Per ulteriori informazioni sull’utilizzo di queste funzioni, consulta i seguenti documenti.

* [Aggiungi un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) <!--CQDOC-21758, #4 -->
* [Gestione certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md) <!--CQDOC-21758, #4 -->

