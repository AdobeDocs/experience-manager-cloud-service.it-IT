---
title: 'Aggiunta di utenti e assegnazione di ruoli di Cloud Manager '
description: Segui questa pagina per scoprire come aggiungere utenti e assegnarli ai ruoli di Cloud Manager
translation-type: tm+mt
source-git-commit: 6e8cf08ec3f85437a8472a45895f3818e473e98c
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 6%

---


# Aggiunta di utenti e assegnazione di ruoli di Cloud Manager {#add-users-assign}

Adobe creerà un identificatore **Organizzazione** per la società in Adobe Identity Management System (IMS), in cui è possibile gestire tutti gli utenti e le relative autorizzazioni. Ogni utente, che deve essere membro di questa organizzazione e avrà accesso a uno qualsiasi dei servizi [!UICONTROL Experience Cloud], dovrà disporre del proprio **Adobe ID**.

## Ruoli utente {#user-roles}

Molte funzionalità di Cloud Manager richiedono autorizzazioni specifiche per funzionare.

Cloud Manager definisce attualmente quattro ruoli per gli utenti che determinano la disponibilità di funzionalità specifiche:

* Business Owner (Proprietario)
* Deployment Manager (Responsabile implementazione)
* Program Manager (Responsabile programma)
* Developer (Sviluppatore)

>[!NOTE]
>La persona sviluppatore in Admin Console non è correlata al ruolo Sviluppatore in [!UICONTROL Cloud Manager].

La tabella seguente riepiloga i ruoli:

| [!UICONTROL Ruoli ] di Cloud Manager | Descrizione |
|--- |--- |
| Business Owner (Proprietario) | Responsabile della definizione dei KPI, dell’approvazione delle implementazioni di produzione e dell’override di importanti errori a 3 livelli. |
| Program Manager (Responsabile programma) | Utilizza [!UICONTROL Cloud Manager] per eseguire la configurazione del team, esaminare lo stato e visualizzare i KPI. Può approvare importanti errori a 3 livelli. |
| Deployment Manager (Responsabile implementazione) | Gestisce le operazioni di distribuzione. Utilizza [!UICONTROL Cloud Manager] per eseguire distribuzioni di stage/produzione. È possibile modificare le pipeline CI/CD. Può approvare importanti errori a 3 livelli. È possibile accedere all’archivio Git. |
| Developer (Sviluppatore) | Sviluppa e verifica il codice personalizzato dell’applicazione. Utilizza principalmente [!UICONTROL Cloud Manager] per visualizzare lo stato. Può accedere all’archivio Git per il commit del codice. |
| Autore del contenuto | In genere non interagisce con [!UICONTROL Cloud Manager]. Per accedere a AEM può essere utilizzato il commutatore di programma [!UICONTROL Cloud Manager] (dopo aver navigato da [!UICONTROL Experience Cloud]). |

### Profilo del prodotto di integrazione {#integration-product-profile}

Oltre a quanto sopra, Cloud Manager creerà automaticamente un profilo di prodotto denominato &quot;Integrazioni - Cloud Service&quot;. Questo profilo di prodotto viene utilizzato per le integrazioni tra Adobe Experience Manager e altri prodotti Adobe. Questo profilo di prodotto **non deve essere eliminato**. Se elimini accidentalmente questo profilo, dovrà essere ricreato manualmente. Il nome visualizzato per questo profilo **deve essere** `CM_CS_DEFAULT`.


## Autorizzazioni associate alle definizioni dei ruoli {#permissions}

[!UICONTROL Cloud Manager dispone di ruoli preconfigurati con le autorizzazioni appropriate. ] Ad esempio, uno sviluppatore sviluppa il codice e dispone dell&#39;autorizzazione per inviare il codice push al **Git Repository**. In alternativa, un proprietario aziendale dispone di autorizzazioni diverse che gli consentono di definire gli indicatori prestazioni chiave (KPI, Key Performance Indicators) e di approvare le distribuzioni.

A ciascun ruolo sono associate autorizzazioni specifiche. La tabella seguente riepiloga i ruoli, elenca le funzioni disponibili e i ruoli che possono eseguire la funzione.

