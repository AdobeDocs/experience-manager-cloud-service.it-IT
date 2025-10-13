---
title: Elenco a discesa a cascata
description: Utilizzare l’integrazione API per popolare dinamicamente l’elenco a discesa
feature: Edge Delivery Services
role: User,Developer
source-git-commit: 53e476981874597bfb7f9293e67b2d135c72b318
workflow-type: ht
source-wordcount: '125'
ht-degree: 100%

---

# Descrizione del caso d’uso

Durante la creazione di moduli o applicazioni, spesso è utile guidare gli utenti attraverso la selezione della posizione in modo strutturato. Un elenco a discesa a cascata lo rende semplice e intuitivo: l’utente seleziona innanzitutto un paese, che filtra l’elenco di stati/province disponibili, e infine effettua la scelta di una città in base allo stato. Questo approccio non solo mantiene i moduli più puliti, ma impedisce anche combinazioni non valide (come la scelta di una città che non esiste in uno stato scelto).

Per eseguire questo caso d’uso sono necessari i seguenti passaggi

- Creare integrazione API
- Creare un modulo con campi per acquisire paese/stato/città
- Creare una regola per popolare gli elenchi a discesa utilizzando l’integrazione API