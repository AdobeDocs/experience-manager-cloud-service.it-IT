---
title: Certificati DV (Domain Validated)
description: Scopri come gestire i certificati convalidati dal dominio (DV) in Cloud Manager.
source-git-commit: 5baeb4012e5aa82a8cd8710b18d9164583ede0bd
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 6%

---


# Certificati DV (Domain Validated) {#domain-validated-certificates}

Scopri come gestire i certificati convalidati dal dominio (DV) in Cloud Manager.

>[!NOTE]
>
>Questa funzione è disponibile solo per [il programma di adozione anticipata.](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)

## Introduzione {#introduction}

Cloud Manager consente di generare e gestire in autonomia un certificato SSL convalidato dal dominio (DV). Questo offre la soluzione più veloce, facile e conveniente per creare un sito web sicuro per il vostro business online.

I certificati convalidati dal dominio sono disponibili per entrambi [programmi di produzione e sandbox.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

## Aggiunta di un dominio personalizzato {#adding-domain}

Per aggiungere un certificato DV (Domain Validated), devi prima configurare il dominio personalizzato. Il processo è sostanzialmente lo stesso descritto nel documento [Introduzione ai nomi di dominio personalizzati.](/help/implementing/cloud-manager/custom-domain-names/introduction.md) Tuttavia, tale funzionalità è stata leggermente ampliata.

1. Durante la verifica del dominio, puoi scegliere di utilizzare i certificati gestiti da Adobe o autogestiti con il dominio. Scegli **Adobe certificato gestito** per aggiungere un certificato DV in un secondo momento.

   ![Scegli gestito da Adobe](assets/verify-domain-dialog.png)

1. Per utilizzare un certificato gestito di Adobe, devi aggiungere un record CNAME al DNS come descritto nella **Verifica dominio** .

   ![Aggiungi voce CNAME](assets/verify-domain-dialog-adobe-managed.png)

1. Una volta creato il dominio, tocca o fai clic sul pulsante con i puntini di sospensione nell’elenco dei domini e seleziona **Verifica** per verificare il dominio.

   ![Verifica dominio](assets/verify-domain.png)

## Aggiunta di un certificato DV {#adding}

Dopo aver configurato correttamente il dominio, per aggiungere un certificato DV tocca o fai clic sul pulsante **Aggiungi certificato SSL** nella finestra Certificati SSL.

![Aggiunta di un certificato controller di dominio](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)

1. Seleziona l’opzione **Adobe gestito (DV)**.
1. Specifica il nome di dominio nel **Seleziona domini** a discesa.
1. Tocca o fai clic su **Salva**.

Una volta aggiunto correttamente, il certificato avrà uno stato in sospeso con un segno di avvertenza giallo al suo nome nel **Certificati SSL** finestra.

![Certificato DV in sospeso](assets/pending-dv-certificate.png)

Una volta rilasciato, il certificato sarà contrassegnato da un segno di spunta verde nel campo **Certificati SSL** finestra.

![Certificato DV rilasciato](assets/issued-dv-certificate.png)

Per ulteriori informazioni sull’aggiunta di certificati SSL e sulla finestra Certificati SSL, consulta il documento [Aggiunta di un certificato SSL.](add-ssl-certificate.md)

## Aggiungi configurazione CDN {#add-cdn}

Questo passaggio deve essere completato per configurare un dominio con SSL utilizzando Fastly CDN.

Per aggiungere una configurazione CDN tramite Cloud Manager, segui la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Seleziona la **Configurazioni CDN** e tocca o fai clic su **Aggiungi** nella barra degli strumenti.

1. In **Configura CDN** fornisci le informazioni necessarie.

   * Seleziona la **Origine**. Può trattarsi di:
      * Un ambiente di Cloud Service
      * Un sito Edge Delivery Services
   * Seleziona il tipo di CDN.
   * Seleziona il dominio.
   * Seleziona il certificato SSL.
      * Obbligatorio solo per CDN gestiti da Adobe.

   ![Finestra di dialogo Configura CDN](assets/configure-cdn-dialog.png)

>
>
>Ad Adobe, le CDN gestite con i certificati DV consentono solo i siti con convalida ACME.
