---
title: Elenco a discesa a cascata
description: Utilizza espressioni Forms adattive per aggiungere convalida, calcolo e attivazione o disattivazione automatica della visibilità di una sezione.
feature: Adaptive Forms, Foundation Components
role: User
hide: true
hidefromtoc: true
source-git-commit: cc3cd74ad87f4213a200f36745ab3d335edca02d
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 86%

---

# Descrizione del caso d’uso

Durante la creazione di moduli o applicazioni, spesso è utile guidare gli utenti attraverso la selezione della posizione in modo strutturato. Un elenco a discesa a cascata lo rende semplice e intuitivo: l’utente seleziona innanzitutto un paese, che filtra l’elenco di stati/province disponibili, e infine effettua la scelta di una città in base allo stato. Questo approccio non solo mantiene i moduli più puliti, ma impedisce anche combinazioni non valide (come la scelta di una città che non esiste in uno stato scelto).

Per eseguire questo caso d’uso sono necessari i seguenti passaggi

- Creare integrazione API
- Creare un modulo con campi per acquisire paese/stato/città
- Creare una regola per popolare gli elenchi a discesa utilizzando l’integrazione API