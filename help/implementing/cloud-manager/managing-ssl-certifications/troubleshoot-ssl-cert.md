---
title: Risolvere i problemi relativi ai certificati SSL
description: Scopri come risolvere i problemi relativi ai certificati SSL identificando le cause comuni in modo da poter mantenere connessioni sicure.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 8fb8f708-51a5-46d0-8317-6ce118a70fab
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 31%

---

# Risolvere i problemi relativi ai certificati SSL {#certificate-problems}

Scopri come risolvere i problemi relativi ai certificati SSL identificando le cause comuni in modo da poter mantenere connessioni sicure.

+++**Certificato non valido**

## Certificato non valido {#invalid-certificate}

Questo errore si verifica perché il cliente ha utilizzato una chiave privata crittografata e ha fornito la chiave in formato DER.

+++

+++**La chiave privata deve essere in formato PKCS 8**

## La chiave privata deve essere in formato PKCS 8 {#pkcs-8}

Questo errore si verifica perché il cliente ha utilizzato una chiave privata crittografata e ha fornito la chiave in formato DER.

+++

+++**Ordine corretto dei certificati**

## Ordine corretto dei certificati {#certificate-order}

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

## Rimuovi certificati client {#client-certificates}

Quando aggiungi un certificato, se ricevi un errore simile al seguente:

```text
The Subject of an intermediate certificate must match the issuer in the previous certificate. The SKI of an intermediate certificate must match the AKI of the previous certificate.
```

È probabile che tu abbia incluso il certificato client nella catena di certificati. Assicurati che la catena non includa il certificato client e riprova.

+++

+++**Criteri certificato**

## Criterio certificato {#policy}

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

+++**Validità certificato

## Validità del certificato {#validity}

Cloud Manager richiede che il certificato SSL sia valido per almeno 90 giorni dalla data corrente. Verifica la validità della catena di certificati.

+++

+++**Il certificato SAN applicato al dominio non è corretto

## Il certificato SAN applicato al dominio non è corretto {#wrong-san-cert}

Si supponga di voler collegare `dev.yoursite.com` e `stage.yoursite.com` all&#39;ambiente non di produzione e `prod.yoursite.com` all&#39;ambiente di produzione.

Per configurare la rete CDN per questi domini, è necessario installare un certificato per ciascuno di essi, quindi installare un certificato che copre `*.yoursite.com` per i domini non di produzione e un altro che copre anche `*.yoursite.com` per i domini di produzione.

Configurazione valida. Tuttavia, quando aggiorni uno dei certificati, poiché entrambi i certificati coprono la stessa voce SAN, la rete CDN installerà il certificato più recente su tutti i domini applicabili, il che potrebbe apparire imprevisto.

Anche se questo comportamento può essere imprevisto, non si tratta di un errore e si tratta del comportamento standard della rete CDN sottostante. Se si dispone di due o più certificati SAN che coprono la stessa voce di dominio SAN, se tale dominio è coperto da un certificato e l&#39;altro è aggiornato, quest&#39;ultimo verrà ora installato per il dominio.

+++
