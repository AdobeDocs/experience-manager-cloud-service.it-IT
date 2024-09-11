---
title: Aggiungi una configurazione CDN
description: Scopri come aggiungere una configurazione CDN per un sito Edge Delivery o un ambiente Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 672513d7-ee0a-4f6e-9ef0-7a41fabbaf9a
source-git-commit: dd696580758e7ab9a5427d47fda4275f9ad7997f
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 8%

---

# Aggiungi una configurazione CDN {#add-cdn}

Per configurare un dominio con SSL è necessario completare l’aggiunta di una configurazione CDN.

>
>
>Ad Adobe, le CDN gestite con i certificati DV consentono solo i siti con convalida ACME.

**Per aggiungere una configurazione CDN:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Fai clic su **Configurazioni CDN**.

1. Fai clic su **Aggiungi** nell&#39;angolo superiore destro della pagina Configurazioni CDN.

   ![Finestra di dialogo Configura CDN](/help/implementing/cloud-manager/assets/configure-cdn-dialog.png)

1. Nella finestra di dialogo **Configura CDN**, fornisci le informazioni necessarie.

   * Nell&#39;elenco a discesa **Origin** eseguire una delle operazioni seguenti:
      * **Siti:** Selezionare un sito Edge Delivery Services.
      * **Ambienti:** Seleziona un ambiente di Cloud Service.
         * **Livello:** Selezionare un livello Web **Publish** o **Anteprima** per l&#39;ambiente selezionato.
   * Seleziona il tipo di CDN: **Adobe CDN gestito** o **altro provider CDN**.
   * Seleziona il dominio.
   * Seleziona il certificato SSL. Obbligatorio solo se hai selezionato **Adobe CDN gestito** come tipo di CDN.

1. Fai clic su **Salva**.
