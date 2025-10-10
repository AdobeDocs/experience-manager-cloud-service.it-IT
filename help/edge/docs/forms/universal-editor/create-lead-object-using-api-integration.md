---
title: Creare un oggetto Lead di Salesforce tramite l’integrazione API
description: Scopri come creare un oggetto Lead di Salesforce utilizzando l’integrazione API.
feature: Adaptive Forms, Core Components, Edge Delivery Services
role: User, Developer
level: Beginner, Intermediate
keywords: integrazione dell’API nell’editor di regole, richiama i miglioramenti del servizio
exl-id: 55835ffe-1b77-449b-b76d-16c0a343cf5c
hide: true
hidefromtoc: true
index: false
source-git-commit: 3a09a3fa9b8fb3dacef4c900979c4cc256551941
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 7%

---

# Creare un oggetto Lead di Salesforce tramite l’integrazione API

Questo caso d’uso illustra come creare un lead in Salesforce utilizzando l’integrazione API. Al termine del processo, sarà possibile:

Configura un&#39;app [connessa in Salesforce](https://help.salesforce.com/s/articleView?id=platform.ev_relay_create_connected_app.htm&type=5) per abilitare l&#39;accesso API protetto.

Configura CORS (Cross-Origin Resource Sharing) per consentire al codice (come JavaScript) in esecuzione in un browser web di comunicare con Salesforce da un’origine specifica, aggiungi l’origine all’elenco Consentiti come mostrato di seguito

![cors](assets/salesforce-cors.png)

## Impostazioni app collegate

Nell&#39;app connessa vengono utilizzate le impostazioni seguenti. Puoi assegnare gli ambiti OAuth in base alle tue esigenze.
![impostazioni-app-connesse](assets/salesforce-connected-app-settings.png)

## Crea integrazione API

| Nome | Valore |
|--------------------------------|------------------|
| URL API | https://`<your-domain>`d.my.salesforce.com/services/data/v32.0/sobjects/Lead |
| ID client | Specifico per l’app connessa |
| Segreto client | Specifico per l’app connessa |
| URL OAuth | https://login.salesforce.com/services/oauth2/authorize |
| URL token di accesso | https://`<your-domain>`/services/oauth2/token |
| Aggiorna URL token | https://`<your-domain>`/services/oauth2/token |
| Ambito autorizzazione | api chatter_api id completo openid refresh_token visualforce web |
| Intestazione autorizzazione | Supporto autorizzazione |

![integrazione api](assets/salesforce-api-integration-create-lead.png)

## Parametri di input e output

Definisci i parametri di input per la chiamata API e mappa i parametri di output utilizzando il seguente json

```json
{
    "id": "00QKY000001LyJR2A0",
    "success": true
}
```

![input-output](assets/create-lead-api-integration-input-output.png)

## Creazione di un modulo

Crea un semplice modulo adattivo utilizzando l’Editor universale per acquisire i dettagli dell’oggetto Lead come mostrato di seguito
![modulo-oggetto-lead](assets/create-lead.png)

Gestisci l’evento clic sulla casella di controllo Crea lead utilizzando l’editor di regole. Mappate i parametri di input ai valori degli oggetti modulo appropriati, come mostrato di seguito. Visualizza l&#39;ID del nuovo oggetto Lead creato nell&#39;oggetto TextField `leadid`
![editor di regole](assets/create-leade-rule-editor.png)

## Testare l’integrazione

- Visualizzare l’anteprima del modulo
- Immetti alcuni valori significativi
- Selezionare la casella di controllo `Create Lead` per attivare la chiamata API
- L&#39;ID lead dell&#39;oggetto lead appena creato viene visualizzato nel campo di testo `Lead ID`.
