---
title: Aggiungere un certificato SSL
description: Scopri come aggiungere un certificato SSL o DV (Domain Validation) personalizzato utilizzando gli strumenti self-service di Cloud Manager.
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 3aec9d13e2eb4bbc9a972e28195a6f43e92c1842
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 22%

---


# Aggiungere un certificato SSL

Scopri come aggiungere un certificato SSL gestito dal cliente o un certificato DV (convalida del dominio) generato e gestito da un Adobe utilizzando gli strumenti self-service di Cloud Manager.


## Aggiungere un certificato SSL o DV {#adding-an-ssl-certificate}

Il provisioning di un certificato può richiedere alcuni giorni. Di conseguenza, l’Adobe consiglia di eseguire il provisioning del certificato con largo anticipo rispetto a qualsiasi scadenza o data di pubblicazione.

Controlla i **requisiti del certificato** in [Introduzione alla gestione dei certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md#requirements) per assicurarti che AEM as a Cloud Service supporti il certificato che desideri aggiungere.

Per completare l&#39;attività, l&#39;utente deve avere il ruolo **Proprietario business** o **Responsabile dell&#39;implementazione**.

>[!NOTE]
>
>Ai clienti non è consentito caricare certificati DV (convalida dominio).

**Per aggiungere un certificato SSL o DV:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Dalla pagina **Panoramica**, passa alla schermata **Ambienti**.

1. Nel pannello di navigazione a sinistra, in **Servizi**, fai clic su **Certificati SSL**. Se il pannello di navigazione a sinistra non è visualizzato come nell’immagine seguente, potrebbe essere necessario fare clic sull’icona con l’hamburger nell’angolo in alto a sinistra.

   ![Aggiunta di un certificato SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Fai clic su **Aggiungi certificato SSL** nell&#39;angolo superiore destro della pagina.

1. Nella finestra di dialogo **Aggiungi certificato SSL**, in base al [caso d&#39;uso particolare](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md), eseguire una delle operazioni seguenti:

   | | Caso d’uso | Passaggi |
   | --- | --- | --- |
   | 1 | **Aggiungere un Adobe di certificato gestito (DV)** | **Per aggiungere un Adobe di certificato gestito (DV):**<br> a. Selezionare il tipo di certificato **Adobe gestito (DV)**.<br>![Aggiungere un certificato DV](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)<br>b. Nell&#39;elenco a discesa **Seleziona domini** selezionare uno o più domini da associare al certificato DV.<br>Nessun dominio da selezionare? In tal caso, devi aggiungere un dominio personalizzato. Vedere [Aggiungere un dominio personalizzato](#add-custom-domain). Dopo aver aggiunto un nome di dominio personalizzato, torna a questo argomento e ricomincia dal passaggio 1.<br> d. Continuare con il passaggio 7. |
   | 2 | **Aggiungere un certificato gestito dal cliente (OV/EV)** | **Per aggiungere un certificato gestito dal cliente (OV/EV):**<br> a. Selezionare il tipo di certificato **OV/EV gestito dal cliente**.<br> b. Nel campo **Nome certificato** immettere un nome per il certificato. Questo campo è solo a scopo informativo e può essere qualsiasi nome che ti aiuti a fare riferimento facilmente al certificato.<br>c. Nei campi **Certificato**, **Chiave privata** e **Catena certificati**, incolla i valori richiesti nei rispettivi campi.<br>![Finestra di dialogo Aggiungi certificato SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)<br>Vengono visualizzati tutti gli errori rilevati nei valori. Prima di poter salvare il certificato, è necessario risolvere tutti gli errori. Per ulteriori informazioni sulla risoluzione dei problemi relativi agli errori comuni, consulta [Errori relativi ai certificati](#certificate-errors).<br> d. Continuare con il passaggio 7. |

<!--
    **Add an SSL certificate:**
    1. Select the certificate type **Customer managed (OV/EV)**.
    1. In **Certificate name** field, enter a name for your certificate. This field is for informational purposes only and can be any name that helps you reference your certificate easily.
    1. In the **Certificate**, **Private key**, and **Certificate chain** fields, paste the required values into their respective fields.

        ![Add SSL certificate dialog box](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)
  
    Any detected errors in values are displayed. Before you can save your certificate, you must address all errors. See [Certificate errors](#certificate-errors) to learn more about troubleshooting common errors.

    **Add a DV certificate:**
    1. Select the certificate type **Adobe managed (DV)**.

        ![Adding a DC certificate](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)

    1. In the **Select domains** drop-down list, select one or more domains that you want associated with the DV certificate.

        No domains to select? If so, it means that you must add a custom domain. See [Add a custom domain](#add-custom-domain). When you are finished, resume the steps from the beginning again. -->

1. Nell&#39;angolo inferiore destro della finestra di dialogo fare clic su **Salva**.

   Dopo il corretto rilascio, il certificato mostra un segno di spunta verde, come mostrato nell’immagine precedente

   ![Certificato DV emesso](assets/issued-dv-certificate.png)

### Aggiungere un dominio personalizzato {#add-custom-domain}

Prima di poter aggiungere un Adobe di certificato DV (Domain Validated) generato e gestito, è necessario aggiungere un dominio personalizzato. Il processo per eseguire questa operazione è quasi lo stesso descritto in [Introduzione ai nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/introduction.md) e [Aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). Tuttavia, tale funzionalità è ora leggermente espansa, come descritto di seguito.

1. Quando si aggiunge un nome di dominio personalizzato, nella finestra di dialogo **Verifica dominio** selezionare un **Adobe di certificato gestito**.

   ![Scegli gestito da Adobe](assets/verify-domain-dialog.png)

1. Nella finestra di dialogo **Verifica dominio**, aggiungi un record di verifica CNAME al DNS.

   ![Aggiungi voce CNAME](assets/verify-domain-dialog-adobe-managed.png)

1. Dopo aver creato il dominio, fare clic sul pulsante con i puntini di sospensione nell&#39;elenco dei domini e selezionare **Verifica** per verificare il dominio.

   ![Verifica dominio](assets/verify-domain.png)

1. Riprendi l&#39;attività [Aggiungi un certificato DV](#adding-an-ssl-certificate).

### Risoluzione dei problemi relativi ai certificati {#certificate-errors}

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

## Passaggi successivi {#next-steps}

Ora hai aggiunto un certificato SSL funzionante per il progetto. Questo passaggio è spesso il primo a configurare un nome di dominio personalizzato.

* Per impostare un nome di dominio personalizzato, vedere [Aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).
* Per informazioni sull&#39;aggiornamento e la gestione dei certificati SSL in Cloud Manager, vedere [Gestione dei certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md).
