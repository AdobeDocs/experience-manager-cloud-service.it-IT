---
title: Elenco a discesa a cascata
description: Utilizza espressioni Forms adattive per aggiungere convalida, calcolo e attivazione o disattivazione automatica della visibilità di una sezione.
feature: Adaptive Forms, Foundation Components
role: User
hide: true
hidefromtoc: true
source-git-commit: 53e476981874597bfb7f9293e67b2d135c72b318
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 2%

---

# Descrizione del caso d’uso

Durante la creazione di moduli o applicazioni, spesso è utile guidare gli utenti attraverso la selezione della posizione in modo strutturato. Un elenco a discesa a cascata lo rende semplice e intuitivo: l’utente seleziona innanzitutto un paese, che filtra l’elenco di stati/province disponibili, e quindi una scelta finale di città in base allo stato. Questo approccio non solo mantiene i moduli più puliti, ma impedisce anche combinazioni non valide (come la scelta di una città che non esiste in uno stato scelto).

Per eseguire questo caso d’uso sono necessari i seguenti passaggi

- Crea integrazione API
- Crea un modulo con campi per acquisire il paese/stato/città
- Creare una regola per popolare gli elenchi a discesa utilizzando l’integrazione API