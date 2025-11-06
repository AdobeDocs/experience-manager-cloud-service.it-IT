---
title: Aggiungere un certificato SSL
description: Scopri come aggiungere un certificato SSL personalizzato o un certificato DV (convalida del dominio) gestito da Adobe utilizzando gli strumenti self-service di Cloud Manager.
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 6%

---


# Aggiungere un certificato SSL {#add-ssl-cert}

Scopri come aggiungere il tuo certificato SSL o il certificato DV (convalida del dominio) gestito da Adobe tramite Cloud

>[!NOTE]
>
>Se utilizzi un certificato SSL gestito dal cliente (OV/EV) e un provider CDN gestito dal cliente, puoi saltare l&#39;aggiunta di un certificato SSL e passare direttamente a [Aggiungi mappatura dominio](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md) quando è pronto.

Il provisioning di un certificato può richiedere diversi giorni. Pertanto, Adobe consiglia di eseguire il provisioning del certificato con largo anticipo rispetto a qualsiasi scadenza o data di pubblicazione, per evitare ritardi.

Per informazioni sull&#39;aggiornamento e la gestione dei certificati SSL in Cloud Manager, vedere [Gestione dei certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md).

In caso di problemi durante l&#39;aggiunta o la gestione dei certificati, vedere [Risoluzione degli errori relativi ai certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md).


## Prerequisiti {#prerequisites}

* Per aggiungere un certificato SSL, l&#39;utente deve avere il ruolo **Proprietario business** o **Responsabile dell&#39;implementazione**.
* Se stai installando un tuo certificato, consulta **Requisiti del certificato** in [Introduzione alla gestione dei certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements).

## Scelta del certificato SSL da aggiungere {#which-ssl-to-add}

