---
title: Configurare un account alias società Dynamic Media
description: Scopri come configurare un account alias aziendale in Dynamic Media.
contentOwner: Rick Brough
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User,Admin
mini-toc-levels: 4
exl-id: 886063d4-71dd-48c8-a342-884ad2c111ca
source-git-commit: 8bf73e87b1dbd9cd536248010a44404bc1b3d5f6
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Informazioni sulla configurazione di un account alias società Dynamic Media {#about-dm-alias-acct}

<!-- hide: yes
hidefromtoc: yes -->

<!-- >[!NOTE]
>
>This feature to create a Dynamic Media company alias account is in the Prerelease Channel for January 2022. See [Prerelease Channel documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=en#enable-prerelease) for information on how to enable the feature for your environment. The feature will be generally available in the February 2022 release. -->

Gli URL di Dynamic Media e il codice di incorporamento del visualizzatore contengono il nome dell&#39;account dell&#39;azienda. Questo nome account è stato creato al momento del provisioning di Dynamic Media. Ci possono essere scenari in cui la tua azienda ha subito un&#39;acquisizione, o un rebranding, o semplicemente vuoi utilizzare un nome più memorabile. In questi scenari, non è facile aggiornare manualmente il nome dell’account aziendale in tutti gli URL e nel codice di incorporamento del visualizzatore fornito con la soluzione. Inoltre, esiste la possibilità che tu possa influire sull’archivio Dynamic Media esistente o sui contenuti live. Per risolvere il problema, è possibile configurare un account alias società Dynamic Media.

Un account alias società Dynamic Media garantisce che tutti gli URL predefiniti di Dynamic Media e il codice di incorporamento del visualizzatore nell’interfaccia utente riflettano eventuali aggiornamenti apportati al contesto aziendale, ad esempio il rebranding. Un account alias ha anche un impatto positivo sull’ottimizzazione SEO (Search Engine Optimization), in quanto gli URL di Dynamic Media e il codice di incorporamento del visualizzatore riflettono il nuovo nome dell’account aziendale.

Quando configuri un account alias società Dynamic Media, tieni presente quanto segue:

* Eventuali URL di Dynamic Media esistenti o codice di incorporamento del visualizzatore sul tuo *live* le proprietà digitali devono essere aggiornate manualmente per riflettere il nuovo nome alias. Tuttavia, gli URL o i visualizzatori che incorporano il codice con il nome originale dell&#39;azienda Dynamic Media continuano a funzionare per le risorse nuove o esistenti.
* La funzionalità dell’account alias della società Dynamic Media è limitata alla modalità e alla consegna di Experience Manager Assets Authoring. Il nome alias della società non funziona con Experience Manager Sites. I componenti WCM (Web Content Management) non sono aggiornati per questa modifica. Tali componenti continuano a funzionare con il nome aziendale originale di Dynamic Media per recuperare le risorse Dynamic Media.
* È possibile impostare un solo account alias società in **[!UICONTROL Modifica configurazione Dynamic Media]** pagina. Tuttavia, puoi creare tutti gli account alias aziendali tramite un caso di supporto e riflettere manualmente il nome alias necessario negli URL di Dynamic Media o nel codice di incorporamento del visualizzatore.
* La soluzione preconfigurata [Annullamento validità cache](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md) La funzionalità di Dynamic Media annulla la validità degli URL con gli account Alias sia della società che della società configurati nella pagina Configurazione di Dynamic Media in Cloud Services.
* Quando si configura un account alias società in **[!UICONTROL Modifica configurazione Dynamic Media]** affinché l’annullamento della validità della cache abbia esito positivo, è necessario invalidare gli URL per *entrambi* il **[!UICONTROL Azienda]** account e **[!UICONTROL Alias società]** account, simultaneamente.

Vedi anche [Creare una configurazione Dynamic Media in Cloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)

## Configurare un account alias società Dynamic Media {#configure-dm-alias-account}

Per iniziare a configurare un account alias della società Dynamic Media, devi prima inviare un caso di supporto. Questo passaggio è obbligatorio.

1. [Utilizza l’Admin Console per creare un caso di supporto](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html).
1. Fornisci le seguenti informazioni nel tuo caso di assistenza:

   * Nome alias società Dynamic Media che si desidera utilizzare. Il nome deve contenere *solo* lettere (è consentito usare maiuscole e minuscole), numeri, trattini e trattini bassi.
   * La tua regione.
   * Se esistono [set di regole](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md) vengono utilizzati in precedenza per ottenere la trasmissione dei contenuti Dynamic Media tramite un nome account aziendale Dynamic Media alternativo.

1. Dopo la creazione dell’account alias Dynamic Media da parte del supporto, nell’istanza Autore as a Cloud Service di Experience Manager, seleziona il logo Experience Manager as a Cloud Service per accedere alla console di navigazione globale.
1. A sinistra della console, seleziona l’icona Strumenti, quindi vai a **[!UICONTROL Cloud Services > Configurazione Dynamic Media]**.
1. Nella pagina Browser configurazioni Dynamic Media, nel riquadro a sinistra, selezionare **[!UICONTROL globale]** (non selezionare l&#39;icona della cartella a sinistra di **[!UICONTROL globale]**). Quindi seleziona **[!UICONTROL Modifica]**.

   ![Campo di testo Alias società Dynamic Media](/help/assets/assets-dm/dm-company-alias.png)

1. Il giorno **[!UICONTROL Modifica configurazione Dynamic Media]** pagina, nella **[!UICONTROL Alias società]** testo, digitare il nome dell&#39;account alias di Dynamic Media specificato in precedenza nel caso di supporto.
1. In alto a destra, seleziona **[!UICONTROL Salva]**.
L’account alias società Dynamic Media ora è salvato e abilitato; tutti gli URL e il codice di incorporamento del visualizzatore per le risorse nuove e esistenti ora riflettono il nuovo nome alias società.