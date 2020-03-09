---
title: Configurazione dell’ambiente dell’account
description: AEM consente di configurare l’account e alcuni aspetti dell’ambiente di authoring
translation-type: ht
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Configurazione dell’ambiente dell’account   {#configuring-your-account-environment}

Con AEM è possibile configurare il proprio account e alcuni aspetti dell’ambiente di authoring.

Utilizza l’opzione [Utente](#user-settings) nell’[intestazione](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header) e la relativa finestra di dialogo [Preferenze](#my-preferences) per modificare le opzioni utente.

Per prima cosa, accedi all’opzione [Utente](#user-settings) nell’intestazione.

## Impostazioni utente {#user-settings}

La finestra di dialogo **Impostazioni utente** consente di accedere alle seguenti funzioni:

* Impersona
   * La funzionalità Impersona permette a un utente di lavorare a nome di un altro utente. <!--With the [Impersonate as](/help/sites-administering/security.md#impersonating-another-user) functionality, a user can work on behalf of another user.-->
* Profilo
   * Offre un collegamento semplice alle impostazioni utente.<!--Offers a convenient link to your [user settings](/help/sites-administering/security.md))-->
* [Preferenze](#my-preferences)
   * Consente di specificare varie preferenze di impostazione specifiche dell’utente.

![Impostazioni utente](/help/sites-cloud/authoring/assets/user-settings.png)

### Preferenze {#my-preferences}

Puoi accedere alla finestra di dialogo **Preferenze** tramite l’opzione [Utente](#user-settings) nell’intestazione.

Ogni utente può impostare autonomamente determinate proprietà.

![Preferenze](/help/sites-cloud/authoring/assets/user-preferences.png)

* **Lingua**

   Consente di definire la lingua da usare nell’interfaccia dell’ambiente di authoring. Seleziona la lingua desiderata dall’elenco delle opzioni disponibili.

* **Gestione finestre**

   Consente di definire il comportamento o l’apertura delle finestre. Puoi selezionare:

   * **Finestre multiple** (predefinito)

      * Le pagine si apriranno in una nuova finestra.
   * **Finestra singola**

      * Le pagine si apriranno nella finestra corrente.


* **Mostra azioni desktop per Assets**

   Questa opzione richiede l’utilizzo dell’app desktop AEM.

* **Colore annotazione**

   Consente di definire il colore predefinito utilizzato per le annotazioni.

   * Fai clic sul blocco dei colori per aprire il selettore di campioni e selezionare un colore.
   * In alternativa, immetti nel campo il codice esadecimale del colore desiderato.

* **Presentazione data relativa**

   Per migliorare la leggibilità, AEM presenta le date degli ultimi sette giorni come date relative (ad esempio, tre giorni fa) e le date più lontane come date esatte (ad esempio, il 20 marzo 2017).

   Questa opzione definisce il modo in cui il sistema visualizza le date. Sono disponibili le seguenti opzioni:

   * **Mostra sempre data esatta**: viene sempre visualizzata la data esatta e non una data relativa.
   * **1 giorno**: viene visualizzata la data relativa per le date entro un giorno; in caso contrario viene visualizzata una data esatta.
   * **7 giorni (impostazione predefinita)**: viene visualizzata la data relativa per date entro sette giorni; in caso contrario viene visualizzata una data esatta.
   * **1 mese**: viene visualizzata la data relativa per le date entro un mese; in caso contrario viene visualizzata una data esatta.
   * **1 anno**: viene visualizzata la data relativa per le date entro un anno; in caso contrario viene visualizzata una data esatta.
   * **Mostra sempre data relativa**: non vengono mai visualizzate date esatte, ma solo date relative.

* **Abilita scelte rapide**

   AEM supporta una serie di scelte rapide da tastiera per ottimizzare l’authoring.

   * [Scelte rapide da tastiera per la modifica delle pagine](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
   * [Scelte rapide da tastiera per le console](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)
   Questa opzione abilita le scelte rapide da tastiera. Queste sono abilitate per impostazione predefinita, ma possono essere disabilitate se, ad esempio, un utente presenta determinati requisiti di accessibilità.

* **Abilita pagina iniziale di Assets**

   Questa opzione è disponibile solo se l’amministratore del sistema ha abilitato l’esperienza Home page di Assets per l’intera organizzazione.

* **Configurazione Stock**

   Questa opzione consente di specificare la configurazione di Adobe Stock preferita ed è disponibile solo se l’amministratore di sistema ha abilitato l’integrazione con Adobe Stock. <!--This option allows to specify the preferred Adobe Stock configuration and is only be available if your system administrator has enabled [Adobe Stock integration](/help/assets/aem-assets-adobe-stock.md).-->
