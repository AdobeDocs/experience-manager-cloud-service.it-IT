---
title: Note sulla versione 2025.06.19 dell’editor universale
description: Queste sono le note sulla versione 2025.06.19 dell’editor universale.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 5ffae9e548ca952975b3ea805808e227102ec99f
workflow-type: ht
source-wordcount: '297'
ht-degree: 100%

---


# Note sulla versione 2025.06.19 dell’editor universale {#release-notes}

Queste sono le note sulla versione del 19 giugno 2025 dell’editor universale.

>[!TIP]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Novità {#what-is-new}

* **Supporto per più campi nella barra delle proprietà** -
  È ora possibile utilizzare [il componente contenitore](/help/implementing/universal-editor/field-types.md#container) per creare proprietà con più campi.
* **Supporto per le proprietà nidificate**: il campo](/help/implementing/universal-editor/field-types.md#nesting) [`name` ora supporta i percorsi per abilitare la nidificazione delle proprietà.
* **Pannello destro ridimensionabile**: il pannello laterale può ora essere ridimensionato per rendere migliore la visualizzazione del contenuto più lungo nel pannello laterale.

## Funzioni per adozione anticipata {#early-adopter}

Per avere la possibilità di testare alcune delle prossime funzioni, partecipa al programma dei primi utilizzatori di Adobe.

### **Annullare/Ripetere** {#undo-redo}

La funzione Annulla e Ripeti è ora disponibile per gli autori di contenuti dell’Editor universale.

* Sono incluse le modifiche apportate nel contesto, quelle effettuate tramite il pannello Proprietà, nonché l’aggiunta (o la duplicazione), lo spostamento e l’eliminazione di blocchi.
* Le operazioni Annulla e Ripeti sono limitate alla sessione corrente del browser.

Se ti interessa testare questa nuova funzione e condividere un tuo feedback, invia un’e-mail al tuo Adobe Customer Success Manager dall’indirizzo e-mail associato al tuo Adobe ID.

## Altri miglioramenti {#other-improvements}

* Sono stati corretti gli errori di collisione relativi alla chiave di risorsa durante lo spostamento di blocchi tra contenitori.
* È stato risolto un problema a causa del quale la duplicazione dell’ultimo blocco di un contenitore non riusciva.
* Il menu a discesa Aggiungi azione ora elenca solo i componenti che hanno un plug-in appropriato definito nel file `component-definition.json`.
* La data di modifica utilizzata nella finestra di dialogo di pubblicazione è stata corretta e in alcune circostanze le pagine non venivano riconosciute come modificate e non venivano ripubblicate.
* È stato corretto il comportamento di ereditarietà MSM a causa del quale la modifica di un contenitore annullava l’ereditarietà per i nodi secondari.
* È stato corretto `fetchUrl`, ripristinando lo spostamento di blocchi da un contenitore all’altro.
