---
title: Gestione degli ambienti - Cloud Service
description: Gestione degli ambienti - Cloud Service
translation-type: tm+mt
source-git-commit: fb979363fcb8c17fbefd11b9b86498447593f745
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 6%

---


# Gestione degli ambienti {#manage-environments}

La sezione seguente descrive i tipi di ambiente che un utente può creare e come l&#39;utente può creare un ambiente.

## Tipi di ambiente {#environment-types}

Un utente con le autorizzazioni richieste può creare i seguenti tipi di ambiente (entro i limiti di ciò che è disponibile per il tenant specifico).

* **Ambiente** di produzione e fase: La produzione e lo stage sono disponibili come due elementi e sono utilizzati a scopo di test e produzione.

* **Sviluppo**: Un ambiente di sviluppo può essere creato a scopo di sviluppo e test e sarà associato solo a condotte non di produzione.

   >[!NOTE]
   >Un ambiente di sviluppo creato automaticamente in un programma sandbox sarà configurato per includere le soluzioni Siti e Risorse.

   Nella tabella seguente sono riepilogati i tipi di ambiente e i relativi attributi:

   | Nome | Livello di authoring | Pubblica livello | Utente può creare | L&#39;utente può eliminare | Pipeline che può essere associata all&#39;ambiente |
   |--- |--- |--- |--- |---|---|
   | Produzione | Sì | Sì se Siti inclusi | Sì | No | pipeline di produzione |
   | Area di visualizzazione | Sì | Sì se Siti inclusi | Sì | No | pipeline di produzione |
   | Sviluppo | Sì | Sì se Siti inclusi | Sì | Sì | pipeline non di produzione |

   >[!NOTE]
   >La produzione e lo stage sono disponibili come due elementi e sono utilizzati a scopo di test e produzione.  L&#39;utente non sarà in grado di creare solo l&#39;ambiente Stage o solo l&#39;ambiente Production.

## Aggiunta di un ambiente {#adding-environments}

1. Fare clic su **Aggiungi ambiente** per aggiungere un ambiente. Questo pulsante sarà accessibile dalla schermata **Ambienti**.
   ![](assets/environments-tab.png)

   L&#39;opzione **Aggiungi ambiente** è disponibile anche sulla scheda **Ambienti** quando il programma non contiene alcun ambiente.

   ![](assets/no-environments.png)

   >[!NOTE]
   >L&#39;opzione **Aggiungi ambiente** verrà disattivata in base alla mancanza di autorizzazioni o agli eventuali contratti.

1. Viene visualizzata la finestra di dialogo **Aggiungi ambiente**. L’utente deve inviare dettagli quali **tipo di ambiente**, **nome dell’ambiente** e **descrizione dell’ambiente** (a seconda dell’obiettivo dell’utente nella creazione dell’ambiente ed entro i limiti di ciò che è disponibile per il tenant specifico).

   ![](assets/add-environment2.png)

   >[!NOTE]
   >Durante la creazione di un ambiente, in  Adobe I/O vengono create una o più *integrazioni*. Questi sono visibili agli utenti del cliente che hanno accesso alla  Adobe I/O Console e non devono essere eliminati. Questo viene negato nella descrizione nella  Adobe I/O Console.

   ![](assets/add-environment-image1.png)

1. Fare clic su **Salva** per aggiungere un ambiente con i criteri popolati.  A questo punto, nella schermata *Panoramica* viene visualizzata la scheda da cui è possibile impostare la pipeline.

   >[!NOTE]
   >Se non avete ancora impostato la pipeline di non produzione, nella schermata *Panoramica* viene visualizzata la scheda da cui potete creare la pipeline non di produzione.


## Ambiente di visualizzazione {#viewing-environment}

La scheda **Ambienti** nella pagina Panoramica elenca fino a tre ambienti.

1. Selezionare il pulsante **Mostra tutto** per passare alla pagina di riepilogo **Ambiente** per visualizzare una tabella con un elenco completo degli ambienti.

   ![](assets/environment-view-1.png)

1. Nella pagina **Ambienti** viene visualizzato l&#39;elenco di tutti gli ambienti esistenti.

   ![](assets/environment-view-2.png)

