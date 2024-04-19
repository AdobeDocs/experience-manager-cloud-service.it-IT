---
title: Configurazione dell’ambiente dell’account
description: Adobe Experience Manager (AEM) consente di configurare l’account e alcuni aspetti dell’ambiente di authoring.
exl-id: 1b948f0b-85b9-478a-8b7e-61495c1d57b6
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 60%

---

# Configurazione dell’ambiente dell’account   {#configuring-your-account-environment}

Adobe Experience Manager (AEM) consente di configurare l’account e alcuni aspetti dell’ambiente di authoring.

Utilizza l’opzione [Utente](#user-settings) nell’[intestazione](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header) e la relativa finestra di dialogo [Preferenze](#my-preferences) per modificare le opzioni utente.

Per prima cosa, accedi all’opzione [Utente](#user-settings) nell’intestazione.

## Impostazioni utente {#user-settings}

Le impostazioni **Utente** consentono di accedere a:

* Impersona
   * La funzionalità Impersona permette a un utente di lavorare a nome di un altro utente. <!--With the [Impersonate as](/help/sites-administering/security.md#impersonating-another-user) functionality, a user can work on behalf of another user.-->
* Profilo
   * Offre un collegamento semplice alle impostazioni utente <!--Offers a convenient link to your [user settings](/help/sites-administering/security.md))-->
* [Preferenze](#my-preferences)
   * Consente di specificare varie preferenze di impostazione specifiche dell’utente.

![Impostazioni utente](/help/sites-cloud/authoring/assets/user-settings.png)

### Preferenze {#my-preferences}

Il **Le mie preferenze** è accessibile tramite il [Utente](#user-settings) nell’intestazione.

Ogni utente può impostare le proprie proprietà preferite.

![Preferenze](/help/sites-cloud/authoring/assets/user-preferences.png)

* **Lingua**

  Consente di definire la lingua da usare nell’interfaccia dell’ambiente di authoring. Seleziona la lingua desiderata dall’elenco disponibile.

* **Gestione finestre**

  Ciò definisce il comportamento o l’apertura delle finestre. Puoi selezionare:

   * **Finestre multiple** (predefinito)

      * Le pagine vengono aperte in una nuova finestra.

   * **Finestra singola**

      * Le pagine vengono aperte nella finestra corrente.

* **Mostra azioni desktop per Assets**

  Questa opzione richiede l’utilizzo dell’app desktop AEM.

* **Colore annotazione**

  Definisce il colore predefinito utilizzato per le annotazioni.

   * Fai clic sul blocco di colori per aprire il selettore di campioni e selezionare un colore.
   * In alternativa, immetti nel campo il codice esadecimale del colore desiderato.

* **Presentazione data relativa**

  Per migliorare la leggibilità, AEM riproduce le date degli ultimi sette giorni come date relative (ad esempio, Tre giorni fa) e le date più lontane come date esatte (ad esempio, 20 marzo 2017).

  Questa opzione definisce il modo in cui il sistema visualizza le date. Sono disponibili le seguenti opzioni:

   * **Mostra sempre data esatta**: viene sempre visualizzata la data esatta e non una data relativa.
   * **1 giorno**: viene visualizzata la data relativa per le date entro un giorno; in caso contrario viene visualizzata una data esatta.
   * **7 giorni (impostazione predefinita)**: viene visualizzata la data relativa per date entro sette giorni; in caso contrario viene visualizzata una data esatta.
   * **1 mese**: viene visualizzata la data relativa per le date entro un mese; in caso contrario viene visualizzata una data esatta.
   * **1 anno**: viene visualizzata la data relativa per le date entro un anno; in caso contrario viene visualizzata una data esatta.
   * **Mostra sempre data relativa**: non vengono mai visualizzate date esatte, ma solo date relative.

* **Abilita scelte rapide**

  AEM supporta varie scelte rapide da tastiera per rendere più efficiente l’authoring.

   * [Scelte rapide da tastiera per la modifica delle pagine](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
   * [Scelte rapide da tastiera per le console](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)

  Questa opzione abilita le scelte rapide da tastiera. Per impostazione predefinita sono abilitate, ma possono essere disabilitate, ad esempio, se un utente ha determinati requisiti di accessibilità.

* **Abilita pagina iniziale di Assets**

  Questa opzione è disponibile solo se l’amministratore di sistema ha attivato l’esperienza Pagina iniziale risorse per l’intera organizzazione.

* **Configurazione Stock**

  Questa opzione consente di specificare la configurazione di Adobe Stock preferita ed è disponibile solo se l’amministratore di sistema ha abilitato [Integrazione con Adobe Stock](/help/assets/aem-assets-adobe-stock.md).
