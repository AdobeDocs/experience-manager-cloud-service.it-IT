---
title: Aggiunta di un certificato SSL - Gestione dei certificati SSL
description: Aggiunta di un certificato SSL - Gestione dei certificati SSL
translation-type: tm+mt
source-git-commit: 4ab944ad15390f9399138672a024aa30cf4aede8
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# Aggiunta di un certificato SSL {#adding-an-ssl-certificate}

>[!NOTE]
>AEM come Cloud Service accetta solo i certificati OV(Organization Validation) o EV(Extended Validation). I certificati DV(Domain Validation) non verranno accettati.

Il provisioning di un certificato richiede alcuni giorni e si consiglia di eseguire il provisioning del certificato anche con mesi di anticipo. Per ulteriori informazioni, consultare [Ottenere un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md).

## Formato certificato {#certificate-format}

Per poter essere installati su Cloud Manager, i file SSL devono essere in formato PEM. Le estensioni di file comuni all&#39;interno del formato PEM includono `.pem,` .`crt`,  `.cer`e  `.cert`.

Per convertire i file SSL in PEM, effettuate le seguenti operazioni:

* Converti PFX in PEM

   `openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes`

* Converti P7B in PEM

   `openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer`

* Converti DER in PEM

   `openssl x509 -inform der -in certificate.cer -out certificate.pem`

## Considerazioni importanti {#important-considerations}

* Per installare un certificato SSL in Cloud Manager, un utente deve avere il ruolo Proprietario business o Gestione distribuzione.

* In qualsiasi momento, Cloud Manager consentirà un massimo di 10 certificati SSL che possono essere associati a uno o più ambienti nel programma, anche se un certificato è scaduto. L&#39;interfaccia utente di Cloud Manager, tuttavia, consentirà l&#39;installazione di fino a 50 certificati SSL nel programma con questo vincolo.

## Aggiunta di un certificato {#adding-a-cert}

Per aggiungere un certificato, effettuate le operazioni seguenti:

1. Accedi a Cloud Manager.
1. Passare alla schermata **Ambienti** dalla pagina **Panoramica**.
1. Fare clic su **Certificati SSL** dal menu di navigazione a sinistra. In questa schermata viene visualizzata una tabella con i dettagli di eventuali certificati SSL esistenti.

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. Fare clic su **Aggiungi certificato SSL** per aprire la finestra di dialogo **Aggiungi certificato SSL**.

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)

   1. Immettere un nome per il certificato in **Nome certificato**. Può trattarsi di un nome qualsiasi che faciliti il riferimento al certificato.
   1. Incollare i **Certificate**, **Private key** e **Certificate chain** nei rispettivi campi. Utilizzate l&#39;icona Incolla a destra della casella di input.
Tutti e tre i campi non sono facoltativi e devono essere inclusi.

1. Fare clic su **Salva** per inviare il certificato. La tabella verrà visualizzata come nuova riga.

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)
   >[!NOTE]
   >Eventuali errori rilevati verranno visualizzati. È necessario risolvere tutti gli errori prima di salvare il certificato. Fare riferimento a [Errori certificati](#certificate-errors) per ulteriori informazioni sulla risoluzione di errori comuni.

## Errori certificati {#certificate-errors}

### Ordine certificato corretto {#correct-certificate-order}

Il motivo più comune per cui una distribuzione di certificati non riesce è che i certificati intermedi o a catena non sono nell&#39;ordine corretto. Nello specifico, i file di certificato intermedi devono terminare con il certificato radice o il certificato più vicino alla radice ed essere in ordine decrescente dal certificato `main/server` alla radice.

È possibile determinare l&#39;ordine dei file intermedi utilizzando il seguente comando:

`openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout`

È possibile verificare che la chiave privata e il certificato `main/server` corrispondano utilizzando i comandi seguenti:

`openssl x509 -noout -modulus -in certificate.pem | openssl md5`

`openssl rsa -noout -modulus -in ssl.key | openssl md5`

>[!NOTE]
>L&#39;output di questi due comandi deve essere esattamente lo stesso. Se non riuscite a individuare una chiave privata corrispondente nel certificato `main/server`, dovrete chiave nuovamente del certificato generando un nuovo CSR e/o richiedendo un certificato aggiornato dal fornitore SSL.

### Date di validità del certificato {#certificate-validity-dates}

Cloud Manager prevede che il certificato SSL sarà valido per almeno 90 giorni in futuro. È necessario verificare la validità della catena di certificati.
