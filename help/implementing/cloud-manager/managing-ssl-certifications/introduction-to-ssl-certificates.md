---
title: Introduzione ai certificati SSL
description: Scopri gli strumenti self-service forniti da Cloud Manager per installare e gestire i certificati SSL.
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: fa99656e0dd02bb97965e8629d5fa657fbae9424
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 22%

---


# Introduzione ai certificati SSL{#introduction}

Scopri gli strumenti self-service forniti da Cloud Manager per installare e gestire i certificati SSL (Secure Socket Layer).

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="Gestire i certificati SSL"
>abstract="Scopri gli strumenti self-service di Cloud Manager per l’installazione e la gestione dei certificati SSL al fine di proteggere il sito per gli utenti. Cloud Manager si avvale di un servizio di piattaforma TLS per gestire i certificati SSL e le chiavi private di proprietà dei clienti ottenuti da autorità di certificazione terze."
>additional-url="https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="Visualizzazione, aggiornamento e sostituzione di un certificato SSL"
>additional-url="https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="Controllo dello stato di un certificato SSL"

## Cosa sono i certificati SSL? {#overview}

Aziende e organizzazioni utilizzano i certificati SSL (Secure Socket Layer) per proteggere i propri siti Web e consentire ai clienti di fidarsi di tali certificati. Per utilizzare il protocollo SSL, un server web richiede un certificato SSL.

Quando un’entità, ad esempio un’organizzazione o un’azienda, richiede un certificato a un’autorità di certificazione (CA), questa completa un processo di verifica. Questo processo può spaziare dalla verifica del controllo dei nomi di dominio alla raccolta dei documenti di registrazione dell’azienda e degli accordi di sottoscrizione. Dopo aver verificato le informazioni di un’entità, l’autorità di certificazione firma la propria chiave pubblica utilizzando la chiave privata dell’autorità di certificazione. Poiché tutte le principali autorità di certificazione dispongono di certificati radice nei browser Web, il certificato dell&#39;entità è collegato tramite una *catena di attendibilità* e il browser Web lo riconosce come attendibile.

>[!IMPORTANT]
>
>Cloud Manager non fornisce certificati SSL o chiavi private. Tali componenti devono essere ottenuti da un&#39;Autorità di certificazione, un&#39;organizzazione terza affidabile. Alcune Autorità di certificazione note includono *DigiCert*, *Crittografiamo*, *GlobalSign*, *Entrust* e *Verisign*.

## Gestire i certificati con Cloud Manager {#cloud-manager}

Cloud Manager offre strumenti self-service per installare e gestire i certificati SSL, garantendo la sicurezza del sito per gli utenti. Cloud Manager supporta due modelli per la gestione dei certificati.

| | Modello | Descrizione |
| --- | --- | --- |
| A | **[Adobe di certificato SSL gestito (DV)](#adobe-managed)** | Cloud Manager consente agli utenti di configurare i certificati DV (Domain Validation) forniti da Adobe per la configurazione rapida del dominio. |
| B | **[Certificato SSL gestito dal cliente (OV/EV)](#customer-managed)** | Cloud Manager offre un servizio di piattaforma TLS (Transport Layer Security) che consente di gestire i certificati SSL OV ed EV di tua proprietà e le chiavi private di autorità di certificazione terze, ad esempio *Crittografiamo*. |

Entrambi i modelli offrono le seguenti funzionalità generali per la gestione dei certificati:

* Ogni ambiente di Cloud Manager può utilizzare più certificati.
* Una chiave privata può emettere più certificati SSL.
* Il servizio di piattaforma TLS indirizza le richieste al servizio CDN del cliente in base al certificato SSL utilizzato per terminare l’operazione e al servizio CDN che ospita tale dominio.

>[!IMPORTANT]
>
>[Per aggiungere e associare un dominio personalizzato a un ambiente](/help/implementing/cloud-manager/custom-domain-names/introduction.md), è necessario disporre di un certificato SSL valido relativo al dominio.

### Adobe di certificati SSL gestiti (DV) {#adobe-managed}

I certificati DV rappresentano il livello di base della certificazione SSL e vengono spesso utilizzati per scopi di test o per proteggere i siti Web con crittografia di base. I certificati DV sono disponibili sia nei [programmi di produzione che nei programmi sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md).

Dopo la creazione del certificato DV, Adobe lo rinnova automaticamente ogni tre mesi, a meno che non venga eliminato.

### Certificati SSL OV/EV gestiti dal cliente {#customer-managed}

I certificati OV ed EV offrono informazioni convalidate dalla CA. Tali informazioni aiutano gli utenti a valutare se il proprietario del sito web, il mittente dell’e-mail o il firmatario digitale dei documenti di codice o PDF possa essere considerato attendibile. I certificati DV non consentono tale verifica della proprietà.

OV ed EV offrono inoltre queste funzioni sui certificati DV in Cloud Manager.

* Più ambienti possono utilizzare un certificato OV/EV. In altre parole, può essere aggiunto una volta, ma utilizzato più volte.
* Ogni certificato OV/EV in genere contiene più domini.
* Cloud Manager accetta certificati OV/EV con caratteri jolly per un dominio.

>[!TIP]
>
>Se disponi di più domini personalizzati, potresti non voler caricare un certificato ogni volta che aggiungi un nuovo dominio. In tal caso, potresti trarre vantaggio dall’ottenimento di un singolo certificato che copre più domini.

>[!NOTE]
>
>Se due certificati coprono lo stesso dominio, viene applicato quello più esatto.
>
>Ad esempio, se il dominio è `dev.adobe.com` e si dispone di un certificato per `*.adobe.com` e un altro per `dev.adobe.com`, verrà utilizzato quello più specifico (`dev.adobe.com`).

#### Requisiti per i certificati SSL OV/EV gestiti dal cliente {#requirements}

Se scegli di aggiungere un certificato OV/EV SSL gestito dal cliente, questo deve soddisfare i seguenti requisiti:

* AEM as a Cloud Service accetta certificati conformi ai criteri OV (convalida organizzazione) o EV (convalida estesa).
   * Cloud Manager non supporta l&#39;aggiunta di certificati DV (Domain Validation) personalizzati.
* Qualsiasi certificato deve essere un certificato TLS X.509 di un’autorità di certificazione attendibile con una chiave privata RSA a 2048 bit corrispondente.
* I certificati autofirmati non sono accettati.

#### Formato dei certificati gestiti dal cliente {#certificate-format}

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

>[!TIP]
>
>L&#39;Adobe consiglia di convalidare localmente l&#39;integrità del certificato utilizzando uno strumento quale `openssl verify -untrusted intermediate.pem certificate.pem` prima di tentare l&#39;installazione tramite Cloud Manager.

## Limitazione del numero di certificati SSL installati {#limitations}

In qualsiasi momento, Cloud Manager consente un massimo di 50 certificati SSL installati. Questi certificati possono essere associati a uno o più ambienti nel programma e includere anche eventuali certificati scaduti.

Se hai raggiunto il limite, rivedi i certificati e prendi in considerazione l’eliminazione di eventuali certificati scaduti. Oppure, raggruppa più domini nello stesso certificato poiché un certificato può coprire più domini (fino a 100 SAN).

## Ulteriori informazioni {#learn-more}

Un utente con le autorizzazioni necessarie può utilizzare Cloud Manager per gestire i certificati SSL di un programma. Per ulteriori informazioni sull’utilizzo di queste funzioni, consulta i seguenti documenti.

* [Aggiungi un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) <!--CQDOC-21758, #4 -->
* [Gestione certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md) <!--CQDOC-21758, #4 -->

