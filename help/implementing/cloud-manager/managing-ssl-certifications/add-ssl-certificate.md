---
title: Aggiunta di un certificato SSL
description: Scopri come aggiungere un certificato SSL personalizzato utilizzando gli strumenti self-service di Cloud Manager.
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
source-git-commit: 2c87d5fb33b83ca77b97391e4b0baaf38f8dd026
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 2%

---

# Aggiunta di un certificato SSL {#adding-an-ssl-certificate}

Scopri come aggiungere un certificato SSL personalizzato utilizzando gli strumenti self-service di Cloud Manager.

>[!TIP]
>
>Il provisioning di un certificato può richiedere alcuni giorni. L’Adobe raccomanda pertanto che il certificato sia predisposto con largo anticipo.

## Formato del certificato {#certificate-format}

Per poter essere installati con Cloud Manager, i file di certificato SSL devono essere in formato PEM. Le estensioni comuni dei file in formato PEM includono `.pem,` .`crt`, `.cer`, e `.cert`.

I seguenti `openssl` i comandi possono essere utilizzati per convertire i certificati non PEM.

* Converti PFX in PEM

   ```shell
   openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes
   ```

* Converti P7B in PEM

   ```shell
   openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer
   ```

* Converti DER in PEM

   ```shell
   openssl x509 -inform der -in certificate.cer -out certificate.pem
   ```

## Aggiunta di un certificato {#adding-a-cert}

Segui questi passaggi per aggiungere un certificato utilizzando Cloud Manager.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.

1. Passa a **Ambienti** dalla schermata **Panoramica** pagina.

1. Fai clic su **Certificati SSL** dal pannello di navigazione a sinistra. Nella schermata principale viene visualizzata una tabella con i dettagli degli eventuali certificati SSL esistenti.

   ![Aggiunta di un certificato SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. Fai clic su **Aggiungi certificato SSL** aprire **Aggiungi certificato SSL** finestra di dialogo.

   * Immetti un nome per il certificato in **Nome certificato**.
      * Questo è solo a scopo informativo e può essere qualsiasi nome che ti aiuti a fare riferimento facilmente al tuo certificato.
   * Incolla **Certificato**, **Chiave privata** e **Catena di certificati** nei rispettivi campi.
      * Puoi utilizzare l’icona Incolla a destra della casella di input.
      * Tutti e tre i campi sono obbligatori.

   ![Finestra di dialogo Aggiungi certificato SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)

   * Vengono visualizzati tutti gli errori rilevati.
      * È necessario risolvere tutti gli errori prima di salvare il certificato.
      * Fai riferimento a [Errori di certificato](#certificate-errors) per ulteriori informazioni sulla gestione degli errori comuni.


1. Fai clic su **Salva** per salvare il certificato.

Una volta salvato, il certificato verrà visualizzato come una nuova riga nella tabella.

![Certificato SSL salvato](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

>[!NOTE]
>
>Un utente deve essere membro del **Proprietario business** o **Gestione distribuzione** per installare un certificato SSL in Cloud Manager.

## Errori di certificato {#certificate-errors}

Alcuni errori possono verificarsi se un certificato non è installato correttamente o soddisfa i requisiti di Cloud Manager.

### Criterio certificato {#certificate-policy}

Se viene visualizzato il seguente errore, controlla i criteri del certificato.

```text
Certificate policy must conform with EV or OV, and not DV policy.
```

Normalmente i criteri dei certificati sono identificati dai valori OID incorporati. L’invio di un certificato al testo e la ricerca dell’OID mostreranno i criteri del certificato.

Puoi generare i dettagli del certificato come testo utilizzando l’esempio seguente come guida.

```text
openssl x509 -in 9178c0f58cb8fccc.pem -text
certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            91:78:c0:f5:8c:b8:fc:cc
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: C = US, ST = Arizona, L = Scottsdale, O = "GoDaddy.com, Inc.", OU = http://certs.godaddy.com/repository/, CN = Go Daddy Secure Certificate Authority - G2
        Validity
            Not Before: Nov 10 22:55:36 2021 GMT
            Not After : Dec  6 15:35:06 2022 GMT
        Subject: C = US, ST = Colorado, L = Denver, O = Alexandra Alwin, CN = adobedigitalimpact.com
        Subject Public Key Info:
...
```

Il pattern OID nel testo definisce il tipo di criterio del certificato.

| Pattern | Criterio | Accettabile in Cloud Manager |
|---|---|---|
| `2.23.140.1.1` | EV | Sì |
| `2.23.140.1.2.2` | OV | Sì |
| `2.23.140.1.2.1` | DV | No |

Da `grep`Se esegui il ping dei pattern OID nel testo del certificato di output, puoi confermare i criteri del certificato.

```shell
# "EV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.1" -B5

# "OV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.2" -B5

# "DV Policy - Not Accepted"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.1" -B5
```

### Ordine di certificazione corretto {#correct-certificate-order}

Il motivo più comune per cui una distribuzione di certificati non riesce è che i certificati intermedi o a catena non sono nell’ordine corretto.

I file di certificato intermedi devono terminare con il certificato principale o con il certificato più vicino alla radice. Devono essere in ordine decrescente dal `main/server` certificato alla radice.

È possibile determinare l&#39;ordine dei file intermedi utilizzando il seguente comando.

```shell
openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout
```

Puoi verificare che la chiave privata e `main/server` corrispondenza del certificato utilizzando i seguenti comandi.

```shell
openssl x509 -noout -modulus -in certificate.pem | openssl md5
```

```shell
openssl rsa -noout -modulus -in ssl.key | openssl md5
```

>[!NOTE]
>
>L&#39;output di questi due comandi deve essere esattamente lo stesso. Se non riesci a individuare una chiave privata corrispondente per la tua `main/server` certificato: devi reimpostare il certificato generando una nuova CSR e/o richiedendo un certificato aggiornato dal fornitore SSL.

### Date di validità del certificato {#certificate-validity-dates}

Cloud Manager prevede che il certificato SSL sia valido per almeno 90 giorni dalla data corrente. È necessario verificare la validità della catena di certificati.
