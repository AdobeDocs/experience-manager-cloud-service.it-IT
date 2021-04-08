---
title: 'Modifica di un programma di produzione '
description: Modifica di un programma di produzione
exl-id: 745c10af-f0a0-49e9-bb79-3fd058fad16c
translation-type: tm+mt
source-git-commit: 26cbd2369762050eb2e85d714b8f6b0ff129f171
workflow-type: tm+mt
source-wordcount: '258'
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

1. Fai clic sull&#39;opzione **Modifica programma** nella pagina *Panoramica* di Cloud Manager

   ![](assets/edit-program-overview.png)

1. Nella pagina **Modifica programma** sono visualizzate due schede **Generale** e **Soluzioni e componenti aggiuntivi**.

   Passa alla scheda **Generale** per modificare la descrizione del programma.

   ![](assets/edit-program-general.png)

   La scheda **Soluzioni e componenti aggiuntivi** visualizza due opzioni, ad esempio **Siti** e **Risorse** sia per i programmi Produzione che per i programmi sandbox. Inoltre, puoi selezionare l&#39;opzione del componente aggiuntivo **Commerce** disponibile in **Sites**, come illustrato nella figura riportata di seguito.

   ![](assets/edit-prg.png)

   >[!NOTE]
   >È necessario selezionare almeno una soluzione per un programma, ovvero l&#39;utente non potrà deselezionare tutte le soluzioni durante il flusso di lavoro Modifica programma.

1. Fai clic su **Salva** per completare il processo del programma di modifica.


## Considerazioni durante la modifica di un programma {#considerations-editing}

Durante la modifica di un programma è necessario rivedere alcune considerazioni:

* È necessario selezionare almeno una soluzione per un programma che non consenta all&#39;utente di deselezionare tutte le soluzioni durante il flusso di lavoro Modifica programma.

* Facendo clic sul pulsante **Salva**, se le soluzioni selezionate sono cambiate, gli aggiornamenti della soluzione agli ambienti avranno effetto dopo la distribuzione successiva.
