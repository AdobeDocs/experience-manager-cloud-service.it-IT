---
title: Configurare l’Assistente IA in Adobe Experience Manager
description: Scopri come impostare e configurare l’Assistente AI utilizzando Admin Console in Adobe Experience Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: ab8fefe18e43c1fe937d0d16df65b6137fc8a292
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 3%

---

# Configurare AEM AI Assistant - Installazione dell’amministratore {#aem-ai-asst-admin-setup}

Un amministratore deve configurare l’accesso, le autorizzazioni e le impostazioni prima che gli utenti della propria organizzazione possano utilizzare le funzioni di AEM AI Assistant. Questo articolo descrive come abilitare l’Assistente AI per la tua organizzazione, impostare le credenziali richieste e salvare le modifiche alla configurazione.

**Panoramica del processo di configurazione dell&#39;Assistente di intelligenza artificiale di AEM**

Il processo di configurazione è costituito dai seguenti passaggi:

1. Creare un nuovo profilo di prodotto in Adobe Admin Console.
1. Abilita l’autorizzazione &quot;Conoscenza del prodotto di AI Assistant&quot;.
1. Crea o utilizza un gruppo di utenti esistente.
1. Aggiungere utenti al gruppo di utenti.
1. Assegna il profilo di prodotto al gruppo di utenti.

**Prerequisiti**

Prima di iniziare, assicurati di aver soddisfatto i seguenti prerequisiti:

* Devi disporre almeno dei diritti di amministratore di prodotto in Adobe Admin Console.
* Conosci la struttura di gestione degli utenti della tua organizzazione.

## 1 - Creare un nuovo profilo di prodotto in Adobe Admin Console{#create-profile}

1. Segui le istruzioni dettagliate in [Creazione di un nuovo profilo di prodotto in Adobe Admin Console](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/create-profile). Trovata la documentazione di Experience Platform.

1. Quando crei il nuovo profilo di prodotto, utilizza i seguenti esempi dei valori che puoi utilizzare per l’Assistente AI.

   | Campo testo | Valore suggerito |
   | --- | --- |
   | Nome del profilo di prodotto | `AEM AI Assistant` (o il tuo nome descrittivo preferito) |
   | Nome visualizzato (facoltativo) | `AI Assistant` |
   | Descrizione (facoltativo) | `Product profile for managing AEM AI Assistant access` |
   | Notifica | Configura in base alle preferenze della tua organizzazione |




## 2 - Abilitare l’autorizzazione &quot;Conoscenza del prodotto di AI Assistant&quot;{#enable-permission}

Il processo di assegnazione di autorizzazioni personalizzate ai profili di prodotto segue il flusso di lavoro standard delle autorizzazioni personalizzate di Adobe Cloud Manager.

Articolo di riferimento: [Assegnare autorizzazioni personalizzate al nuovo profilo di prodotto](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

1. In Admin Console, fai clic sul nome del nuovo profilo di prodotto creato (`AEM AI Assistant`)

   ![Schermata](/help/implementing/cloud-manager/assets/ai-assistant-console.png)

1. Per visualizzare l&#39;elenco delle autorizzazioni modificabili, fare clic sulla scheda **Autorizzazioni**.

1. Nell&#39;elenco della tabella individuare l&#39;autorizzazione `AI Assistant Product Knowledge`.

   ![Scheda Autorizzazioni Assistente AI in Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-permission.png)

1. A destra del nome dell&#39;autorizzazione, fare clic sull&#39;icona ![Matita o Modifica](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg).

1. Nella pagina **Modifica autorizzazioni per Assistente IA**, attiva l&#39;opzione **Informazioni sul prodotto Assistente IA**.

   ![Modifica pagina autorizzazioni per l&#39;opzione di attivazione/disattivazione della Knowledge Base di AI Assistant](/help/implementing/cloud-manager/assets/ai-assistant-prod-knowledge.png)

1. Nell&#39;angolo inferiore destro della pagina fare clic su **Salva**.

   Il tuo profilo di prodotto ora dispone dell’autorizzazione alla conoscenza del prodotto di AI Assistant abilitata.


## 3 - Creare un gruppo di utenti (o utilizzare un gruppo di utenti esistente){#create-user-group}

1. Effettua una delle seguenti operazioni:

>[!BEGINTABS]

>[!TAB Crea un nuovo gruppo di utenti]

1. In Admin Console, fai clic su **Utenti** > **Gruppi di utenti**.

   ![Gruppi di utenti](/help/implementing/cloud-manager/assets/ai-assistant-user-groups.png)

1. Nella pagina **Gruppi utenti**, fai clic su **Nuovo gruppo utenti**.

   ![Pulsante Nuovo gruppo utenti nella pagina Gruppi utenti](/help/implementing/cloud-manager/assets/ai-assistant-new-user-group.png)

1. Nella pagina **Crea un nuovo gruppo di utenti**, fornisci le seguenti informazioni:

   | Opzione | Valore suggerito |
   | --- | --- |
   | Nome gruppo di utenti | `AEM AI Assistant` (o il tuo nome preferito) |
   | Descrizione (facoltativo) | `User group for managing AEM AI Assistant access` |

   ![Crea una nuova pagina gruppo utenti](/help/implementing/cloud-manager/assets/ai-assistant-create-new-user-group.png)

1. Nell&#39;angolo inferiore destro della pagina fare clic su **Salva**.

>[!TAB Utilizza un gruppo di utenti esistente]

Invece di creare un nuovo gruppo, puoi utilizzare un gruppo di utenti AEM esistente se soddisfa i requisiti di accesso all’Assistente IA.

>[!ENDTABS]

## 4 - Aggiungere utenti al gruppo{#add-users}

1. Effettua una delle seguenti operazioni:

>[!BEGINTABS]

>[!TAB Aggiungi singoli utenti]

1. Nella tabella **Nome gruppo** della pagina **Gruppi utenti** fare clic sul nome del gruppo utenti appena creato o su un nome di gruppo utenti esistente.

   ![Pagina Gruppi di utenti che mostra il nome del gruppo di utenti dell&#39;Assistente di AEM AI nella tabella](/help/implementing/cloud-manager/assets/ai-assistant-user-group-name-in-table.png)

1. Nella pagina **Gruppi di utenti** per l&#39;**Assistente di AEM AI**, fai clic sulla scheda **Utenti**, quindi su **Aggiungi utenti**.

   ![La pagina dei gruppi di utenti dell&#39;Assistente di AEM AI mostra la scheda Utenti e il pulsante Aggiungi utenti](/help/implementing/cloud-manager/assets/ai-assistant-add-users.png)

1. Nella pagina **Aggiungi utenti a questo gruppo di utenti**, cerca e seleziona gli utenti che devono accedere all&#39;Assistente di AEM AI.

   ![Aggiungi utenti a questa pagina gruppo utenti](/help/implementing/cloud-manager/assets/ai-assistant-add-users-to-this-group.png)

1. Nell&#39;angolo inferiore destro della pagina fare clic su **Salva**.

>[!TAB Aggiungere utenti in blocco]

Puoi utilizzare la funzione di caricamento in blocco in Admin Console.

1. Prepara un file CSV con le informazioni utente.

1. Utilizza l&#39;opzione **Aggiungi utenti per CSV** per un&#39;aggiunta in blocco efficiente.

>[!ENDTABS]




## 5 - Assegnare il profilo di prodotto al gruppo di utenti{#assign-product-profile}




