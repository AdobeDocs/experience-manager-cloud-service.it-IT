---
title: Note sulla versione 2025.2.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Ulteriori informazioni sulla versione 2025.2.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: ee7a99c5bf08b39a743d4b326ac23cc8546c512e
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 18%

---

# Note sulla versione 2025.2.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3389843928 -->

Ulteriori informazioni sulla versione 2025.2.0 di Cloud Manager in AEM (Adobe Experience Manager) as a Cloud Service.


Consulta anche le [note sulla versione corrente di Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Date di pubblicazione {#release-date}

La data di pubblicazione della versione 2025.2.0 di Cloud Manager in AEM as a Cloud Service è il venerdì 13 febbraio 2025.

La prossima pubblicazione è pianificata per il venerdì 13 marzo 2025.

## Novità {#what-is-new}

* **Aggiornamento alle regole di qualità del codice**

  A partire da giovedì 13 febbraio 2025, il passaggio della qualità del codice di Cloud Manager utilizza ora SonarQube 9.9.5.90363.

  Le regole aggiornate, disponibili per Cloud Manager su AEM as a Cloud Service in [questo collegamento](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules), determinano i punteggi di sicurezza e la qualità del codice per le pipeline di Cloud Manager.

* SonarQube 9.9 è ora il motore di scansione della qualità del codice predefinito per tutti i clienti.

* **Supporto per la compilazione di Java 17 e Java 21**

  I clienti possono ora creare con Java 17 o Java 21, accedendo a miglioramenti delle prestazioni e a nuove funzioni del linguaggio. Per i passaggi di configurazione, incluso l’aggiornamento delle versioni del progetto Maven e della libreria, consulta [Ambiente di build](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). Quando la versione della build è impostata su Java 17 o Java 21, il runtime distribuito è Java 21.

* **Rapporti di uptime di SLA al 99,99% per Edge Delivery Services**

  Per i programmi Edge Delivery Services qualificati è ora disponibile un rapporto di uptime ad alta disponibilità del 99,99%. Per abilitare questa funzione, i clienti devono effettuare correttamente l’onboarding dei propri siti Edge Delivery Services e applicare il 99,99% di Service level agreement (SLA) in Cloud Manager.

  Vedi anche [SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla).

* **Esperienza di invito utente migliorata per Edge Delivery Services**

  Sono stati apportati miglioramenti all’esperienza di invito degli utenti all’archivio dei contenuti associato a Edge Delivery Services. <!-- CMGR-65331 -->

* **Creazione automatica dei profili amministratore nelle istanze di pubblicazione**

  In precedenza, Cloud Manager consentiva la creazione manuale di profili di amministrazione sulle istanze di pubblicazione, ma non supportava la creazione automatica per impostazione predefinita. Con questo aggiornamento, i profili di amministratore vengono ora creati automaticamente sulle istanze di pubblicazione, migliorando l’usabilità e riducendo i tempi di configurazione per i clienti.

  Per ulteriori dettagli, vedere [Autorizzazioni personalizzate](/help/implementing/cloud-manager/custom-permissions.md).

  ![Filtro attività pipeline](/help/implementing/cloud-manager/release-notes/assets/product-profiles.png)

* **Transizione a OAuth per ambienti Cloud Service**

  I nuovi ambienti Cloud Service ora utilizzano l’autenticazione service-to-service basata su OAuth per i progetti di integrazione di Adobe Developer Console invece del metodo di autenticazione JWT utilizzato in precedenza. L’autenticazione JWT è obsoleta ed è prevista per la fine del ciclo di vita a giugno 2025.

* **Supporto per chiavi private EC (curva ellittica) (secp384r1)**

  Cloud Manager ora supporta le chiavi private EC (Elliptic Curve) `secp384r1`, fornendo maggiore sicurezza e conformità per i certificati SSL OV/EV gestiti dal cliente.
Per ulteriori dettagli, vedi [Requisiti per i certificati SSL OV/EV gestiti dal cliente](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md). <!-- CMGR-63636 -->

* **Ambienti di test specializzati**

  A partire dal 27 febbraio 2025, sarà disponibile un nuovo ambiente di sviluppo con risorse migliorate per i primi utenti.


<!--
## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->


## Correzioni di bug

* **(UI) È stato risolto un problema che impediva la configurazione CDN per i domini in Cloud Manager.**
I clienti che tentavano di aggiungere una configurazione CDN in Cloud Manager riscontravano un errore di schermata quando selezionavano un dominio dal menu a discesa. Questo bug dell’interfaccia utente impediva la mappatura del dominio negli ambienti di produzione, bloccando il processo di configurazione.

  Inoltre, alcuni domini sono rimasti inaccessibili nel backend, nonostante fossero stati rimossi dall’interfaccia utente. Questo problema causava conflitti con le configurazioni CDN esistenti.

  Con questa correzione, ora puoi selezionare correttamente un dominio dal menu a discesa senza incontrare un errore. Sono state risolte le incoerenze di back-end che impedivano la riconfigurazione del dominio. Infine, il miglioramento della convalida ora garantisce che i domini in conflitto vengano rimossi correttamente prima di aggiungerli nuovamente.<!-- CMGR-64888 -->
* **(back-end) È stato risolto un problema che causava l&#39;invio ripetuto di notifiche di scadenza SSL.**
È stato identificato un bug a causa del quale il modulo di pianificazione delle notifiche di scadenza SSL, progettato per essere eseguito una volta al giorno a mezzanotte, veniva erroneamente attivato due volte al giorno, una volta a mezzanotte e di nuovo alle 00:30. Questo problema causava l’invio di più notifiche ridondanti relative alla scadenza dei certificati SSL.

  Il modulo di pianificazione delle notifiche ora viene eseguito correttamente una sola volta al giorno, come previsto. Inoltre, non riceverai più notifiche di scadenza SSL duplicate. <!-- CMGR-64748 -->




<!-- ## Known issues {#known-issues} -->
