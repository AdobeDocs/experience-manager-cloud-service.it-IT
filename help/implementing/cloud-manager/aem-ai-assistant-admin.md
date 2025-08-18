---
title: Configurare l’Assistente IA in Adobe Experience Manager
description: Scopri come impostare e configurare l’Assistente IA utilizzando Admin Console in Adobe Experience Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: a7f3dc14-29f7-473a-9870-d52393e6fa6e
source-git-commit: e853e7b46c762ab724d5eecb344897a83e4fb724
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 3%

---

# Configurare l’Assistente IA in Adobe Experience Manager {#aem-ai-asst-admin-setup}

Un amministratore deve configurare l’accesso, le autorizzazioni e le impostazioni prima che gli utenti della propria organizzazione possano utilizzare le funzioni dell’Assistente IA di AEM (Adobe Experience Manager).

Il processo di configurazione dell’Assistente di intelligenza artificiale di AEM consiste nei seguenti passaggi:

1. [Crea un nuovo profilo di prodotto in Adobe Admin Console](#create-profile).
1. [Abilitare l&#39;autorizzazione alla conoscenza del prodotto dell&#39;Assistente all&#39;intelligenza artificiale](#enable-permission).
1. [Creare un nuovo gruppo utenti (o utilizzare un gruppo utenti esistente)](#create-user-group).
1. [Aggiungi utenti al gruppo di utenti](#add-users).
1. [Assegna il profilo di prodotto al gruppo di utenti](#assign-product-profile).

**Prerequisiti**

Prima di iniziare, assicurati di aver soddisfatto i seguenti prerequisiti:

* Devi disporre almeno dei diritti di amministratore di prodotto in Adobe Admin Console.
* Conosci la struttura di gestione degli utenti della tua organizzazione.

**Considerazioni sulla configurazione**

* Tempo di elaborazione: le risorse create in Cloud Manager potrebbero richiedere fino a 2 minuti per essere visualizzate in Admin Console per la configurazione delle autorizzazioni.
* Più profili: gli utenti possono far parte di più profili e le autorizzazioni sono combinate da tutti i profili assegnati.
* Ambito organizzazione: alcune autorizzazioni possono essere applicate a livello di organizzazione in tutti i programmi.
* Profili predefiniti: non eliminare i profili di autorizzazione predefiniti da Admin Console.


## 1 - Creare un nuovo profilo di prodotto in Adobe Admin Console{#create-profile}

1. Segui le istruzioni dettagliate in [Creare un nuovo profilo di prodotto in Adobe Admin Console](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/create-profile), reperibile nella documentazione di Experience Platform.

1. Quando crei il nuovo profilo di prodotto, puoi utilizzare i seguenti valori consigliati per l’Assistente IA.

   | Campo testo | Valore suggerito |
   | --- | --- |
   | Nome del profilo di prodotto | `AEM AI Assistant` (o il tuo nome descrittivo preferito) |
   | Nome visualizzato (facoltativo) | `AI Assistant` |
   | Descrizione (facoltativo) | `Product profile for managing AEM AI Assistant access` |
   | Notifica | Configura in base alle preferenze della tua organizzazione |


## 2 - Abilitare l’autorizzazione alla conoscenza del prodotto di AI Assistant{#enable-permission}

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


## 3 - Creare un nuovo gruppo di utenti (o utilizzare un gruppo di utenti esistente){#create-user-group}

1. Effettua una delle seguenti operazioni:

>[!BEGINTABS]

>[!TAB Crea un nuovo gruppo di utenti]

1. In Admin Console, fai clic su **Utenti** > **Gruppi di utenti**.

   ![Gruppi di utenti](/help/implementing/cloud-manager/assets/ai-assistant-user-groups.png)

1. Nella pagina **Gruppi utenti**, fare clic su **Nuovo gruppo utenti**.

   ![Pulsante Nuovo gruppo utenti nella pagina Gruppi utenti](/help/implementing/cloud-manager/assets/ai-assistant-new-user-group.png)

1. Nella pagina **Crea un nuovo gruppo utenti**, fornisci le seguenti informazioni:

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

1. Nella pagina **`Add users to this user group`** cercare e selezionare gli utenti che devono accedere all&#39;Assistente di AEM AI.

   ![Aggiungi utenti a questa pagina gruppo utenti](/help/implementing/cloud-manager/assets/ai-assistant-add-users-to-this-group.png)

1. Nell&#39;angolo inferiore destro della pagina fare clic su **Salva**.
1. Ora, assegna il profilo di prodotto al gruppo di utenti&rbrack;(#assign-product-profile).

>[!TAB Aggiungere utenti in blocco]

Puoi utilizzare la funzione di caricamento in blocco in Admin Console.

1. Prepara un file CSV con le informazioni utente.
1. Utilizza l&#39;opzione **`Add users by CSV`** per un&#39;aggiunta in blocco efficiente.
1. Ora, assegna il profilo di prodotto al gruppo di utenti&rbrack;(#assign-product-profile).

>[!ENDTABS]


## 5 - Assegnare il profilo di prodotto al gruppo di utenti{#assign-product-profile}

Questo passaggio segue il flusso di lavoro standard di Adobe Admin Console per l’assegnazione di profili di prodotto ai gruppi di utenti.

Articolo di riferimento: [Gestire i profili di prodotto per gli utenti aziendali](https://helpx.adobe.com/it/enterprise/using/manage-product-profiles.html)

1. Mentre sei ancora nel gruppo di utenti di AEM AI Assistant da [4 - Aggiungi utenti al gruppo di utenti](#add-users), fai clic sulla scheda **Profili di prodotto assegnati**.
1. Fare clic su **Assegna profilo**.

   ![Pagina gruppo utenti Assistente di AEM AI con scheda Profili di prodotto assegnati selezionata](/help/implementing/cloud-manager/assets/ai-assistant-assign-profile.png)

1. Nella pagina **Assegna prodotti e profili**, nella finestra di dialogo **Seleziona profili di prodotto**, cerca e seleziona il profilo di prodotto **Assistente AI**.

   ![Pagina &quot;Assegna prodotti e profili&quot;, con la finestra di dialogo &quot;Seleziona profili di prodotto&quot; e il profilo di prodotto &quot;Assistente AI&quot; selezionato](/help/implementing/cloud-manager/assets/ai-assistant-select-product-profile.png)

1. Fai clic su **Applica** nell&#39;angolo inferiore destro della finestra di dialogo.
1. Fai clic su **Salva** nell&#39;angolo inferiore destro della pagina **Assegna prodotti e profili**.

   ![Il profilo di prodotto dell&#39;Assistente IA visualizzato è assegnato al gruppo di utenti dell&#39;Assistente IA di AEM](/help/implementing/cloud-manager/assets/ai-assistant-profile-assigned-to-user-group.png)


## Verifica la configurazione

* Verifica che il tuo profilo di prodotto mostri il numero corretto di gruppi di utenti assegnati.
* Verifica che il gruppo di utenti mostri il numero corretto di utenti.
* Conferma che l’autorizzazione Knowledge base del prodotto di AI Assistant sia abilitata e configurata correttamente.


## Verifica la configurazione

Chiedi a un utente del gruppo assegnato di effettuare le seguenti operazioni:

1. Accedi ad AEM.
2. Verifica che le funzioni dell’Assistente AI siano accessibili.
3. Verifica la funzionalità dell’Assistente AI per assicurarne la corretta attivazione.

## Consulta anche

* [Controllo dell&#39;accesso a Adobe Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview)
* [Autorizzazioni personalizzate di Cloud Manager](/help/implementing/cloud-manager/custom-permissions.md)


