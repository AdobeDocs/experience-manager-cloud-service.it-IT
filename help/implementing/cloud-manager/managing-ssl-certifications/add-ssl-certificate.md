---
title: Aggiunta di un certificato SSL
description: Scopri come aggiungere un certificato SSL personalizzato con gli strumenti self-service di Cloud Manager.
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
source-git-commit: d1b2226a1deec2e71056c43c84672cb4a358bc8c
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 73%

---

# Aggiunta di un certificato SSL {#adding-an-ssl-certificate}

Scopri come aggiungere un certificato SSL personalizzato con gli strumenti self-service di Cloud Manager.

>[!TIP]
>
>Il provisioning di un certificato può richiedere alcuni giorni. Adobe consiglia pertanto di eseguire il provisioning del certificato con largo anticipo.

## Requisiti dei certificati {#certificate-requirements}

Rivedi la sezione **Requisiti dei certificati** del documento [Introduzione alla gestione dei certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md#requirements) per garantire che il certificato che desideri aggiungere sia supportato da AEM as a Cloud Service.

## Aggiunta di un certificato {#adding-a-cert}

Per aggiungere un certificato con Cloud Manager, segui la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Il giorno **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)** , selezionare il programma.

1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.

1. Clic **Certificati SSL** dal pannello di navigazione a sinistra. Nella schermata principale viene visualizzata una tabella con i dettagli di tutti i certificati SSL esistenti.

   ![Aggiunta di un certificato SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. Clic **Aggiungi certificato SSL** per aprire **Aggiungi certificato SSL** .

   * Inserisci un nome per il certificato nel campo **Nome certificato**.
      * Il nome è unicamente a scopo informativo e può essere qualsiasi nome che ti aiuta a ricordare facilmente il certificato.
   * Incolla il **certificato**, la **chiave privata** e la **catena di certificati** nei rispettivi campi. Tutti e tre i campi sono obbligatori.
   * In alcuni casi, il certificato dell’utente finale può essere incluso nella catena e deve essere rimosso prima di incollare la catena nel campo.

   ![Finestra di dialogo Aggiungi certificato SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)

   * Vengono visualizzati tutti gli eventuali errori rilevati.
      * Prima di salvare il certificato è necessario risolvere tutti gli errori.
      * Per ulteriori informazioni su come risolvere gli errori comuni, consulta la sezione [Errori relativi ai certificati](#certificate-errors).

1. Per salvare il certificato, fai clic su **Salva**.

Una volta salvato, il certificato viene visualizzato come una nuova riga nella tabella.

![Certificato SSL salvato](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

>[!NOTE]
>
>Per installare un certificato SSL in Cloud Manager, l’utente deve avere il ruolo **Proprietario business** o **Responsabile dell’implementazione**.

>[!NOTE]
>
>Se ricevi un errore simile a `The Subject of an intermediate certificate must match the issuer in the previous certificate. The SKI of an intermediate certificate must match the AKI of the previous certificate.`, è probabile che tu abbia incluso il certificato client nella catena di certificati. Verifica che la catena non includa il certificato client e riprova.

## Errori relativi ai certificati {#certificate-errors}

Se un certificato non è installato correttamente o non soddisfa i requisiti di Cloud Manager, possono verificarsi alcuni errori.

### Criteri del certificato {#certificate-policy}

Se visualizzi il seguente errore, controlla i criteri del certificato.

```text
Certificate policy must conform with EV or OV, and not DV policy.
```

Normalmente i criteri del certificato sono identificati dai valori OID incorporati. Per visualizzare i criteri del certificato, genera il certificato come testo e ricerca i valori OID.

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
>L’output di questi due comandi deve essere esattamente lo stesso. Se non riesci a individuare una chiave privata corrispondente al tuo `main/server` , ti viene richiesto di reimpostare il certificato generando una nuova CSR e/o richiedendo un certificato aggiornato al fornitore SSL.

### Date di validità del certificato {#certificate-validity-dates}

Cloud Manager richiede che il certificato SSL sia valido per almeno 90 giorni dalla data corrente. Verifica la validità della catena di certificati.
