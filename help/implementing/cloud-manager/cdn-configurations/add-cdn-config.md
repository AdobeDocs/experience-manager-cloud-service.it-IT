---
title: Aggiungi una configurazione CDN
description: Scopri come aggiungere una configurazione CDN per un sito Edge Delivery o un ambiente Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 672513d7-ee0a-4f6e-9ef0-7a41fabbaf9a
source-git-commit: bc9aa376a402a55191e153f662262ff65df32f5e
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 7%

---


# Aggiungi una configurazione CDN {#add-cdn}

Per collegare un dominio con un certificato SSL sulla rete CDN gestita dall’Adobe all’interno del programma, è necessario aggiungere una configurazione CDN (Content Delivery Network).

Ad Adobe, le CDN gestite, quando si utilizzano certificati DV, sono consentiti solo i siti con convalida ACME.

>[!IMPORTANT]
>
>Hai [aggiunto un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) e [aggiunto rispettivamente un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)? In caso contrario, è necessario completare queste due attività prima di poter aggiungere una configurazione CDN.

**Per aggiungere una configurazione CDN:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nel pannello di navigazione a sinistra, in **Servizi**, fai clic su **Configurazioni CDN**.

1. Fai clic su **Aggiungi** nell&#39;angolo superiore destro della pagina Configurazioni CDN.

   ![Finestra di dialogo Configura CDN](/help/implementing/cloud-manager/assets/configure-cdn-dialog.png)

1. Nella finestra di dialogo **Configura CDN**, nell&#39;elenco a discesa **Origin**, selezionare una delle opzioni seguenti:

   | Origine | Descrizione |
   | --- | --- |
   | Sites | Seleziona un sito Edge Delivery. |
   | Ambiente | Seleziona un ambiente di Cloud Service specifico di cui desideri eseguire il targeting all’interno della configurazione AEM.<br>Nell&#39;elenco a discesa **Livello**, selezionare una delle opzioni seguenti:<br>· Selezionare **Publish** per impostare come destinazione un ambiente di produzione live in cui il contenuto viene distribuito agli utenti finali.<br>· Selezionare **Anteprima** per gli ambienti di staging o non di produzione in cui si esegue il test delle modifiche prima che vengano pubblicate. |

1. Seleziona il tipo di CDN e la configurazione associata selezionando una delle seguenti opzioni:

   | Tipo CDN | Dettagli configurazione |
   | --- | --- |
   | CDN gestita da Adobe | In **Dettagli configurazione** eseguire le operazioni seguenti:<br>a. Nell&#39;elenco a discesa **Dominio** selezionare il nome di dominio che si desidera utilizzare.<br>Nessun dominio verificato disponibile nell&#39;elenco a discesa? Vedere [Aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).<br> b. Nell&#39;elenco a discesa **Certificato SSL** selezionare il certificato che si desidera utilizzare.<br>Nessun certificato SSL disponibile nell&#39;elenco a discesa? Vedi [Aggiungere un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md). |
   | Altro provider CDN | Seleziona questa opzione se utilizzi un provider CDN personalizzato e non la rete CDN gestita dall’Adobe disponibile.<br>In **Dettagli configurazione**, nell&#39;elenco a discesa **Dominio**, selezionare il nome di dominio che si desidera utilizzare.<br>Nessun dominio verificato disponibile nell&#39;elenco a discesa? Vedere [Aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |

1. Fai clic su **Salva**.