Dopo [l&#39;aggiunta di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) in AEM Cloud Manager, il passaggio successivo dipende dalla scelta di utilizzare un certificato SSL gestito da Adobe (DV) (consigliato) o un certificato SSL gestito dal cliente (OV/EV).

* **Per un certificato SSL gestito da Adobe:**
   * Il processo di convalida del dominio viene eseguito dopo l’aggiunta e la verifica del dominio personalizzato in Cloud Manager.
   * È ora necessario [aggiungere un certificato SSL gestito da Adobe](#add-adobe-managed-ssl-cert).
Una volta aggiunto a Cloud Manager, attendi che Adobe rilasci e installi il certificato SSL DV per tuo conto.
   * Quando il certificato è attivo, il dominio personalizzato è pronto per l’uso.

* **Per un certificato SSL gestito dal cliente (OV/EV):**

   * Ottieni il tuo certificato SSL OV/EV da un’autorità di certificazione. Per ulteriori dettagli, controlla i [requisiti per i certificati SSL OV/EV gestiti dal cliente](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements).
   * Dopo aver acquisito il certificato, [aggiungi i dettagli del certificato SSL gestito dal cliente (OV/EV)](#add-customer-managed-ssl-cert) in Cloud Manager.
   * Una volta aggiunto, il nome di dominio personalizzato viene contrassegnato come verificato e viene applicato il certificato SSL.

In entrambi i casi, dopo la verifica e l’installazione del certificato, il dominio personalizzato è disponibile per un utilizzo sicuro nell’ambiente. Assicurarsi di [controllare regolarmente lo stato del dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) nell&#39;interfaccia di Cloud Manager per verificare che tutto funzioni come previsto.

Vedi anche [Introduzione ai certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md).

## Aggiungere un certificato SSL gestito (DV) di Adobe {#add-adobe-managed-ssl-cert}

Hai bisogno di assistenza per scegliere se utilizzare un certificato SSL gestito da Adobe (consigliato) o un certificato SSL gestito dal cliente con il tuo dominio? Vedi [Scelta del certificato SSL da aggiungere](#which-ssl-to-add)

**Per aggiungere un certificato SSL gestito (DV) di Adobe:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.
1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.
1. Nell&#39;angolo superiore sinistro della pagina fare clic su ![Mostra icona menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) per visualizzare il menu laterale.

1. Sotto l&#39;intestazione **Services**, fare clic su ![Blocca icona chiuso](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **Certificati SSL**.

   ![Aggiunta di un certificato SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Fare clic su **Aggiungi certificato SSL** nell&#39;angolo superiore destro della pagina Certificati SSL.

1. Nella finestra di dialogo **Aggiungi certificato SSL**, in base al [caso d&#39;uso particolare](#which-ssl-to-add), seleziona **Gestione Adobe (DV)**.

   ![Aggiungi un certificato DV](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)

1. Nel campo **Nome certificato** immettere un nome che si desidera associare al certificato SSL DV.

1. Nell&#39;elenco a discesa **Seleziona domini** selezionare uno o più domini verificati che si desidera associare al certificato SSL DV.
   * Nessun dominio da selezionare? In tal caso, devi innanzitutto [aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) e assicurarti che sia verificato prima di poter aggiungere un certificato SSL gestito da Adobe.
   * Dopo aver aggiunto un nome di dominio personalizzato, torna a questo argomento e ricomincia dal passaggio 1.

1. Nell’angolo inferiore a destra della finestra di dialogo, fai clic su **Salva**.

   Dopo il corretto rilascio, il certificato SSL viene visualizzato con un segno di spunta verde valido nella tabella **Certificati SSL**.

È stato aggiunto un certificato SSL DV gestito di Adobe per il progetto. Questo passaggio è spesso il primo a configurare un nome di dominio personalizzato.

Ora puoi aggiungere una [configurazione CDN](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md).

## Aggiungere un certificato SSL gestito dal cliente (OV/ED) {#add-customer-managed-ssl-cert}

<!-- IF THIS TOPIC GET UPDATED, REMEMBER TO UPDATE THE STEPS ALSO IN THE "MANAGE SSL CERTIFICATES TOPIC TOO -->

Hai bisogno di assistenza per scegliere se utilizzare un certificato SSL gestito da Adobe (consigliato) o un certificato SSL gestito dal cliente con il tuo dominio? Vedi [Scelta del certificato SSL da aggiungere](#which-ssl-to-add)

>[!IMPORTANT]
>
>Quando aggiungi o aggiorni un certificato SSL, non includere il nuovo certificato nella catena di certificati. L’inclusione di impedisce il completamento del caricamento.

**Per aggiungere un certificato SSL gestito dal cliente (OV/EV):**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Nell&#39;angolo superiore sinistro della pagina fare clic su ![Mostra icona menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) per visualizzare il menu laterale.

1. Sotto l&#39;intestazione **Services**, fare clic su ![Blocca icona chiuso](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **Certificati SSL**.

   ![Aggiunta di un certificato SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Fare clic su **Aggiungi certificato SSL** nell&#39;angolo superiore destro della pagina Certificati SSL.

1. Nella finestra di dialogo **Aggiungi certificato SSL**, in base al [caso d&#39;uso particolare](#which-ssl-to-add), seleziona **Gestione clienti (OV/EV)**.

1. Nel campo **Nome certificato** immettere un nome per il certificato.
Questo campo è solo a scopo informativo e può essere qualsiasi nome che ti aiuti a fare riferimento facilmente al certificato SSL.

1. Nei campi **Certificato**, **Chiave privata** e **Catena di certificati**, copia i valori richiesti dal certificato SSL OV o EV e incollali nei rispettivi campi nella finestra di dialogo.

   Vengono visualizzati tutti gli eventuali errori rilevati nei valori. Prima di poter salvare il certificato, è necessario risolvere tutti gli errori. Per ulteriori informazioni sulla risoluzione dei problemi relativi agli errori comuni, consulta [Errori relativi ai certificati](#certificate-errors).

   ![Finestra di dialogo Aggiungi certificato SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)|

1. Nell’angolo inferiore a destra della finestra di dialogo, fai clic su **Salva**.

   >[!NOTE]
   >
   >* Se hai selezionato **Certificato gestito dal cliente** mentre [aggiungi un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md), il dominio viene verificato ***dopo*** che il certificato SSL gestito dal cliente (OV/EV) è stato aggiunto e salvato. Vedi anche [Verifica lo stato di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#how-to).

   Dopo il corretto rilascio, il certificato SSL viene visualizzato con un segno di spunta verde nella tabella **Certificati SSL**.

Ora hai aggiunto un certificato SSL funzionante per il progetto. Questo passaggio è spesso il primo a configurare un nome di dominio personalizzato.

Ora puoi aggiungere una [configurazione CDN](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md).























<!--
## Add an SSL certificate {#add-ssl-cert}

1. Log into Cloud Manager at [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) and select the appropriate program.
1. On the **[My Programs](/help/implementing/cloud-manager/navigation.md#my-programs)** console, select the program.
1. In the upper-left corner of the page, click ![Show menu icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) to reveal the side menu. 
1. Under the **Services** heading, click ![Lock closed icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **SSL Certificates**. 

   ![Adding an SSL certificate](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Near the upper-right corner of the SSL Certificates page, click **Add SSL Certificate**.

1. In the **Add SSL certificate** dialog box, based on [your particular use case](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md), do one of the following:

    | | Use case | Steps |
    | --- | --- | --- |
    | 1 | **Add an Adobe managed (DV) certificate** | **To add an Adobe managed (DV) SSL certificate:**<br>a. In the **Add SSL Certificate** dialog box, select the certificate type **Adobe managed (DV)**.<br>![Add a DV certificate](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)<br>b. In the **Certificate name** field, enter a name you want associated with the certificate.<br>c. In the **Select domains** drop-down list, select one or more domains that you want associated with the DV SSL certificate.<br>No domains to select? If so, it means that you must first add a custom domain name and ensure it is verified before you can add an SSL certificate. See [Add a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). When you are finished adding a custom domain name, return to this topic and begin at step 1 again.<br>d. Continue to step 7. |
    | 2 | **Add a customer managed (OV/EV) certificate** | **To add a customer managed (OV/EV) SSL certificate:**<br>a. In the **Add SSL Certificate** dialog box, select the certificate type **Customer managed (OV/EV)**.<br>b. In the **Certificate name** field, enter a name for your certificate. This field is for informational purposes only and can be any name that helps you reference your SSL certificate easily.<br>c. In the **Certificate**, **Private key**, and **Certificate chain** fields, paste the required values into their respective fields.<br>![Add SSL certificate dialog box](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)<br>Any detected errors in values are displayed. Before you can save your certificate, you must address all errors. See [Certificate Errors](#certificate-errors) to learn more about troubleshooting common errors.<br>d. Continue to step 7. | 

1. In the lower-right corner of the dialog box, click **Save**.

    >[!NOTE]
    >
    >* If you selected **Adobe managed certificate** while [adding a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md), the domain is verified with the added certificate when the custom domain is added. 
    >
    >* If you selected **Customer managed certificate** while [adding a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md), the domain is verified ***after*** the customer managed (OV/EV) SSL certificate is added and saved. See also [Check the status of a custom domain name](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#how-to).

    After the SSL certificate is successfully issued, it is displayed with a green verified check mark in the **SSL Certificates** table. 

    You now have added a working SSL certificate for your project. This step is often the first to set up a custom domain name. 
    

* To learn about updating and managing your SSL certificates in Cloud Manager, see [Manage SSL certificates](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md).

* If you are having issues adding or managing your certificates, see [Troubleshoot SSL certificate errors](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md). -->
