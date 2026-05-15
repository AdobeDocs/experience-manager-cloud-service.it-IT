---
title: Creare un modulo con l’editor universale
description: Utilizza espressioni Forms adattive per aggiungere convalida, calcolo e attivazione o disattivazione automatica della visibilità di una sezione.
feature: Adaptive Forms, Foundation Components
role: User
hide: true
hidefromtoc: true
source-git-commit: cc3cd74ad87f4213a200f36745ab3d335edca02d
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 67%

---

# Creare un modulo con l’editor universale

Crea il seguente modulo utilizzando l’editor universale. Il modulo dispone di 3 elenchi a discesa, i cui valori verranno compilati utilizzando l’integrazione API
![modulo adattivo](assets/address-form.png)

## Paese di residenza

Al momento dell’inizializzazione, nel menu a discesa del paese di residenza verranno inseriti i risultati della chiamata API.
![initialize-event](assets/initialize-event.png)

## Handler operazione riuscita

Handler operazione riuscita è stato definito per impostare enum e enumNames dell’elenco a discesa del paese con i valori appropriati dall’array dei nomi geografici. L’array di nomi geografici è disponibile nell’opzione Payload evento
![payload evento](assets/event-payload.png)
![handler di successo](assets/success-handler.png)

## Recupera valori secondari

La voce di elenco Stato o Provincia viene compilato quando l’utente effettua una selezione nell’elenco a discesa Paese di residenza. Il geonameId associato al paese selezionato viene passato come parametro di input all’integrazione API GetChildren

![get-children](assets/invoke-service-get-children.png)

Il gestore di risultati è stato definito per impostare il campo a discesa enum/enumNames del campo StateOrProvince
![get-children-success-handler](assets/child-success-handler.png)

Quando hai selezionato stato o provincia, puoi popolare l’elenco a discesa città seguendo il modello sopra indicato, utilizzato per popolare l’elenco a discesa stato o provincia.