---
title: Aggiunta di un certificato SSL - Gestione dei certificati SSL
description: Aggiunta di un certificato SSL - Gestione dei certificati SSL
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
source-git-commit: e8848a006a28e87a622779ae62bc43c159b2b20c
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---

# Aggiunta di un certificato SSL {#adding-an-ssl-certificate}

>[!NOTE]
>AEM come Cloud Service accetterà solo i certificati OV (Organization Validation) o EV (Extended Validation). I certificati DV (Convalida del dominio) non verranno accettati. Inoltre, qualsiasi certificato deve essere un certificato TLS X.509 di un’autorità di certificazione (CA) affidabile con una chiave privata RSA a 2048 bit corrispondente. AEM come Cloud Service accetterà i certificati SSL con caratteri jolly per un dominio.

Il provisioning di un certificato richiede alcuni giorni e si consiglia di effettuare il provisioning del certificato con mesi di anticipo. Per ulteriori informazioni, consulta [Ottenere un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md) .

## Formato del certificato {#certificate-format}

Per poter essere installati su Cloud Manager, i file SSL devono essere in formato PEM. Le estensioni di file comuni che si trovano nel formato PEM includono `.pem,` .`crt`,  `.cer` e  `.cert`.

Per convertire il formato dei file SSL in PEM, effettua le seguenti operazioni:

* Converti PFX in PEM

   `openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes`

* Converti P7B in PEM

   `openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer`

* Converti DER in PEM

   `openssl x509 -inform der -in certificate.cer -out certificate.pem`

## Considerazioni importanti {#important-considerations}

* Per installare un certificato SSL in Cloud Manager, un utente deve trovarsi nel ruolo Proprietario business o Gestore distribuzione.

* In un dato momento, Cloud Manager consentirà un massimo di 10 certificati SSL che possono essere associati a uno o più ambienti nel programma, anche se un certificato è scaduto. L’interfaccia utente di Cloud Manager, tuttavia, consentirà l’installazione di un massimo di 50 certificati SSL nel programma con questo vincolo.

## Aggiunta di un certificato {#adding-a-cert}

Per aggiungere un certificato, effettua le seguenti operazioni:

1. Accedi a Cloud Manager.
1. Passa alla schermata **Ambienti** dalla pagina **Panoramica** .
1. Fai clic su **Certificati SSL** dal menu di navigazione a sinistra. In questa schermata viene visualizzata una tabella con i dettagli degli eventuali certificati SSL esistenti.

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. Fai clic su **Aggiungi certificato SSL** per aprire la finestra di dialogo **Aggiungi certificato SSL**.

   * Immetti un nome per il certificato in **Nome certificato**. Può essere un nome qualsiasi che ti aiuti a fare riferimento facilmente al certificato.
   * Incolla la **Certificato**, **Chiave privata** e **Catena certificati** nei rispettivi campi. Utilizza l’icona Incolla a destra della casella di input.
Tutti e tre i campi non sono facoltativi e devono essere inclusi.

      ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)


      >[!NOTE]
      >Vengono visualizzati tutti gli errori rilevati. È necessario risolvere tutti gli errori prima di salvare il certificato. Per ulteriori informazioni sulla gestione degli errori comuni, consulta [Errori di certificato](#certificate-errors) .

1. Fai clic su **Salva** per inviare il certificato. Viene visualizzata come una nuova riga nella tabella.

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

## Errori di certificato {#certificate-errors}

### Ordine certificato corretto {#correct-certificate-order}

Il motivo più comune per cui una distribuzione di certificati non riesce è che i certificati intermedi o a catena non sono nell’ordine corretto. In particolare, i file di certificato intermedio devono terminare con il certificato principale o il certificato più vicino alla radice ed essere in ordine decrescente dal certificato `main/server` alla radice.

È possibile determinare l&#39;ordine dei file intermedi utilizzando il seguente comando:

`openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout`

Puoi verificare che la chiave privata e il certificato corrispondano utilizzando i seguenti comandi:`main/server`

`openssl x509 -noout -modulus -in certificate.pem | openssl md5`

`openssl rsa -noout -modulus -in ssl.key | openssl md5`

>[!NOTE]
>L&#39;output di questi due comandi deve essere esattamente lo stesso. Se non riesci a individuare una chiave privata corrispondente al certificato `main/server`, dovrai chiave nuovamente del certificato generando una nuova CSR e/o richiedendo un certificato aggiornato dal fornitore SSL.

### Date di validità del certificato {#certificate-validity-dates}

Cloud Manager prevede che il certificato SSL sia valido per almeno 90 giorni nel futuro. È necessario verificare la validità della catena di certificati.
