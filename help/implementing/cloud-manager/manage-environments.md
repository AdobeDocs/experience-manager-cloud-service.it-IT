---
title: Gestisci ambienti - Cloud Service
description: Gestisci ambienti - Cloud Service
exl-id: 93fb216c-c4a7-481a-bad6-057ab3ef09d3
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 4%

---

# Gestione degli ambienti {#manage-environments}

La sezione seguente descrive i tipi di ambiente che un utente può creare e come l’utente può creare un ambiente.

## Tipi di ambiente {#environment-types}

Un utente con le autorizzazioni necessarie può creare i seguenti tipi di ambiente (entro i limiti di ciò che è disponibile per il tenant specifico).

* **Ambiente** di produzione e fase: La fase di produzione è disponibile come duo e viene utilizzata a scopo di test e produzione.

* **Sviluppo**: Un ambiente di sviluppo può essere creato a scopo di sviluppo e test e sarà associato solo alle pipeline non di produzione.

   >[!NOTE]
   >Un ambiente di sviluppo creato automaticamente in un programma sandbox verrà configurato per includere le soluzioni Sites e Assets.

   La tabella seguente riepiloga i tipi di ambiente e i relativi attributi:

   | Nome | Livello di authoring | Livello di pubblicazione | Utente può creare | L&#39;utente può eliminare | Pipeline che può essere associata all’ambiente |
   |--- |--- |--- |--- |---|---|
   | Produzione | Sì | Sì se Sites include | Sì | No | pipeline di produzione |
   | Area di visualizzazione | Sì | Sì se Sites include | Sì | No | pipeline di produzione |
   | Sviluppo | Sì | Sì se Sites include | Sì | Sì | pipeline non di produzione |

   >[!NOTE]
   >La fase di produzione è disponibile come duo e viene utilizzata a scopo di test e produzione.  L’utente non sarà in grado di creare solo l’ambiente Stage o di produzione.

## Aggiunta di ambiente {#adding-environments}

1. Fai clic su **Aggiungi ambiente** per aggiungere un ambiente. Questo pulsante sarà accessibile dalla schermata **Ambienti** .
   ![](assets/environments-tab.png)

   L&#39;opzione **Aggiungi ambiente** è disponibile anche nella scheda **Ambienti** quando il programma non contiene ambienti.

   ![](assets/no-environments.png)

   >[!NOTE]
   >L&#39;opzione **Aggiungi ambiente** verrà disabilitata per mancanza di autorizzazioni o per elementi che possono essere oggetto di contratti.

1. Viene visualizzata la finestra di dialogo **Aggiungi ambiente**. L’utente deve inviare dettagli quali **tipo di ambiente**, **nome dell’ambiente** e **descrizione dell’ambiente** (a seconda dell’obiettivo dell’utente nella creazione dell’ambiente ed entro i limiti di ciò che è disponibile per il tenant specifico).

   ![](assets/add-environment2.png)

   >[!NOTE]
   >Durante la creazione di un ambiente, in Adobe I/O vengono create una o più *integrazioni* . Questi sono visibili agli utenti che hanno accesso alla console Adobe I/O e non devono essere eliminati. Questa operazione è sconosciuta nella descrizione nella console Adobe I/O.

   ![](assets/add-environment-image1.png)

1. Fai clic su **Salva** per aggiungere un ambiente con i criteri popolati.  Ora nella schermata *Panoramica* viene visualizzata la scheda da cui è possibile impostare la pipeline.

   >[!NOTE]
   >Nel caso in cui non sia ancora stata impostata la pipeline non di produzione, nella schermata *Panoramica* viene visualizzata la scheda da cui è possibile creare la pipeline non di produzione.


## Dettagli ambiente {#viewing-environment}

La scheda **Ambienti** nella pagina Panoramica elenca fino a tre ambienti.

1. Selezionare il pulsante **Mostra tutto** per passare alla pagina di riepilogo **Ambiente** per visualizzare una tabella con un elenco completo di ambienti.

   ![](assets/environment-view-1.png)

1. La pagina **Ambienti** visualizza l&#39;elenco di tutti gli ambienti esistenti.

   ![](assets/environment-view-2.png)

1. Seleziona uno qualsiasi degli ambienti dall’elenco per visualizzare i dettagli dell’ambiente.

   ![](assets/environment-view-3.png)


## Aggiornamento dell&#39;ambiente {#updating-dev-environment}

Gli aggiornamenti degli ambienti Stage e Production vengono gestiti automaticamente da Adobe.

Gli aggiornamenti agli ambienti di sviluppo sono gestiti dagli utenti del programma. Quando un ambiente non esegue l&#39;ultima versione AEM disponibile al pubblico, lo stato della scheda Ambienti nella schermata principale verrà visualizzato **AGGIORNA DISPONIBILE**.

![](assets/environ-update.png)


L&#39;opzione **Aggiorna** è disponibile dalla scheda **Ambienti** .
Questa opzione è disponibile anche se fai clic su **Dettagli** dalla scheda **Ambienti** . Viene visualizzata la pagina **Ambienti** e, dopo aver selezionato l&#39;ambiente di sviluppo, fai clic su **...** e seleziona **Aggiorna**, come illustrato nella figura seguente:

![](assets/environ-update2.png)

Selezionando questa opzione, un gestore distribuzione potrà aggiornare la pipeline associata a questo ambiente alla versione più recente ed eseguire la pipeline.

Se la pipeline è già stata aggiornata, all’utente viene richiesto di eseguire la pipeline.

## Eliminazione dell&#39;ambiente {#deleting-environment}

L&#39;utente con le autorizzazioni necessarie potrà eliminare un ambiente di sviluppo.