| Autorizzazione | Descrizione | Business Owner (Proprietario) | Deployment Manager (Responsabile implementazione) | Program Manager (Responsabile programma) | Developer (Sviluppatore) |
|--- |--- |--- |--- |--- |--- |
| Aggiungi programma | Aggiungi un nuovo programma. | x |  |  |  |
| Creare un ambiente | Crea Prod+Stage, Sviluppo, Ambienti. | x | x |  |  |
| Ambiente di aggiornamento | Aggiorna Prod+Stage, Dev, Ambienti. | x | x |  |  |
| Elimina ambiente | Elimina ambienti non prod, sviluppo e non. | x | x |  |  |
| Configurazione della pipeline | Impostare o modificare la pipeline. |  | x |  |  |
| Esecuzione della pipeline | Avvia la pipeline. | x | x |  |  |
| Esecuzione della pipeline | Rifiutare/Approvare Importanti Errori A 3 Livelli. | x | x | x |  |
| Esecuzione della pipeline | Fornire l’approvazione GoLive. | x | x | x |  |
| Esecuzione della pipeline | Pianificazione distribuzione produzione. | x | x | x |  |
| Elimina pipeline | Consente di eliminare una pipeline. |  | x |  |  |
| Annulla esecuzione | Annulla esecuzione corrente. |  | x |  |  |
| Genera token di accesso personale | Accedi a Git. |  | x |  | x |

## Aggiunta di utenti {#add-users}

>[!NOTE]
>Per aggiungere un utente è necessario essere un amministratore di sistema.

1. Se sei un amministratore di sistema, passa a [Admin Console](https://adminconsole.adobe.com). In alternativa, puoi anche passare a Cloud Manager e visualizzare il pulsante **Gestione accesso** , come descritto di seguito.

1. Fai clic sul pulsante **Gestisci accesso**, in alto a destra nella pagina di destinazione di Cloud Manager, per aprire Admin Console in una nuova scheda.

   ![](/help/onboarding/getting-access-to-aem-in-cloud/assets/sys-admin5.png)

   Dall’ **Admin Console**, puoi aggiungere utenti a Cloud Manager e assegnarli a Ruoli, denominati ad Admin Console Profili di prodotto .

1. Seleziona **Adobe Experience Manager come Cloud Service** dalla scheda **Prodotti e servizi** come mostrato di seguito.

   ![](/help/onboarding/what-is-required/assets/admin-console-1.png)

1. Seleziona la scheda **Utenti** dalla barra delle azioni, quindi seleziona **Aggiungi utente**.

   ![](/help/onboarding/what-is-required/assets/admin-console-2.png)

1. Seleziona l’utente e assegna all’utente i ruoli o i profili di prodotto Cloud Manager appropriati, come illustrato di seguito.

   ![](/help/onboarding/what-is-required/assets/admin-console-3.png)

   >[!NOTE]
   >Consulta le sezioni precedenti, [Ruoli utente e autorizzazioni](#user-roles) e [Autorizzazioni associate alle definizioni dei ruoli](#permissions) per assicurarti che agli utenti giusti siano assegnati i Ruoli giusti nell&#39; **Admin Console**.

   Ora hai aggiunto gli utenti a Adobe Experience Manager as a Cloud Service Product Context e sei configurato con i ruoli o i profili di prodotto giusti.

   Ad esempio, se ti trovi nel ruolo di un:

   * ***Proprietario business***, disponi dell’autorizzazione per aggiungere un nuovo programma o modificare un programma, aggiungere o aggiornare un ambiente, aggiungere/modificare/eliminare la pipeline ed eseguire qualsiasi pipeline e distribuire il codice per AEM ambiente o qualità del codice.

   * ***Deployment Manager***, è disponibile l’autorizzazione per aggiungere o aggiornare un ambiente, eseguire una pipeline e distribuire il codice per AEM ambiente o qualità del codice.

   * ***Sviluppatore***, disponi dell’autorizzazione per generare Token di accesso personale per accedere a Git.

      >[!NOTE]
      > Un utente può essere assegnato a più ruoli. Ad esempio, l&#39;assegnazione di ruoli Business Owner (Proprietario business) e Deployment Manager a un utente fornisce loro la combinazione o la somma di queste autorizzazioni.
