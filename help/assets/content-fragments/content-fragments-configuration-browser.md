---
title: Frammenti di contenuto - Browser di configurazione
description: Scoprite come abilitare determinate funzionalità di frammento di contenuto nel browser di configurazione.
translation-type: tm+mt
source-git-commit: c821baff208e563009e68f51700555ea1d516886
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 19%

---


# Frammenti di contenuto - Browser di configurazione{#content-fragments-configuration-browser}

>[!CAUTION]
>
>L&#39;API AEM GraphQL, per la distribuzione dei frammenti di contenuto, verrà rilasciata all&#39;inizio del 2021.
>
>La documentazione correlata è già disponibile a scopo di anteprima.

## Abilita funzionalità frammento di contenuto per l&#39;istanza {#enable-content-fragment-functionality-instance}

Prima di utilizzare i frammenti di contenuto è necessario utilizzare il **browser di configurazione** per attivare:

* **Modelli**  di frammenti di contenuto - obbligatori
* **GraphQL - Query**  persistenti - facoltative

>[!CAUTION]
>
>Se non si abilita l&#39;opzione **Modelli di frammenti di contenuto**, l&#39;opzione **Crea** non sarà disponibile per la creazione di nuovi modelli.

Per abilitare la funzionalità dei frammenti di contenuto è necessario:

* Abilitare l&#39;utilizzo della funzionalità dei frammenti di contenuto tramite il browser di configurazione
* Applica la configurazione alla cartella Risorse

### Abilitare la funzionalità dei frammenti di contenuto nel browser di configurazione {#enable-content-fragment-functionality-in-configuration-browser}

Per [utilizzare alcune funzionalità di frammento di contenuto](#creating-a-content-fragment-model) è necessario **innanzitutto attivarle mediante il** browser di configurazione **:**

>[!NOTE]
>
>Per ulteriori dettagli, vedere anche [Browser di configurazione:](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!CAUTION]
>
>Le sottoconfigurazioni (una configurazione nidificata all&#39;interno di una configurazione) non sono supportate per l&#39;uso con i frammenti di contenuto.

1. Accedi a **Strumenti**, **Generali**, quindi apri **Browser configurazioni**.

1. Utilizzate **Create** per aprire la finestra di dialogo in cui:

   1. Specificare un **Titolo**.
   1. Per attivarne l&#39;uso, seleziona
      * **Modelli per frammenti di contenuto**
      * **GraphQL - Query persistenti**

      ![Definisci configurazione](assets/cfm-conf-01.png)


1. Selezionare **Crea** per salvare la definizione.

<!-- 1. Select the location appropriate to your website. -->

### Applica la configurazione alla cartella delle risorse {#apply-the-configuration-to-your-assets-folder}

Quando la configurazione **global** è abilitata per la funzionalità di frammento di contenuto, viene applicata a qualsiasi cartella Assets.

Per utilizzare altre configurazioni con una cartella Risorse simile, ovvero escludendo il formato globale, è necessario definire la connessione. Questa operazione viene eseguita selezionando l’appropriata **Configurazione** nella scheda **Cloud Services** della finestra **Proprietà cartella** della cartella specifica.

![Applica configurazione](assets/cfm-conf-02.png)