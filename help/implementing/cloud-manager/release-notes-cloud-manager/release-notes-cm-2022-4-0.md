---
title: Note sulla versione per Cloud Manager 2022.4.0 in Adobe Experience Manager as a Cloud Service
description: Queste sono le note sulla versione per Cloud Manager 2022.4.0 in AEM as a Cloud Service.
feature: Release Information
exl-id: e7ff623b-aeca-40a6-bf48-98af270a4117
source-git-commit: 458d63c27bb2ab4d09237aa3ecb96c0f6d5e67ed
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 3%

---

# Note sulla versione per Cloud Manager 2022.4.0 in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina documenta le note sulla versione per Cloud Manager 2022.4.0 in AEM as a Cloud Service.

>[!NOTE]
>
>Fai riferimento a [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md) per le note sulla versione corrente per Adobe Experience Manager as a Cloud Service.

## Data di pubblicazione {#release-date}

La data di rilascio della versione 2022.4.0 di Cloud Manager in AEM as a Cloud Service è il 7 aprile 2022. La prossima versione è prevista per il 5 maggio 2022.

## Novità {#what-is-new}

* Sono stati implementati miglioramenti alla durata e al tasso di successo delle fasi di generazione della pipeline e verranno distribuiti in modo incrementale a tutti i clienti entro il mese di aprile.
* È ora possibile trovare facilmente un ramo git digitando i primi caratteri del nome nel campo di input nella procedura guidata di aggiunta e modifica della pipeline e selezionando tra le corrispondenze suggerite per entrambi [produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) e [non produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) gasdotti.
* Poco dopo la versione di aprile, l’India sarà disponibile per la selezione quando definirà l’area cloud durante la creazione dell’ambiente.
* La **Tubi** La pagina ora dispone di impaginazione per migliorare l’usabilità dei programmi con un numero elevato di pipeline.
   * Nella tabella vengono visualizzate 50 righe per pagina.
* Versione del [Archetipo di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) utilizzato da Cloud Manager è stato aggiornato alla versione 36.
* Oracle JDK è ora il JDK predefinito per lo sviluppo e il funzionamento delle applicazioni AEM. Il processo di creazione di Cloud Manager passa automaticamente a utilizzando Oracle JDK, anche se nella toolchain Maven è selezionata esplicitamente un’opzione alternativa.
   * Per ulteriori informazioni su come passare ad Oracle JDK, consulta [la documentazione sull’ambiente di creazione.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)
   * Fai riferimento a [Domande frequenti sui criteri di supporto Java per Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-65/assets/Java_Policy_for_Adobe_Experience_Manager.pdf) per risolvere le domande comuni su questa modifica.
* L’esecuzione della pipeline ora non riesce più rapidamente rilevando versioni AEM precedenti durante il passaggio di convalida. Agli utenti verrà presentato un messaggio nell’interfaccia utente per guidarli.

## Correzioni di bug {#bug-fixes}

* Il registro creato nel passaggio Test interfaccia utente è ora disponibile per il download tramite l’interfaccia utente.
* Le pipeline di configurazione a livello web possono ora riutilizzare solo i pacchetti dalle esecuzioni di configurazione a livello web.
* Ai messaggi dell’interfaccia utente è stata aggiunta maggiore chiarezza su come aggiornare AEM in un ambiente obsoleto.
