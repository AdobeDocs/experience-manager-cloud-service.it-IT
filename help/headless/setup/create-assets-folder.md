---
title: 'Creazione di una cartella di risorse: configurazione headless'
description: Utilizza i modelli per frammenti di contenuto di AEM per definire la struttura dei frammenti di contenuto, che sta alla base dei contenuti headless.
exl-id: 9a156a17-8403-40fc-9bd0-dd82fb7b2235
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 38a4bf89e099432163163e90e08aa0f47407724f
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 77%

---

# Creazione di una cartella di risorse: configurazione headless {#creating-an-assets-folder}

Utilizza i modelli per frammenti di contenuto di AEM per definire la struttura dei frammenti di contenuto, che sta alla base dei contenuti headless. I frammenti di contenuto vengono poi memorizzati nelle cartelle di risorse.

## Cos’è una cartella di risorse? {#what-is-an-assets-folder}

[Dopo aver creato i modelli per frammenti di contenuto](create-content-model.md) che definiscono la struttura per i futuri frammenti di contenuto, è ora di creare alcuni frammenti.

Tuttavia, è necessario innanzitutto creare una cartella di risorse in cui memorizzarli.

Le cartelle di risorse vengono utilizzate per [organizzare le risorse di contenuti tradizionali](/help/assets/manage-digital-assets.md) come immagini e video, insieme ai frammenti di contenuto.

## Creare e configurare una cartella di Assets {#create-and-configure-an-assets-folder}

Di solito, un amministratore deve creare cartelle solo occasionalmente, per organizzare i contenuti al momento della creazione. Usa la console Assets per creare la nuova cartella.

Una volta creata, devi applicare la [configurazione](/help/headless/setup/create-configuration.md) alla cartella. Per ulteriori dettagli, vedere [Applicare la configurazione alla cartella](/help/sites-cloud/administering/content-fragments/setup.md#apply-the-configuration-to-your-folder).

Puoi creare ulteriori sottocartelle all’interno della cartella creata. Le sottocartelle ereditano la **configurazione cloud** della cartella principale. Tuttavia, questo può essere ignorato se desideri utilizzare modelli di un’altra configurazione.

Se utilizzi una struttura del sito localizzata, puoi [creare una directory principale della lingua](/help/assets/translate-assets.md) al di sotto della nuova cartella.

## Passaggi successivi {#next-steps}

Dopo aver creato una cartella per i frammenti di contenuto, puoi passare alla quarta parte della guida introduttiva e [creare frammenti di contenuto](create-content-fragment.md).

>[!TIP]
>
>Per informazioni complete sulla gestione dei Frammenti di contenuto, consulta la sezione [Documentazione sui Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/overview.md).
