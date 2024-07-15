---
title: Certificati convalidati dal dominio (DV)
description: Scopri come gestire i certificati convalidati dal dominio (DV) in Cloud Manager.
exl-id: 7f2c71b6-15c3-4919-9f51-a3e26d0d48d4
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 8%

---

# Certificati convalidati dal dominio (DV) {#domain-validated-certificates}

Scopri come gestire i certificati convalidati dal dominio (DV) in Cloud Manager.

>[!NOTE]
>
>Questa funzione è disponibile solo per [il programma di adozione anticipata.](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)

## Introduzione {#introduction}

Cloud Manager consente di generare e gestire in autonomia un certificato SSL (DV) convalidato dal dominio. Questo offre la soluzione più veloce, facile e conveniente per creare un sito web sicuro per il vostro business online.

I certificati convalidati dal dominio sono disponibili per [programmi sandbox e di produzione.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

## Aggiunta di un dominio personalizzato {#adding-domain}

Per aggiungere un certificato DV (Domain Validated), devi prima configurare il dominio personalizzato. Il processo è sostanzialmente lo stesso descritto nel documento [Introduzione ai nomi di dominio personalizzati.](/help/implementing/cloud-manager/custom-domain-names/introduction.md) Tuttavia questa funzionalità è stata leggermente espansa.

1. Durante la verifica del dominio, puoi scegliere di utilizzare i certificati gestiti da Adobe o autogestiti con il dominio. Scegliere **Adobe certificato gestito** per aggiungere un certificato DV in un secondo momento.

   ![Scegli gestito da Adobe](assets/verify-domain-dialog.png)

1. Per utilizzare un Adobe di certificato gestito, è necessario aggiungere un record CNAME al DNS come descritto nella finestra di dialogo **Verifica dominio**.

   ![Aggiungi voce CNAME](assets/verify-domain-dialog-adobe-managed.png)

1. Dopo aver creato il dominio, tocca o fai clic sul pulsante con i puntini di sospensione nell&#39;elenco dei domini e seleziona **Verifica** per verificare il dominio.

   ![Verifica dominio](assets/verify-domain.png)

## Aggiunta di un certificato DV {#adding}

Dopo aver configurato correttamente il dominio, per aggiungere un certificato DV tocca o fai clic sul pulsante **Aggiungi certificato SSL** nella finestra Certificati SSL.

![Aggiunta di un certificato controller di dominio](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)

1. Selezionare l&#39;opzione **Adobe gestito (DV)**.
1. Specificare il nome di dominio nell&#39;elenco a discesa **Seleziona domini**.
1. Tocca o fai clic su **Salva**.

Una volta aggiunto correttamente il certificato, nella finestra **Certificati SSL** verrà visualizzato uno stato in sospeso con un segno di avviso giallo al nome.

![Certificato DV in sospeso](assets/pending-dv-certificate.png)

Una volta rilasciato correttamente, il certificato avrà un segno di spunta verde sul suo nome nella finestra **Certificati SSL**.

![Certificato DV emesso](assets/issued-dv-certificate.png)

Per ulteriori informazioni sull&#39;aggiunta di certificati SSL e sulla finestra Certificati SSL, vedere il documento [Aggiunta di un certificato SSL.](add-ssl-certificate.md)

## Aggiungi configurazione CDN {#add-cdn}

Questo passaggio deve essere completato per configurare un dominio con SSL utilizzando Fastly CDN.

Per aggiungere una configurazione CDN utilizzando Cloud Manager, segui la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Seleziona la scheda **Configurazioni CDN** e tocca o fai clic su **Aggiungi** nella barra degli strumenti.

1. Nella finestra di dialogo **Configura CDN**, fornisci le informazioni necessarie.

   * Seleziona l&#39;**origine**. Può trattarsi di:
      * Un ambiente di Cloud Service
      * Un sito Edge Delivery Services
   * Seleziona il tipo di CDN.
   * Seleziona il dominio.
   * Seleziona il certificato SSL.
      * Obbligatorio solo per CDN gestiti da Adobe.

   ![Configura finestra di dialogo CDN](assets/configure-cdn-dialog.png)

>
>
>Ad Adobe, le CDN gestite con i certificati DV consentono solo i siti con convalida ACME.
