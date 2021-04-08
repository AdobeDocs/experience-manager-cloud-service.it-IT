---
title: 'Modifica di un programma sandbox '
description: Modifica di un programma sandbox
exl-id: e4545f7e-5329-40ad-81bb-a383c68f5d66
translation-type: tm+mt
source-git-commit: 8766b6fc6044a292b6dc7c2d9203a70d082edb01
workflow-type: tm+mt
source-wordcount: '237'
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

1. La pagina **Modifica programma** visualizza tre opzioni (**Siti** e **Risorse**) sia per i programmi Produzione che per i programmi Sandbox. Inoltre, puoi selezionare l&#39;opzione del componente aggiuntivo **Commerce** disponibile in **Sites**, come illustrato nella figura riportata di seguito.

   ![](assets/edit-prg.png)

   >[!NOTE]
   >È necessario selezionare almeno una soluzione per un programma, ovvero l&#39;utente non potrà deselezionare tutte le soluzioni durante il flusso di lavoro Modifica programma.

1. Fai clic su **Salva** per completare il processo del programma di modifica.


## Considerazioni durante la modifica di un programma {#considerations-editing}

Durante la modifica di un programma è necessario rivedere alcune considerazioni:

* È necessario selezionare almeno una soluzione per un programma, non sarà consentito deselezionare tutte le soluzioni durante il flusso di lavoro Modifica programma.

* Facendo clic sul pulsante **Salva**, se le soluzioni selezionate sono cambiate, gli aggiornamenti della soluzione agli ambienti avranno effetto dopo la distribuzione successiva.
