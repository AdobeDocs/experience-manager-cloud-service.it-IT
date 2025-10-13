---
title: Creare un modulo con l’editor universale
description: Crea un modulo adattivo per testare l’elenco a discesa tramite le integrazioni API
feature: Edge Delivery Services
role: User
source-git-commit: 53e476981874597bfb7f9293e67b2d135c72b318
workflow-type: ht
source-wordcount: '202'
ht-degree: 100%

---

# Creare un modulo con l’editor universale

Crea il seguente modulo utilizzando l’editor universale. Il modulo dispone di 3 elenchi a discesa, i cui valori verranno compilati utilizzando l’integrazione API
![modulo adattivo](assets/address-form.png)

## Paese di residenza

Al momento dell’inizializzazione, nel menu a discesa del paese di residenza verranno inseriti i risultati della chiamata API.
![initialize-event](assets/initialize-event.png)

## Handler operazione riuscita

Handler operazione riuscita è stato definito per impostare enum e enumNames dell’elenco a discesa del paese con i valori appropriati dall’array dei nomi geografici. L’array di nomi geografici è disponibile nell’opzione Payload evento
![event-payload](assets/event-payload.png)
![success-handler](assets/success-handler.png)

## Recupera valori secondari

La voce di elenco Stato o Provincia viene compilato quando l’utente effettua una selezione nell’elenco a discesa Paese di residenza. Il geonameId associato al paese selezionato viene passato come parametro di input all’integrazione API GetChildren

![get-children](assets/invoke-service-get-children.png)

Il handler operazione riuscirta è stato definito per impostare il dato enum/enumNames del campo StateOrProvince
![get-children-success-handler](assets/child-success-handler.png)

Quando hai selezionato stato o provincia, puoi popolare l’elenco a discesa città seguendo il modello sopra indicato, utilizzato per popolare l’elenco a discesa stato o provincia.