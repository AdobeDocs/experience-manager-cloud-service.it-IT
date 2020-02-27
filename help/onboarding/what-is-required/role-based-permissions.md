---
title: Autorizzazioni basate sul ruolo
description: Autorizzazioni basate sul ruolo
translation-type: tm+mt
source-git-commit: e59fe55c255d5239a561a9fb878faa81d17b4b48

---


# Autorizzazioni basate sul ruolo {#role-based-permissions}

[!UICONTROL Cloud Manager] dispone di ruoli preconfigurati con autorizzazioni appropriate. Ad esempio, uno sviluppatore sviluppa il codice e ha l&#39;autorizzazione per inviare il codice al repository **** Git. In alternativa, il proprietario di un&#39;azienda dispone di autorizzazioni diverse che consentono di definire gli indicatori prestazioni chiave (KPI, Key Performance Indicators) e di approvare le distribuzioni.

## Autorizzazioni utente {#user-permissions}

A ciascun ruolo sono associate autorizzazioni specifiche, attività preconfigurate o autorizzazioni specifiche. In questa tabella sono elencate le funzioni disponibili e i ruoli che possono eseguire la funzione.

| Autorizzazione | Descrizione | Proprietario | Gestione distribuzione | Program Manager | Sviluppatore | CSE |
|--- |--- |--- |--- |--- |--- |--- |
| Lettura applicazione | Leggi KPI del programma. | x | x | x | x | x |
| Scrivi applicazione | Installazione o modifica del programma. | x |  |  |  |  |
| Ambiente di lettura | Consultate Dettagli ambiente. | x | x | x | x | x |
| Crea esecuzione | Avviate la tubazione. | x | x | x |  |  |
| Lettura esecuzione | Vedere stato di esecuzione. | x | x | x | x | x |
| Riprendi esecuzione | Può riprendere l&#39;esecuzione in pausa. | x | x | x |  | x |
| Approvazione esecuzione distribuzione in produzione | Fornisci l&#39;approvazione GoLive. | x | x | x |  |  |
| Programma di esecuzione Distribuisci in produzione | Pianificazione distribuzione produzione. | x | x | x |  | x |
| Implementazione in produzione | Implementare l&#39;applicazione in produzione quando viene messa in pausa per CSE Oversight. |  |  |  |  | x |
| Annullamento esecuzione | Annulla esecuzione corrente. | x | x | x |  |  |
| Errori Gate Di Sostituzione Dell&#39;Esecuzione | Approvare Importanti Errori Di Controllo Della Qualità. | x | x | x |  |  |
| Crea tubazione | Impostazione/Modifica tubazione. |  | x |  |  |  |
| Lettura pipeline | Consultate Dettagli sulla tubazione. | x | x | x | x | x |
| Scrittura pipeline | Impostazione/Modifica tubazione. |  | x |  |  |  |
| Approvazione modifica pipeline | Consente di modificare l&#39;opzione Proprietario business. |  | x |  |  |  |
| Distribuzione gestita tramite modifica pipeline | Consente di modificare l&#39;opzione CSE Oversight. |  | x |  |  |  |
| Lettura passaggio | Vedi i risultati delle metriche sulla qualità dei passaggi. | x | x | x | x | x |