L&#39;opzione **Elimina** è disponibile dal menu a discesa nella scheda **Ambienti** . Fai clic su **..** per un ambiente di sviluppo da eliminare.

![](assets/environ-delete.png)

È disponibile anche l’opzione Elimina, se fai clic su **Dettagli** dalla scheda **Ambienti** . Viene visualizzata la pagina **Ambienti** e, dopo aver selezionato l&#39;ambiente di sviluppo, fai clic su **...** e seleziona **Elimina**, come illustrato nella figura seguente:

![](assets/environ-delete2.png)


>[!NOTE]
>Questa funzione non è disponibile per l’ambiente Produzione/Stage impostato in un programma di produzione configurato a scopo di produzione. La funzione è tuttavia disponibile per gli ambienti di produzione/stage in un programma sandbox.

## Gestione dell&#39;accesso {#managing-access}

Seleziona **Gestisci accesso** dal menu a discesa nella scheda **Ambienti**. Puoi passare direttamente all’istanza di authoring e gestire l’accesso per il tuo ambiente.

Per ulteriori informazioni, consulta [Gestione dell’accesso all’istanza di authoring](/help/onboarding/what-is-required/accessing-aem-instance.md) .

![](assets/environ-access.png)


## Accesso alla Console per sviluppatori {#accessing-developer-console}

Seleziona **Console per sviluppatori** dal menu a discesa nella scheda **Ambienti** . Verrà aperta una nuova scheda nel browser con la pagina di accesso a **Console per sviluppatori**.

Solo un utente con il ruolo Sviluppatore avrà accesso a **Console per sviluppatori**. Eccezione per i programmi sandbox, in cui qualsiasi utente con accesso al programma sandbox di Cloud Manager avrà accesso a **Console per sviluppatori**.

Per ulteriori informazioni, consulta [Sospensione e disattivazione degli ambienti sandbox](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/sandbox-programs.html#hibernating-introduction) .


![](assets/environ-devconsole.png)

Questa opzione è disponibile anche se fai clic su **Dettagli** dalla scheda **Ambienti** . Viene visualizzata la pagina **Ambienti** e, dopo aver selezionato un ambiente, fai clic su **...** e seleziona **Console per sviluppatori**.

## Accedi localmente {#login-locally}

Seleziona **Accesso locale** dal menu a discesa nella scheda **Ambienti** per accedere localmente ad Adobe Experience Manager.

![](assets/environ-login-locally.png)

Inoltre, puoi accedere localmente dalla pagina di riepilogo **Ambienti**.

![](assets/environ-login-locally-2.png)

## Gestione dei nomi di dominio personalizzati {#manage-cdn}

Passa alla pagina dei dettagli **Ambienti** dalla pagina Riepilogo ambienti .

Le seguenti azioni possono essere eseguite sul servizio Publish per il tuo ambiente come descritto di seguito:

1. [Aggiunta di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)

1. [Visualizzazione e aggiornamento di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.md)

1. [Eliminazione di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)

1. [Controllo dello stato del nome di dominio personalizzato ](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) o di un certificato [ ](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn)SSL.

1. [Controllo dello stato di un Elenco consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn)

## Gestione degli Elenchi consentiti IP {#manage-ip-allow-lists}

Passa alla pagina dei dettagli dell’ambiente dalla pagina Riepilogo ambienti . Puoi eseguire le seguenti operazioni sui servizi di pubblicazione e/o authoring per il tuo ambiente qui.

### Applicazione di un Elenco consentiti IP {#apply-ip-allow-list}

L’applicazione di un Elenco consentiti IP è il processo tramite il quale tutti gli intervalli IP inclusi nella definizione dell’elenco consentiti sono associati a un servizio Author o Publish in un ambiente. Per poter applicare un Elenco consentiti IP, è necessario accedere a un utente con il ruolo Proprietario business o Gestore distribuzione.

>[!NOTE]
>L’Elenco consentiti IP deve esistere in Cloud Manager per applicarlo a un servizio ambiente. Per ulteriori informazioni sugli Elenchi consentiti IP in Cloud Manager, passa a [Introduzione agli Elenchi consentiti IP in Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

Per applicare un Elenco consentiti IP, effettua le seguenti operazioni:

1. Passa all’ambiente specifico dalla pagina dei dettagli **Ambienti** e passa alla tabella **Elenchi consentiti IP** .
1. Utilizza i campi di input nella parte superiore della tabella dell’Elenco consentiti IP per selezionare l’Elenco consentiti IP e il servizio Author o Publish a cui desideri applicarlo.
1. Fai clic su **Applica** e conferma l’invio.

### Annullamento dell&#39;applicazione di un Elenco consentiti IP {#unapply-ip-allow-list}

L&#39;annullamento dell&#39;applicazione di un Elenco consentiti IP è il processo tramite il quale tutti gli intervalli IP inclusi nella definizione dell&#39;Elenco consentiti vengono disassociati da un servizio Author o Publisher in un ambiente. Per poter annullare l’applicazione di un Elenco consentiti IP, è necessario che un utente con il ruolo Proprietario business o Gestore distribuzione sia connesso.

Per annullare l’applicazione di un Elenco consentiti IP, effettua le seguenti operazioni:

1. Passa alla pagina dei dettagli **Ambienti** specifica dalla schermata Ambienti e passa alla tabella **Elenchi consentiti IP** .
1. Identifica la riga in cui è elencata la regola dell’Elenco consentiti IP che desideri annullare l’applicazione.
1. Seleziona il **...Menu** dall&#39;estremità destra della riga.
1. Seleziona l’opzione **Annulla applicazione** e conferma l’invio.
