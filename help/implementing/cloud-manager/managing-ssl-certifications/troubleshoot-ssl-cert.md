---
title: Risolvere i problemi relativi agli errori dei certificati SSL
description: Scopri come risolvere gli errori dei certificati SSL identificando le cause comuni in modo da poter mantenere connessioni sicure.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 9ffec422ec4b5a45962f07142c49a466e8892754
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 53%

---


# Risolvere i problemi relativi agli errori dei certificati SSL {#certificate-errors}

Se un certificato non è installato correttamente o non soddisfa i requisiti di Cloud Manager, possono verificarsi alcuni errori.

+++**Ordine corretto dei certificati**

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

+++

+++**Rimuovi certificati client**

Quando aggiungi un certificato, se ricevi un errore simile al seguente:

```text
The Subject of an intermediate certificate must match the issuer in the previous certificate. The SKI of an intermediate certificate must match the AKI of the previous certificate.
```

È probabile che tu abbia incluso il certificato client nella catena di certificati. Assicurati che la catena non includa il certificato client e riprova.

+++

+++**Criteri certificato**

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

+++

+++**Date validità certificato**

Cloud Manager richiede che il certificato SSL sia valido per almeno 90 giorni dalla data corrente. Verifica la validità della catena di certificati.

+++