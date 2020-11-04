---
title: Aggiunta di un certificato SSL - Gestione dei certificati SSL
description: Aggiunta di un certificato SSL - Gestione dei certificati SSL
translation-type: tm+mt
source-git-commit: e27e5302802e68dce2a5713626950896bb35420a
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---


# Aggiunta di un certificato SSL {#adding-an-ssl-certificate}

>[!NOTE]
>Il provisioning di un certificato richiede alcuni giorni e si consiglia di eseguire il provisioning del certificato anche con mesi di anticipo. Vai Come ottenere un certificato SSL per saperne di più.INSERT LINK

## Formato certificato {#certificate-format}

Per poter essere installati su Cloud Manager, i file SSL devono essere in formato PEM. Le estensioni di file comuni che si trovano nel formato PEM includono .pem, .crt, .cer e .cert.

Per convertire i file SSL in PEM, effettuate le seguenti operazioni:

1. Converti PFX in PEM

`openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes`

1. Converti P7B in PEM

`openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer`

1. Converti DER in PEM

`openssl x509 -inform der -in certificate.cer -out certificate.pem`

## Aggiunta del certificato {#adding-certificate}

>[!NOTE]
>* Per installare un certificato SSL in Cloud Manager, un utente deve avere il ruolo Proprietario business o Gestione distribuzione.
>* In qualsiasi momento, Cloud Manager consentirà un massimo di 5 certificati SSL che possono essere associati a uno o più ambienti nel programma, anche se il certificato è scaduto. L&#39;interfaccia utente di Cloud Manager, tuttavia, consentirà l&#39;installazione di fino a 50 certificati SSL nel programma con questo vincolo.


1. Accedi a Cloud Manager.
1. Passare alla schermata Ambienti dalla pagina Panoramica.
1. Andate alla schermata Certificati SSL dal menu di navigazione a sinistra. In questa schermata verrà visualizzata una tabella con i dettagli di eventuali certificati SSL esistenti.INSERT IMAGE
1. Fate clic sul pulsante **Aggiungi certificato** per avviare una procedura guidata.
1. Immettete un nome per il certificato. Può trattarsi di un nome qualsiasi che faciliti il riferimento al certificato.
1. Incollate il contenuto Certificato, Chiave privata e Catena nei rispettivi campi. Utilizzate l&#39;icona Incolla a destra della casella di input.
1. Seleziona **Salva**.

   >[!NOTE]
   >Eventuali errori rilevati verranno visualizzati. È necessario risolvere tutti gli errori prima di salvare il certificato. Per ulteriori informazioni sulla risoluzione degli errori comuni, fare riferimento a Errori di collegamento per l&#39;inserimento di certificati.

   Dopo aver inviato il certificato, verrà visualizzato come una nuova riga nella tabella.

## Errori di certificato {#certificate-errors}

### Ordine certificato corretto {#correct-certificate-order}

Il motivo più comune per cui una distribuzione di certificati non riesce è che i certificati intermedi o a catena non sono nell&#39;ordine corretto. Nello specifico, i file di certificato intermedi devono terminare con il certificato radice o il certificato più vicino alla radice ed essere in ordine decrescente dal `main/server` certificato alla radice.

È possibile determinare l&#39;ordine dei file intermedi utilizzando il seguente comando:

`openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout`

Potete verificare che la chiave privata e il `main/server` certificato corrispondano ai seguenti comandi:

`openssl x509 -noout -modulus -in certificate.pem | openssl md5`

`openssl rsa -noout -modulus -in ssl.key | openssl md5`

>[!NOTE]
>L&#39;output di questi due comandi deve essere esattamente lo stesso. Se non riuscite a individuare una chiave privata corrispondente nel `main/server` certificato, dovrete chiave nuovamente il certificato generando un nuovo CSR e/o richiedendo un certificato aggiornato dal fornitore SSL.

### Date validità certificato {#certificate-validity-dates}

Cloud Manager prevede che il certificato SSL sarà valido per almeno 90 giorni nel futuro

Verificare la validità della catena di certificati.
