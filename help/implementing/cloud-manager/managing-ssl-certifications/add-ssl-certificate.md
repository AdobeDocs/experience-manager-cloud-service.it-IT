---
title: Aggiungere un certificato SSL
description: Scopri come aggiungere un certificato SSL personalizzato o un certificato DV (convalida del dominio) gestito da Adobe utilizzando gli strumenti self-service di Cloud Manager.
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 493c5729c3107f151685a243006b17196b74c1bd
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 6%

---


# Aggiungere un certificato SSL {#add-ssl-cert}

Scopri come aggiungere un certificato SSL personalizzato o un certificato DV (convalida del dominio) gestito da Adobe utilizzando Cloud

>[!TIP]
>
>Il provisioning di un certificato può richiedere alcuni giorni. Di conseguenza, l’Adobe consiglia che, se stai fornendo un certificato personalizzato, questo venga fornito con largo anticipo rispetto a qualsiasi scadenza o data di pubblicazione.

## Prerequisiti {#prerequisites}

* Per aggiungere un certificato, l&#39;utente deve essere membro del ruolo **Proprietario business** o **Responsabile dell&#39;implementazione**.
* Se stai installando un certificato personalizzato, assicurati di rivedere **Requisiti del certificato** in [Introduzione alla gestione dei certificati SSL.](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements)

## Aggiunta di un certificato SSL {#add-certificate}

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona il programma appropriato.
1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.
1. Nell&#39;angolo superiore sinistro della pagina fare clic su ![Mostra icona menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) per visualizzare il menu laterale.
1. Sotto l&#39;intestazione **Services**, fare clic su ![Blocca icona chiuso](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **Certificati SSL**.

   ![Aggiunta di un certificato SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Fare clic su **Aggiungi certificato SSL** nell&#39;angolo superiore destro della pagina Certificati SSL.

1. Nella finestra di dialogo **Aggiungi certificato SSL**, in base al [caso d&#39;uso particolare](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md), eseguire una delle operazioni seguenti:

   | | Caso d’uso | Passaggi |
   | --- | --- | --- |
   | 1 | **Aggiungere un Adobe di certificato gestito (DV)** | **Per aggiungere un Adobe di certificato gestito (DV):**<br> a. Nella finestra di dialogo **Aggiungi certificato SSL**, selezionare il tipo di certificato **Adobe gestito (DV)**.<br>![Aggiungere un certificato DV](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)<br>b. Nel campo **Nome certificato** immettere un nome che si desidera associare al certificato.<br>c. Nell&#39;elenco a discesa **Seleziona domini** selezionare uno o più domini da associare al certificato DV.<br>Nessun dominio da selezionare? In tal caso, devi aggiungere un dominio personalizzato. Vedere [Aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). Dopo aver aggiunto un nome di dominio personalizzato, torna a questo argomento e ricomincia dal passaggio 1.<br> d. Continuare con il passaggio 7. |
   | 2 | **Aggiungere un certificato gestito dal cliente (OV/EV)** | **Per aggiungere un certificato gestito dal cliente (OV/EV):**<br> a. Nella finestra di dialogo **Aggiungi certificato SSL**, selezionare il tipo di certificato **Gestione clienti (OV/EV)**.<br> b. Nel campo **Nome certificato** immettere un nome per il certificato. Questo campo è solo a scopo informativo e può essere qualsiasi nome che ti aiuti a fare riferimento facilmente al certificato.<br>c. Nei campi **Certificato**, **Chiave privata** e **Catena certificati**, incolla i valori richiesti nei rispettivi campi.<br>![Finestra di dialogo Aggiungi certificato SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)<br>Vengono visualizzati tutti gli errori rilevati nei valori. Prima di poter salvare il certificato, è necessario risolvere tutti gli errori. Per ulteriori informazioni sulla risoluzione dei problemi relativi agli errori comuni, consulta [Errori relativi ai certificati](#certificate-errors).<br> d. Continuare con il passaggio 7. |

1. Nell’angolo inferiore a destra della finestra di dialogo, fai clic su **Salva**.

Dopo il corretto rilascio, il certificato viene visualizzato con un segno di spunta verde nella tabella **Certificati SSL**.

Ora hai aggiunto un certificato SSL funzionante per il progetto. Questo passaggio è spesso il primo a configurare un nome di dominio personalizzato.

* Per impostare un nome di dominio personalizzato, vedere [Aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).
* Per informazioni sull&#39;aggiornamento e la gestione dei certificati SSL in Cloud Manager, vedere [Gestione dei certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md).

>[!TIP]
>
>In caso di problemi durante l&#39;aggiunta o la gestione dei certificati, vedere il documento [Risoluzione dei problemi relativi agli errori dei certificati SSL.](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md)
