---
title: 'Modifica di un programma di produzione '
description: 'Modifica di un programma di produzione '
translation-type: tm+mt
source-git-commit: c34b9cbd019ee74059e13be4f19c1bb9a54fa2ba
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# Modifica di un programma di produzione {#create-production-program}

Gli utenti con le autorizzazioni necessarie possono ora modificare un programma di produzione, consentendo loro di effettuare le seguenti operazioni in modalità self-service:

* Aggiungi la soluzione Sites a un programma esistente con Assets (o viceversa).
* Rimuovi Sites (o Assets) da un programma esistente sia con Sites che con Assets.
* Aggiungi il secondo diritto inutilizzato alla soluzione a un programma esistente o a un nuovo programma.

   >[!NOTE]
   >Per modificare correttamente il programma, è necessario che un utente con il ruolo Proprietario business sia connesso.

Segui i passaggi seguenti per modificare un programma di produzione:

1. Passa alla pagina **Modifica programma** dalla pagina *Panoramica* di Cloud Manager

1. Nella pagina **Modifica programma** vengono visualizzate due schede (Generale e Soluzioni) sia per i programmi Produzione che per i programmi Sandbox.

   ![](assets/edit-program.png)

   >[!NOTE]
   >Anche se verranno visualizzati sia Sites che Assets, uno di questi potrebbe essere disabilitato in base a ciò che è stato acquistato e non utilizzato. In particolare, se l&#39;organizzazione non dispone di diritti inutilizzati per una particolare soluzione, questa verrà visualizzata ma disabilitata.

## Considerazioni durante la modifica di un programma {#considerations-editing}

Durante la modifica di un programma è necessario rivedere alcune considerazioni:

* È necessario selezionare almeno una soluzione per un programma, non sarà consentito deselezionare tutte le soluzioni durante il flusso di lavoro Modifica programma.

* Facendo clic sul pulsante **Salva**, se le soluzioni selezionate sono cambiate, gli aggiornamenti della soluzione agli ambienti avranno effetto dopo la distribuzione successiva.