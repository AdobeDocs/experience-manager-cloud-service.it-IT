---
title: Note sulla versione 2025.06.19 dell’editor universale
description: Queste sono le note sulla versione 2025.06.19 dell’editor universale.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 5ffae9e548ca952975b3ea805808e227102ec99f
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 26%

---


# Note sulla versione 2025.06.19 dell’editor universale {#release-notes}

Queste sono le note sulla versione del 19 giugno 2025 di Universal Editor.

>[!TIP]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Novità {#what-is-new}

* **Supporto per più campi nella barra delle proprietà** -
  [È ora possibile utilizzare il componente contenitore](/help/implementing/universal-editor/field-types.md#container) per creare proprietà con più campi.
* **Supporto per le proprietà nidificate** - Il campo [`name`](/help/implementing/universal-editor/field-types.md#nesting) ora supporta i percorsi per abilitare la nidificazione delle proprietà.
* **Pannello destro ridimensionabile** - Il pannello laterale può ora essere ridimensionato per rendere migliore la visualizzazione del contenuto più lungo nel pannello laterale.

## Funzioni di adozione anticipata {#early-adopter}

Per testare alcune delle prossime funzionalità, partecipa al primo programma di adozione di Adobe.

### **Annulla/Ripristina** {#undo-redo}

Le funzioni Annulla e Ripristina sono ora disponibili per gli autori di contenuti dell’Editor universale.

* Sono incluse le modifiche apportate nel contesto, le modifiche effettuate tramite il pannello Proprietà, nonché l’aggiunta (o la duplicazione), lo spostamento e l’eliminazione di blocchi.
* Le operazioni Annulla e Ripristina sono limitate alla sessione corrente del browser.

Se ti interessa testare questa nuova funzione e condividere il feedback, invia un’e-mail al tuo Adobe Customer Success Manager dall’indirizzo e-mail associato al tuo Adobe ID.

## Altri miglioramenti {#other-improvements}

* Sono stati corretti gli errori di collisione relativi alla chiave di risorsa durante lo spostamento di blocchi tra contenitori.
* È stato risolto un problema a causa del quale la duplicazione dell’ultimo blocco di un contenitore non riusciva.
* Il menu a discesa Add action (Aggiungi azione) ora elenca solo i componenti che hanno un plug-in appropriato definito nel file `component-definition.json`.
* La data di modifica utilizzata nella finestra di dialogo di pubblicazione è stata corretta e in alcune circostanze le pagine non venivano riconosciute come modificate e non venivano ripubblicate.
* È stato corretto il comportamento di ereditarietà MSM a causa del quale la modifica di un contenitore annullava l’ereditarietà per i nodi figlio.
* `fetchUrl` è stato corretto, ripristinando lo spostamento di blocchi da un contenitore all&#39;altro.
