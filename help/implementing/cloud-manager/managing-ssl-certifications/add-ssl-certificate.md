---
title: Aggiunta di un certificato SSL - Gestione dei certificati SSL
description: Aggiunta di un certificato SSL - Gestione dei certificati SSL
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
source-git-commit: 828490e12d99bc8f4aefa0b41a886f86fee920b4
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 0%

---

# Aggiunta di un certificato SSL {#adding-an-ssl-certificate}

>[!NOTE]
>AEM as a Cloud Service accetterà solo i certificati conformi ai criteri OV (Organization Validation) o EV (Extended Validation). I criteri di convalida del dominio DV non verranno accettati. Inoltre, qualsiasi certificato deve essere un certificato TLS X.509 di un’autorità di certificazione (CA) affidabile con una chiave privata RSA a 2048 bit corrispondente. AEM as a Cloud Service accetterà i certificati SSL con caratteri jolly per un dominio.

Il provisioning di un certificato richiede alcuni giorni e si consiglia di effettuare il provisioning del certificato con mesi di anticipo. Fai riferimento a [Ottenimento di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md) per ulteriori dettagli.

## Formato del certificato {#certificate-format}

Per poter essere installati su Cloud Manager, i file SSL devono essere in formato PEM. Le estensioni comuni di file che si trovano nel formato PEM includono `.pem,` .`crt`, `.cer`, e `.cert`.

Per convertire il formato dei file SSL in PEM, effettua le seguenti operazioni:

* Converti PFX in PEM

   `openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes`

* Converti P7B in PEM

   `openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer`

* Converti DER in PEM

   `openssl x509 -inform der -in certificate.cer -out certificate.pem`

## Considerazioni importanti {#important-considerations}

* Per installare un certificato SSL in Cloud Manager, un utente deve trovarsi nel ruolo Proprietario business o Gestore distribuzione.

* In un dato momento, Cloud Manager consentirà un massimo di 10 certificati SSL che possono essere associati a uno o più ambienti nel programma, anche se un certificato è scaduto. L’interfaccia utente di Cloud Manager, tuttavia, consentirà l’installazione di un massimo di 50 certificati SSL nel programma con questo vincolo. In genere un certificato può includere più domini (fino a 100 SAN), pertanto è consigliabile raggruppare più domini nello stesso certificato per rimanere entro questo limite.


## Aggiunta di un certificato {#adding-a-cert}

Per aggiungere un certificato, effettua le seguenti operazioni:

1. Accedi a Cloud Manager.
1. Passa a **Ambienti** schermata da **Panoramica** pagina.
1. Fai clic su **Certificati SSL** dal menu di navigazione a sinistra. In questa schermata viene visualizzata una tabella con i dettagli degli eventuali certificati SSL esistenti.

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. Fai clic su **Aggiungi certificato SSL** aprire **Aggiungi certificato SSL** finestra di dialogo.

   * Immetti un nome per il certificato in **Nome certificato**. Può essere un nome qualsiasi che ti aiuti a fare riferimento facilmente al certificato.
   * Incolla **Certificato**, **Chiave privata** e **Catena di certificati** nei rispettivi campi. Utilizza l’icona Incolla a destra della casella di input.
Tutti e tre i campi non sono facoltativi e devono essere inclusi.

      ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)


      >[!NOTE]
      >Vengono visualizzati tutti gli errori rilevati. È necessario risolvere tutti gli errori prima di salvare il certificato. Fai riferimento a [Errori di certificato](#certificate-errors) per ulteriori informazioni sulla gestione degli errori comuni.

1. Fai clic su **Salva** per inviare il certificato. Viene visualizzata come una nuova riga nella tabella.

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

## Errori di certificato {#certificate-errors}

### Criterio certificato {#certificate-policy}

Se viene visualizzato l&#39;errore &quot;La policy del certificato deve essere conforme a EV o OV e non a DV policy&quot;, controllare la policy del certificato.

Normalmente i tipi di certificato sono identificati dai valori OID incorporati nei criteri. Questi OID sono univoci e quindi la conversione di un certificato in un modulo di testo e la ricerca dell’OID confermerà che il certificato corrisponde.

Puoi visualizzare i dettagli del certificato come segue.

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

Queste tabelle forniscono pattern di identificazione.

| Pattern | Tipo di certificato | Accettabile |
|---|---|---|
| `2.23.140.1.2.1` | DV | No |
| `2.23.140.1.2.2` | OV | Sì |
| `2.23.140.1.2.3` e `TLS Web Server Authentication` | IV cert con permesso di utilizzo per https | Sì |

`grep`per verificare i pattern, puoi confermare il tipo di certificato.

```shell
# "EV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.1" -B5

# "OV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.2" -B5

# "DV Policy - Not Accepted"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.1" -B5
```

### Ordine di certificazione corretto {#correct-certificate-order}

Il motivo più comune per cui una distribuzione di certificati non riesce è che i certificati intermedi o a catena non sono nell’ordine corretto. In particolare, i file di certificato intermedi devono terminare con il certificato principale o il certificato più vicino alla radice ed essere in ordine decrescente dal `main/server` certificato alla radice.

È possibile determinare l&#39;ordine dei file intermedi utilizzando il seguente comando:

`openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout`

Puoi verificare che la chiave privata e `main/server` corrispondenza del certificato utilizzando i seguenti comandi:

`openssl x509 -noout -modulus -in certificate.pem | openssl md5`

`openssl rsa -noout -modulus -in ssl.key | openssl md5`

>[!NOTE]
>L&#39;output di questi due comandi deve essere esattamente lo stesso. Se non riesci a individuare una chiave privata corrispondente alla tua `main/server` certificato: devi reimpostare il certificato generando una nuova CSR e/o richiedendo un certificato aggiornato dal fornitore SSL.

### Date di validità del certificato {#certificate-validity-dates}

Cloud Manager prevede che il certificato SSL sia valido per almeno 90 giorni nel futuro. È necessario verificare la validità della catena di certificati.
