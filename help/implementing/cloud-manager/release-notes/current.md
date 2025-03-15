---
title: Note sulla versione 2025.3.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Ulteriori informazioni sulla versione 2025.3.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 5983c8579dd8606bc8bedfe6fa2a3838493452cd
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 31%

---

# Note sulla versione 2025.3.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

Ulteriori informazioni sulla versione 2025.3.0 di Cloud Manager in AEM (Adobe Experience Manager) as a Cloud Service.


Consulta anche le [note sulla versione corrente di Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Date di pubblicazione {#release-date}

La data di pubblicazione della versione 2025.3.0 di Cloud Manager in AEM as a Cloud Service è il venerdì 13 marzo 2025.

La prossima pubblicazione è pianificata per il venerdì 10 aprile 2025.

## Novità {#what-is-new}

* **Esegui più pipeline**

  La possibilità di eseguire più pipeline contemporaneamente è stata introdotta nella pagina Pipeline. Gli utenti devono selezionare almeno una pipeline ma non più di dieci. Nell&#39;angolo superiore destro della pagina Pipeline, fare clic su **Esegui selezionati (x)**. Viene visualizzata una finestra di dialogo modale in cui sono elencate tutte le pipeline che non possono essere avviate. Fai clic su **Esegui** per avviare tutte le pipeline valide.

  ![Finestra di dialogo Esegui pipeline selezionate](/help/implementing/cloud-manager/release-notes/assets/run-selected-pipelines.png)

* **Supporto esteso alle versioni di Node.js**

  L&#39;ambiente di sviluppo front-end ora supporta le seguenti `Node.js` versioni:

   * 23
   * 22
   * 20

  Vedi anche [Sviluppare siti con la pipeline front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md#node-versions). <!-- CMGR-65307 -->

<!--
## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->


## Correzioni di bug

* **(UI) Correzione per gli aggiornamenti di &#39;Configurazione di rete avanzata&#39; in Cloud Manager**

  È stato risolto un raro problema che impediva gli aggiornamenti alla **Configurazione di rete avanzata** quando era presente una notifica &quot;Aggiornamento disponibile&quot;. In precedenza, Cloud Manager bloccava le modifiche di configurazione, incluse le impostazioni di rete avanzate, per evitare conflitti durante un aggiornamento. I clienti possono ora attivare manualmente l’aggiornamento in sospeso per applicare le modifiche necessarie senza restrizioni. <!-- CMGR-65913 and CMGR-65788 -->

* **(UI) Correzione per gli aggiornamenti dell&#39;elenco consentiti IP bloccati nello stato &quot;Aggiornamento&quot;**

  È stato risolto un raro problema a causa del quale gli aggiornamenti degli elenchi consentiti IP in Cloud Manager rimanevano bloccati nello stato &quot;Aggiornamento&quot; a causa di una configurazione del dominio attivo duplicata per un ambiente. In precedenza, i clienti riscontravano ritardi di elaborazione indefiniti durante l’aggiornamento degli elenchi consentiti IP, impedendo le necessarie regolazioni dell’accesso alla rete. Questa correzione assicura che gli aggiornamenti degli elenchi consentiti IP possano essere completati correttamente senza bloccarsi. <!-- CMGR-65786 -->




<!-- ## Known issues {#known-issues} -->
