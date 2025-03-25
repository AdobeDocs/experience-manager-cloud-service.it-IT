---
title: Note sulla versione 2025.3.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Ulteriori informazioni sulla versione 2025.3.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 663234640f16e6aa653251399751abf5daa17f82
workflow-type: ht
source-wordcount: '329'
ht-degree: 100%

---

# Note sulla versione 2025.3.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

Ulteriori informazioni sulla versione 2025.3.0 di Cloud Manager in AEM (Adobe Experience Manager) as a Cloud Service.


Consulta anche le [note sulla versione corrente di Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Date di pubblicazione {#release-date}

La data di pubblicazione della versione 2025.3.0 di Cloud Manager in AEM as a Cloud Service è il venerdì 13 marzo 2025.

La prossima pubblicazione è pianificata per il 10 aprile 2025.

## Novità {#what-is-new}

* **Esecuzione di più pipeline**

  Nella pagina Pipeline è stata introdotta la possibilità di eseguire più pipeline contemporaneamente. Gli utenti devono selezionare almeno una pipeline e non più di dieci. Accanto all’angolo in alto a destra, nella pagina Pipeline, fai clic su **Esegui selezionate (x)**. Viene visualizzata una finestra di dialogo modale in cui sono elencate tutte le pipeline che non possono essere avviate. Fai clic su **Esegui** per avviare tutte le pipeline valide.

  ![Finestra di dialogo Esegui pipeline selezionate](/help/implementing/cloud-manager/release-notes/assets/run-selected-pipelines.png)

  Consulta anche [Esecuzione di più pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#run-multiple-pipelines)

* **Supporto esteso alle versioni di Node.js**

  L’ambiente di sviluppo front-end ora supporta le seguenti versioni di `Node.js`:

   * 23
   * 22
   * 20

  Consulta anche [Sviluppare siti con la pipeline front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md#node-versions). <!-- CMGR-65307 -->

<!--
## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->


## Correzioni di bug

* **(UI) Correzione per gli aggiornamenti di “Configurazione di rete avanzata” in Cloud Manager**

  È stato risolto un raro problema che impediva gli aggiornamenti alla **Configurazione di rete avanzata** in presenza di una notifica “Aggiornamento disponibile”. In precedenza, Cloud Manager bloccava le modifiche di configurazione, incluse le impostazioni di rete avanzate, per evitare conflitti durante un aggiornamento. La clientela ora può attivare manualmente l’aggiornamento in sospeso per applicare le modifiche necessarie senza restrizioni. <!-- CMGR-65913 and CMGR-65788 -->

* **(UI) Correzione per gli aggiornamenti dell’elenco IP consentiti bloccati nello stato “Aggiornamento”**

  È stato risolto un raro problema a causa del quale gli aggiornamenti degli elenchi IP consentiti in Cloud Manager rimanevano bloccati nello stato “Aggiornamento” dovuto a una configurazione del dominio attivo duplicata per un ambiente. In precedenza, la clientela riscontrava ritardi di elaborazione indefiniti durante l’aggiornamento degli elenchi IP consentiti, impedendo le modifiche di accesso alla rete necessarie. Questa correzione garantisce che gli aggiornamenti degli elenchi IP consentiti possano essere completati correttamente senza bloccarsi. <!-- CMGR-65786 -->




<!-- ## Known issues {#known-issues} -->