1. Selezionare uno degli ambienti elencati per visualizzare i dettagli dell&#39;ambiente.

   ![](assets/environment-view-3.png)


## Aggiornamento dell&#39;ambiente {#updating-dev-environment}

Gli aggiornamenti degli ambienti Stage e Produzione vengono gestiti automaticamente da  Adobe.

Gli aggiornamenti agli ambienti di sviluppo sono gestiti dagli utenti del programma. Se un ambiente non esegue l&#39;ultima versione AEM disponibile al pubblico, lo stato della scheda Ambienti nella Home Screen mostrerà **UPDATE AVAILABLE**.

![](assets/environ-update.png)


L&#39;opzione **Aggiorna** è disponibile dalla scheda **Ambienti**.
Questa opzione è disponibile anche, se si fa clic su **Dettagli** dalla scheda **Ambienti**. Viene visualizzata la pagina **Ambienti** e, dopo aver selezionato l&#39;ambiente di sviluppo, fare clic su **...** e selezionare **Aggiorna**, come illustrato nella figura seguente:

![](assets/environ-update2.png)

Selezionando questa opzione, un gestore distribuzione potrà aggiornare la pipeline associata a questo ambiente alla versione più recente ed eseguire la pipeline.

Se la pipeline è già stata aggiornata, all&#39;utente viene richiesto di eseguire la pipeline.

## Eliminazione dell&#39;ambiente {#deleting-environment}

L&#39;utente con le autorizzazioni necessarie sarà in grado di eliminare un ambiente di sviluppo.

L&#39;opzione **Elimina** è disponibile dal menu a discesa nella scheda **Ambienti**. Fare clic su **...** per un ambiente di sviluppo da eliminare.

![](assets/environ-delete.png)

L&#39;opzione di eliminazione è disponibile anche, se si fa clic su **Details** dalla scheda **Environment**. Viene visualizzata la pagina **Ambienti** e, dopo aver selezionato l&#39;ambiente di sviluppo, fare clic su **...** e selezionare **Elimina**, come illustrato nella figura seguente:

![](assets/environ-delete2.png)


>[!NOTE]
>
>Questa funzione non è disponibile per l&#39;ambiente Produzione/Fase impostato in un programma regolare impostato a scopo di produzione. La funzione è tuttavia disponibile per gli ambienti Produzione/Fase in un programma sandbox.

## Gestione dell&#39;accesso {#managing-access}

Selezionare **Gestisci accesso** dal menu a discesa nella scheda **Ambienti**. Potete passare direttamente all’istanza di authoring e gestire l’accesso all’ambiente in uso.

Per ulteriori informazioni, fare riferimento a [Managing Access to Author Instance](/help/onboarding/getting-access-to-aem-in-cloud/navigation.md#manage-access-aem) (Gestione dell&#39;accesso all&#39;istanza Author).

![](assets/environ-access.png)


## Accesso alla console per sviluppatori {#accessing-developer-console}

Selezionare **Developer Console** dal menu a discesa nella scheda **Ambienti**. In questo modo si aprirà una nuova scheda nel browser con la pagina di accesso su **Developer Console**.

Solo un utente nel ruolo Sviluppatore avrà accesso a **Developer Console**. Eccezione per i programmi sandbox, in cui qualsiasi utente con accesso al Programma sandbox di Cloud Manager avrà accesso a **Developer Console**.

Per ulteriori informazioni, fare riferimento a [Ambienti sandbox in sospensione e in sospensione](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/sandbox-programs.html#hibernating-introduction).


![](assets/environ-devconsole.png)

Questa opzione è disponibile anche, se si fa clic su **Dettagli** dalla scheda **Ambienti**. Viene visualizzata la pagina **Ambienti** e, dopo aver selezionato un ambiente, fare clic su **...** e selezionare **Developer Console**.

## Login Locale {#login-locally}

Selezionare **Accesso locale** dal menu a discesa nella scheda **Ambienti** per accedere localmente ad Adobe Experience Manager.

![](assets/environ-login-locally.png)

È inoltre possibile accedere localmente dalla pagina di riepilogo **Ambienti**.

![](assets/environ-login-locally-2.png)

