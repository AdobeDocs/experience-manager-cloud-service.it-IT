---
title: 'Modifica di un programma sandbox '
description: 'Modifica di un programma sandbox '
translation-type: tm+mt
source-git-commit: 751f611ecccc39ef4650a1c7a9941655a6b2aedd
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Modifica di un programma sandbox {#create-sandbox-program}

Gli utenti con le autorizzazioni necessarie possono ora modificare un programma di produzione, consentendo loro di effettuare le seguenti operazioni in modalità self-service:

* Aggiungi la soluzione Sites a un programma esistente con Assets (o viceversa).
* Rimuovi Sites (o Assets) da un programma esistente sia con Sites che con Assets.
* Aggiungi il secondo diritto inutilizzato alla soluzione a un programma esistente o a un nuovo programma.

   >[!NOTE]
   >Per modificare correttamente il programma, è necessario che un utente con il ruolo Proprietario business sia connesso.

Per modificare un programma Sandbox, effettua le seguenti operazioni:

1. Passa alla pagina **Modifica programma** dalla pagina *Panoramica* di Cloud Manager.

1. Nella pagina **Modifica programma** sono visualizzate due schede (Generale e Soluzioni) sia per i programmi Produzione che per quelli Sandbox.
   ![](assets/edit-program.png)


## Considerazioni durante la modifica di un programma {#considerations-editing}

Durante la modifica di un programma è necessario rivedere alcune considerazioni:

* È necessario selezionare almeno una soluzione per un programma, non sarà consentito deselezionare tutte le soluzioni durante il flusso di lavoro Modifica programma.

* Facendo clic sul pulsante **Salva**, se le soluzioni selezionate sono cambiate, gli aggiornamenti della soluzione agli ambienti avranno effetto dopo la distribuzione successiva.