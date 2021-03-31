---
title: Frammenti di contenuto - Browser di configurazione
description: Scopri come abilitare alcune funzionalità dei frammenti di contenuto nel browser di configurazione per sfruttare AEM potenti funzionalità di distribuzione headless.
feature: Frammenti di contenuto
role: Professionista
translation-type: tm+mt
source-git-commit: 6fa911f39d707687e453de270bc0f3ece208d380
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 20%

---


# Frammenti di contenuto - Browser di configurazione{#content-fragments-configuration-browser}

Scopri come abilitare alcune funzionalità dei frammenti di contenuto nel browser di configurazione per sfruttare AEM potenti funzionalità di distribuzione headless.

## Abilita la funzionalità dei frammenti di contenuto per la tua istanza {#enable-content-fragment-functionality-instance}

Prima di utilizzare Frammenti di contenuto è necessario utilizzare il **Browser configurazioni** per abilitare:

* **Modelli per frammenti di contenuto**  - obbligatori
* **Query persistenti GraphQL**  - facoltativo

>[!CAUTION]
>
>Se non abiliti l’opzione **Modelli di frammento di contenuto** , l’opzione **Crea** non sarà disponibile per la creazione di nuovi modelli.

Per abilitare la funzionalità dei frammenti di contenuto è necessario:

* Abilita l’utilizzo della funzionalità dei frammenti di contenuto tramite il browser di configurazione
* Applica la configurazione alla cartella Assets

### Abilita funzionalità frammento di contenuto nel browser di configurazione {#enable-content-fragment-functionality-in-configuration-browser}

Per [utilizzare alcune funzionalità dei frammenti di contenuto](#creating-a-content-fragment-model) **è necessario** prima abilitarle tramite il **Browser di configurazione**:

>[!NOTE]
>
>Per ulteriori dettagli, consulta anche [Browser di configurazione:](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!CAUTION]
>
>Le sottoconfigurazioni (una configurazione nidificata all’interno di una configurazione) non sono supportate per l’uso con Frammenti di contenuto.

1. Accedi a **Strumenti**, **Generali**, quindi apri **Browser configurazioni**.

1. Utilizza **Crea** per aprire la finestra di dialogo in cui:

   1. Specifica un **titolo**.
   1. Per attivarne l&#39;uso, seleziona
      * **Modelli per frammenti di contenuto**
      * **Query persistenti GraphQL**

      ![Definire la configurazione](assets/cfm-conf-01.png)


1. Seleziona **Crea** per salvare la definizione.

<!-- 1. Select the location appropriate to your website. -->

### Applica la configurazione alla cartella delle risorse {#apply-the-configuration-to-your-assets-folder}

Quando la configurazione **global** è abilitata per la funzionalità di frammento di contenuto, si applica a qualsiasi cartella Assets.

Per utilizzare altre configurazioni con una cartella Risorse simile, ovvero escludendo il formato globale, è necessario definire la connessione. Questa operazione viene eseguita selezionando l’appropriata **Configurazione** nella scheda **Cloud Services** della finestra **Proprietà cartella** della cartella specifica.

![Applica configurazione](assets/cfm-conf-02.png)