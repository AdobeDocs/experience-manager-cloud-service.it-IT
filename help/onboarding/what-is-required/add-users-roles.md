---
title: Aggiunta di utenti e ruoli - Elementi richiesti
description: Aggiunta di utenti e ruoli - Elementi richiesti
translation-type: tm+mt
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247

---


# Aggiunta di utenti e ruoli - Elementi richiesti {#add-users-roles}


Molte funzionalità di [!UICONTROL Cloud Manager] richiedono autorizzazioni specifiche per funzionare. Ad esempio, solo alcuni utenti possono impostare i KPI (Key Performance Indicators) per un programma. Tali autorizzazioni sono logicamente raggruppate in ruoli.

[!UICONTROL Cloud Manager] definisce attualmente quattro ruoli per gli utenti che determinano la disponibilità di funzionalità specifiche:

* Proprietario
* Program Manager
* Gestione distribuzione
* Sviluppatore

>[!CAUTION]
>
>Per utilizzare [!UICONTROL Cloud Manager], è necessario disporre di un Adobe ID e del contesto prodotto dei servizi gestiti Adobe.

## Definizioni dei ruoli {#role-definitions}

>[!NOTE]
>
>La persona Sviluppatore in Admin Console non è correlata al ruolo Sviluppatore in [!UICONTROL Cloud Manager].

La tabella seguente riepiloga i ruoli:

| [!UICONTROL Ruoli di Cloud Manager] | Descrizione |
|--- |--- |
| Proprietario | Responsabile della definizione dei KPI, dell&#39;approvazione delle implementazioni di produzione e della risoluzione di importanti errori a 3 livelli. |
| Program Manager | Utilizza [!UICONTROL Cloud Manager] per eseguire la configurazione del team, verificare lo stato e visualizzare i KPI. Può approvare importanti fallimenti a 3 livelli. |
| Gestione distribuzione | Gestisce le operazioni di distribuzione. Utilizza [!UICONTROL Cloud Manager] per eseguire distribuzioni di fase/produzione. È possibile modificare le tubazioni CI/CD. Può approvare importanti fallimenti a 3 livelli. Può accedere al repository Git. |
| Sviluppatore | Sviluppa e verifica il codice applicazione personalizzato. Utilizza principalmente [!UICONTROL Cloud Manager] per visualizzare lo stato. Può accedere all’archivio Git per il commit del codice. |
| Content Author | Generalmente non interagisce con [!UICONTROL Cloud Manager]. Può utilizzare il commutatore di programmi [!UICONTROL Cloud Manager] (dopo aver navigato da [!UICONTROL Experience Cloud]) per accedere ad AEM. |

## Utilizzo di Admin Console per creare un profilo {#using-admin-console-to-create-a-profile}

I ruoli vengono gestiti per [!UICONTROL Cloud Manager] dall’Admin Console di Adobe. Iscrizioni di ruolo specifiche vengono fornite aggiungendo l&#39;utente a un profilo di prodotto [!UICONTROL Cloud Manager] in Admin Console.

Puoi assegnare iscrizioni di ruolo specifiche aggiungendo l’utente a un profilo [!UICONTROL di] prodotto **Cloud Manager** nell’Admin Console di Adobe, una posizione centrale per la gestione delle adesioni Adobe in tutta l’organizzazione. Per ulteriori informazioni su Adobe Admin Console, consulta la documentazione di [Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html).

>[!NOTE]
>
>Per accedere alla console di amministrazione e configurare il team (utenti e ruoli), aprite un browser e visitate [https://adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise).

Per fornire le autorizzazioni appropriate basate sul ruolo agli utenti di [!UICONTROL Cloud Manager] , un amministratore dell&#39; **organizzazione** del cliente deve creare nuovi profili di prodotto nel contesto di prodotto dei servizi [!UICONTROL gestiti] AEM.

Per concedere le autorizzazioni appropriate basate sul ruolo agli utenti di [!UICONTROL Cloud Manager] , in qualità di amministratore è necessario creare quattro nuovi profili di prodotto nel contesto di prodotto dei servizi [!UICONTROL gestiti] AEM, corrispondenti a ciascuno dei quattro ruoli di [!UICONTROL Cloud Manager] :

* Proprietario
* Gestione distribuzione
* Sviluppatore
* Program Manager

Puoi creare o aggiungere utenti/gruppi a questi profili di prodotto con [Admin Console](https://adminconsole.adobe.com/) per [!UICONTROL Cloud Manager], come illustrato nella figura seguente:

1. Accedi ad Admin Console e fai clic su **Nuovo profilo** per aggiungere un nuovo profilo.

1. Compila i campi per impostare un nuovo ruolo per [!UICONTROL Cloud Manager].

   Immettete Nome **** profilo e Nome **** visualizzato per creare un nuovo profilo. Inoltre, potete selezionare un gruppo **di** autorizzazioni per il profilo.

   Fate clic su **Fine** per completare il passaggio di creazione del profilo.

   >[!NOTE]
   >
   >Quando si creano questi profili di prodotto, il Nome **** visualizzato deve essere il valore tecnico definito da [!UICONTROL Cloud Manager] (vedi tabella di seguito). Il Nome **** profilo può essere qualsiasi cosa, anche se per evitare confusione si consiglia di utilizzare i valori nella colonna Nome *profilo* consigliato di seguito. A questo scopo, durante la creazione del profilo di prodotto, deselezionate **Come nome** profilo e specificate il valore corrispondente come nome **** visualizzato.

   | **Ruolo** | **Nome visualizzato (obbligatorio)** | **Nome profilo consigliato** |
   |---|---|---|
   | Proprietario | CM_BUSINESS_OWNER_ROLE_PROFILE | [!UICONTROL Cloud Manager] - Ruolo proprietario business |
   | Gestione distribuzione | CM_DEPLOYMENT_MANAGER_ROLE_PROFILE | [!UICONTROL Cloud Manager] - Ruolo Gestione distribuzione |
   | Sviluppatore | CM_DEVELOPER_ROLE_PROFILE | [!UICONTROL Cloud Manager] - Ruolo sviluppatore |
   | Program Manager | CM_PROGRAM_MANAGER_ROLE_PROFILE | [!UICONTROL Cloud Manager] - Ruolo di Program Manager |

1. Dopo aver creato il profilo di prodotto, puoi aggiungere utenti (o gruppi) a Profili di prodotto.


