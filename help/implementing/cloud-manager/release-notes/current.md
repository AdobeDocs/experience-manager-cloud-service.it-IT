---
title: Note sulla versione 2025.1.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Ulteriori informazioni sulla versione 2025.1.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
role: Admin
source-git-commit: bf12306969581723e4e9ce1517a8f0d445f26521
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 22%

---

# Note sulla versione 2025.1.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

Ulteriori informazioni sulla versione 2025.1.0 di Cloud Manager in AEM (Adobe Experience Manager) as a Cloud Service.

>[!NOTE]
>
>Consulta le [note sulla versione corrente di Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Date di pubblicazione {#release-date}

La data di rilascio per Cloud Manager 2025.1.0 in AEM as a Cloud Service è mercoledì 22 gennaio 2025.

La prossima versione è pianificata per il venerdì 13 febbraio 2025.


## Novità {#what-is-new}

* **Regole di qualità del codice:** il passaggio Qualità codice di Cloud Manager inizierà con SonarQube Server 9.9 con la versione 2025.2.0 di Cloud Manager, pianificata per giovedì 13 febbraio 2025.

Per preparare, le regole SonarQube aggiornate sono ora disponibili in [Regole per la qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules).

Puoi &quot;verificare anticipatamente&quot; le nuove regole impostando la seguente variabile di testo della pipeline:

`CM_BUILD_IMAGE_OVERRIDE` = `self-service-build:sonar-99-upgrade-java17or21`

Inoltre, impostare la variabile seguente per garantire che il passaggio di qualità del codice venga eseguito per lo stesso commit (normalmente ignorato per lo stesso `commitId`):

`CM_DISABLE_BUILD_REUSE` = `true`

![Pagina Configurazione variabili](/help/implementing/cloud-manager/release-notes/assets/variables-config.png)

>[!NOTE]
>
>Adobe consiglia di creare una nuova pipeline CI/CD Code Quality, configurata sullo stesso ramo della pipeline di produzione principale. Imposta le variabili appropriate *prima* della versione del 13 febbraio 2025 per verificare che le nuove regole applicate non introducano blocchi.

* Supporto per la compilazione di **Java 17 e Java 21:** I clienti possono ora creare con Java 17 o Java 21, accedendo a miglioramenti delle prestazioni e a nuove funzioni del linguaggio. Per i passaggi di configurazione, incluso l&#39;aggiornamento delle versioni del progetto Maven e della libreria, consulta [Ambiente di build](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). Quando la versione della build è impostata su Java 17 o Java 21, il runtime distribuito è Java 21.

   * **Abilitazione funzionalità**
      * Questa funzione verrà abilitata per tutti i clienti giovedì 13 febbraio 2025, in coincidenza con il rollout predefinito della nuova versione di SonarQube.
      * I clienti possono abilitarlo *immediatamente* impostando le due configurazioni di variabili descritte in precedenza per l&#39;aggiornamento della versione 9.9 di SonarQube.

   * **Distribuzione runtime Java 21**
      * Il runtime Java 21 viene distribuito durante la generazione con Java 17 o Java 21.
      * Il rollout graduale a tutti gli ambienti Cloud Manager inizia a febbraio per le sandbox e gli ambienti di sviluppo e si estende agli ambienti di produzione in aprile.
      * I clienti che desiderano adottare il runtime Java 21 *precedente* possono contattare Adobe all&#39;indirizzo [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com).


<!-- ## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->

<!-- ## Bug fixes -->




<!-- ## Known issues {#known-issues} -->
