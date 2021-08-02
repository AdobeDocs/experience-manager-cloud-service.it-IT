---
title: Navigazione a Cloud Manager
description: Segui questa pagina per scoprire come passare alla pagina di destinazione di Cloud Manager
exl-id: 9cf25d1d-a351-4ea0-b2e9-1df6ca4915b7
source-git-commit: e7f8e7daa88c5bf8bb13c2a635fb84724f8bd7bb
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 6%

---

# Passa a Cloud Manager {#cloud-manager}

Cloud Manager è una parte importante del AEM come Cloud Service. Consente alle organizzazioni di gestire in modo autonomo gli Experienci Manager nel cloud. Include un framework di integrazione continua e distribuzione continua (CI/CD, Continuous Integration/Continuous Delivery) che consente ai team IT e ai partner dell’implementazione di accelerare la distribuzione di personalizzazioni o aggiornamenti senza compromettere prestazioni o sicurezza. Utilizzando l’interfaccia utente, puoi configurare e avviare la pipeline CI/CD.

Una volta che l’amministratore di sistema ti concede l’accesso a Cloud Manager, riceverai un’e-mail che ti porterà alla pagina Home di [Adobe Experience Cloud](https://experience.adobe.com).

>[!NOTE]
>Devi essere aggiunto come utente e deve essere assegnato almeno a un ruolo Cloud Manager (profilo prodotto in Admin Console) dall’amministratore di sistema.

1. Dal messaggio e-mail di benvenuto, fai clic su **Inizia**, come illustrato nella figura riportata di seguito.
   ![](/help/onboarding/what-is-required/assets/get-started-email.png)

   >[!NOTE]
   >In alternativa, puoi anche accedere direttamente alla pagina di accesso di Cloud Manager da [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/). A seconda dei ruoli assegnati in [!UICONTROL Cloud Manager] e dello stato dell&#39;applicazione, verranno visualizzate diverse schermate durante l&#39;utilizzo dell&#39;interfaccia utente [!UICONTROL Cloud Manager]. Per ulteriori informazioni, consulta la sezione seguente, [Pagina di destinazione di Cloud Manager](#cloud-manager-landing) .

1. Selezionare **Experience Manager**.
   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/landing-page1.png)

1. Fai clic su **Launch** dalla scheda Cloud Manager. Dopo aver effettuato l&#39;accesso a [!UICONTROL Cloud Manager], puoi utilizzare l&#39;interfaccia utente (interfaccia utente).
   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/landing-page2.png)


## Pagina di destinazione di Cloud Manager {#cloud-manager-landing}

Dopo l’accesso, verrai indirizzato alla pagina di destinazione di Cloud Manager.

>[!NOTE]
>A seconda dei ruoli assegnati in [!UICONTROL Cloud Manager] e dello stato dell&#39;applicazione, verranno visualizzate diverse schermate durante l&#39;utilizzo dell&#39;interfaccia utente [!UICONTROL Cloud Manager].

Verrà visualizzata una delle tre opzioni descritte di seguito:

* **In Cloud Manager non esiste alcun programma**

   Se nell’organizzazione non è presente alcun programma, la pagina di destinazione ti invita a creare il primo programma, come illustrato nella figura riportata di seguito.
   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

* **Quando in Cloud Manager sono già presenti programmi**

   Se nell’organizzazione sono già presenti programmi, nella pagina di destinazione viene indicato di aggiungere un altro programma e vengono visualizzati anche tutti i programmi esistenti, come illustrato nella figura riportata di seguito.

   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

* **Quando esiste un programma e l&#39;utente è amministratore di sistema**

   Se nell&#39;organizzazione sono già presenti programmi e si è amministratori di sistema, nella pagina di destinazione viene visualizzato il pulsante **Gestisci accesso** insieme all&#39;opzione **Aggiungi programma** , come illustrato nella figura riportata di seguito.

   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

Da qui, un utente con le autorizzazioni giuste, ad esempio un ruolo Proprietario business in Cloud Manager, è in grado di selezionare **Aggiungi programma** per avviare la [procedura guidata Aggiungi programma](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/production-programs/creating-production-program.html?lang=en#getting-access).

Per informazioni su come aggiungere un programma in Cloud Manager, consulta:

* Creazione di un programma di produzione
* Creazione di un programma sandbox