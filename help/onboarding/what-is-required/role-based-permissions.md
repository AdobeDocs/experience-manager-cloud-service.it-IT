---
title: Autorizzazioni basate sul ruolo
description: Autorizzazioni basate sul ruolo
translation-type: tm+mt
source-git-commit: 6cae9b2b719dab687f601a0596d37f99afded9ab

---


# Autorizzazioni basate sul ruolo {#role-based-permissions}

[!UICONTROL Cloud Manager] dispone di ruoli preconfigurati con autorizzazioni appropriate. Ad esempio, uno sviluppatore sviluppa il codice e ha l&#39;autorizzazione per inviare il codice al repository **** Git. In alternativa, il proprietario di un&#39;azienda dispone di autorizzazioni diverse che consentono di definire gli indicatori prestazioni chiave (KPI, Key Performance Indicators) e di approvare le distribuzioni.

## Autorizzazioni utente {#user-permissions}

A ciascun ruolo sono associate autorizzazioni specifiche, attività preconfigurate o autorizzazioni specifiche. In questa tabella sono elencate le funzioni disponibili e i ruoli che possono eseguire la funzione.

| Autorizzazione | Descrizione | Proprietario | Gestione distribuzione | Program Manager | Sviluppatore |
|--- |--- |--- |--- |--- |--- |
| Crea tenant | Crea un nuovo tenant. |  |  |  |  |
| Aggiorna tenant | Aggiorna tenant. |  |  |  |  |
| Aggiungi programma | Aggiungere un nuovo programma. | x |  |  |  |
| Crea ambiente | Creare Ambienti Prod+Stage, Dev, Playground. | x | x |  |  |
| Configurare le variabili di ambiente | Configurare le variabili di ambiente e i segreti. |  | x |  | x |
| Aggiungi o rimuovi nome di dominio personalizzato, carica o aggiorna certificato SSL | Aggiungi/rimuovi nome di dominio personalizzato, carica/aggiorna certificato SSL. | x | x |  |  |
| Aggiorna ambiente | Aggiornare Gli Ambienti Prod+Stage, Dev, Playground. | x | x |  |  |
| Elimina ambiente | Elimina ambienti non prod, Dev, Playground. | x | x |  |  |
| Elimina ambiente | Elimina Ambiente Prod+Fase. |  |  |  |  |
| Ambiente di sospensione | Ambienti Non-prod, Dev, Playground. | x | x |  |  |
| Impostazione programma | Configurare il programma (inclusi i KPI). | x |  |  |  |
| Impostazione programma | Configurare i criteri di ridimensionamento (Generale: configurazione del numero massimo di livelli e della scala orizzontale su richiesta: consenso). | x |  |  |  |
| Impostazione programma | Accesso A Git Conferma. |  | x |  | x |
| Impostazione pipeline | Configurazione o modifica della tubazione. |  | x |  |  |
| Esecuzione pipeline | Avviate la tubazione. | x | x |  |  |
| Esecuzione pipeline | Rifiuta/Approva Importanti Errori A 3 Livelli. | x | x | x |  |
| Esecuzione pipeline | Fornisci l&#39;approvazione GoLive. | x | x | x |  |
| Esecuzione pipeline | Pianificazione distribuzione produzione. | x | x | x |  |
| Esecuzione pipeline | Riprende tubazione produzione. |  |  |  |  |
| Consenso (o rifiuto) al provisioning | Consenso al provisioning orizzontale su richiesta dalla schermata di configurazione del programma. Configurate i segmenti P-D &#39;consentiti&#39; massimi che possono essere ridimensionati orizzontalmente in ambienti di PROD e non-PROD. | x |  |  |  |
| Gestisci ambiente | Aggiungi segmento Publish-Dispatcher dalla schermata Manage Environment (Gestisci ambiente). | x | x |  |  |  |
| Aggiornamento del prodotto | La scheda Aggiornamento AEM è visibile e porta l&#39;utente a effettuare l&#39;aggiornamento guidato. | x | x | x | x |
| Aggiornamento del prodotto | È possibile intervenire su Aggiornamento guidato prodotto. | x | x |  |  |
| Aggiornamento push | Avviate la pipeline di aggiornamento push. |  |  |  |  |
| Genera token di accesso personale | Genera token di accesso personale. |  | x |  | x |

