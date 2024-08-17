---
title: Aggiungere un certificato SSL
description: Scopri come aggiungere un certificato SSL personalizzato con gli strumenti self-service di Cloud Manager.
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 64aa010c3d840adad9e1ab6040a6d80c07cd8455
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 45%

---


# Aggiungere un certificato SSL {#adding-an-ssl-certificate}

Scopri come aggiungere un certificato SSL personalizzato con gli strumenti self-service di Cloud Manager.

>[!TIP]
>
>Il provisioning di un certificato può richiedere alcuni giorni. L’Adobe raccomanda pertanto di predisporre il certificato con largo anticipo rispetto a qualsiasi scadenza o data di pubblicazione.

## Requisiti del certificato {#certificate-requirements}

Rivedi **Requisiti del certificato** in [Introduzione alla gestione dei certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md#requirements) per assicurarti che AEM as a Cloud Service supporti il certificato che desideri aggiungere.

## Aggiungi un certificato {#adding-a-cert}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.

1. Nel pannello di navigazione a sinistra, in **Servizi**, fai clic su **Certificati SSL**. Se necessario, fai clic sull’icona dell’hamburger nell’angolo in alto a sinistra per visualizzare il pannello di navigazione. Viene visualizzata una tabella con i dettagli di eventuali certificati SSL esistenti.

   ![Aggiunta di un certificato SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. Fare clic su **Aggiungi certificato SSL** per aprire la finestra di dialogo **Aggiungi certificato SSL**.

   * Immettere un nome per il certificato in **Nome certificato**. Questo campo è solo a scopo informativo e può essere qualsiasi nome che ti aiuti a fare riferimento facilmente al certificato.
   * Incolla il **certificato**, la **chiave privata** e la **catena di certificati** nei rispettivi campi. I tre campi sono obbligatori.

   ![Finestra di dialogo Aggiungi certificato SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)

   * Vengono visualizzati tutti gli eventuali errori rilevati nei valori. Prima di poter salvare il certificato, è necessario risolvere tutti gli errori.
Per ulteriori informazioni su come risolvere gli errori comuni, consulta [Errori relativi ai certificati](#certificate-errors).

1. Fai clic su **Salva**.

![Certificato SSL salvato](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)Il certificato viene ora visualizzato come una nuova riga nella tabella, simile all&#39;immagine precedente.

>[!NOTE]
>
>Per installare un certificato SSL in Cloud Manager, l’utente deve avere il ruolo **Proprietario business** o **Responsabile dell’implementazione**.

## Errori relativi ai certificati {#certificate-errors}

Se un certificato non è installato correttamente o non soddisfa i requisiti di Cloud Manager, possono verificarsi alcuni errori.

### Ordine corretto dei certificati {#correct-certificate-order}

Il motivo più comune alla base di una distribuzione dei certificati non riuscita è che i certificati intermedi o a catena non sono disposti nell’ordine corretto.

I file di certificato intermedi devono terminare con il certificato radice o con quello più vicino. Devono essere disposti in ordine decrescente, dal certificato `main/server` alla radice.

È possibile determinare l’ordine dei file intermedi con il seguente comando.

```shell
openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout
```

Puoi verificare che la chiave privata e il certificato `main/server` corrispondano con i seguenti comandi.

```shell
openssl x509 -noout -modulus -in certificate.pem | openssl md5
```

```shell
openssl rsa -noout -modulus -in ssl.key | openssl md5
```

>[!NOTE]
>
>L’output di questi due comandi deve essere esattamente lo stesso. Se non riesci a individuare una chiave privata corrispondente al certificato `main/server`, ti viene richiesto di generarne una nuova generando un nuovo CSR e/o richiedendo un certificato aggiornato al fornitore SSL.

### Rimuovi certificati client {#client-certificates}

Quando aggiungi un certificato, se ricevi un errore simile al seguente:

```text
The Subject of an intermediate certificate must match the issuer in the previous certificate. The SKI of an intermediate certificate must match the AKI of the previous certificate.
```

È probabile che tu abbia incluso il certificato client nella catena di certificati. Assicurati che la catena non includa il certificato client e riprova.

### Criterio certificato {#certificate-policy}

Se visualizzi il seguente errore, controlla i criteri del certificato.

```text
Certificate policy must conform with EV or OV, and not DV policy.
```

I valori OID incorporati solitamente identificano i criteri del certificato. L’output di un certificato come testo e la ricerca dell’OID rivelano i criteri del certificato.

Puoi generare i dettagli del certificato come testo basandoti sull’esempio seguente come guida.

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

Conferma il criterio del certificato eseguendo il comando `grep` per i pattern OID nel testo del certificato generato.

```shell
# "EV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.1" -B5

# "OV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.2" -B5

# "DV Policy - Not Accepted"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.1" -B5
```

### Date di validità del certificato {#certificate-validity-dates}

Cloud Manager richiede che il certificato SSL sia valido per almeno 90 giorni dalla data corrente. Verifica la validità della catena di certificati.

## Passaggi successivi {#next-steps}

Congratulazioni Ora disponi di un certificato SSL funzionante per il progetto. Questo passaggio è spesso il primo a configurare un nome di dominio personalizzato.

* Per impostare un nome di dominio personalizzato, vedere [Aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).
* Per informazioni sull&#39;aggiornamento e la gestione dei certificati SSL in Cloud Manager, vedere [Gestione dei certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md).
