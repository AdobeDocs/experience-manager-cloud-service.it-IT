---
title: Ruoli utente e autorizzazioni
description: Questa pagina descrive i ruoli utente e le autorizzazioni. Segui questa pagina per scoprire come aggiungere utenti e assegnarli ai ruoli di Cloud Manager.
translation-type: tm+mt
source-git-commit: f1f5766a41763634e0aaba44e55471ac2ea5dc8f
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 9%

---


# Ruoli utente e autorizzazioni {#user-roles-permissions}

Adobe creerà un identificatore **Organizzazione** per la società in Adobe Identity Management System (IMS), in cui è possibile gestire tutti gli utenti e le relative autorizzazioni. Ogni utente, che deve essere membro di questa organizzazione e avrà accesso a uno qualsiasi dei servizi [!UICONTROL Experience Cloud], dovrà disporre del proprio **[Adobe ID](/help/onboarding/what-is-required/get-your-adobe-id.md)**.

## Ruoli utente {#user-roles}

Molte funzionalità di Cloud Manager richiedono autorizzazioni specifiche per funzionare.

Molte funzioni di Cloud Manager richiedono autorizzazioni specifiche per funzionare e limitano le azioni eseguite all’interno dell’interfaccia utente in base ai ruoli e alle autorizzazioni assegnate. In alcuni casi, se non si dispone dell&#39;autorizzazione per eseguire un&#39;azione, il controllo dell&#39;interfaccia è presente ma è disabilitato.

Se desideri eseguire un&#39;azione, ma non puoi, controlla [le autorizzazioni associate alle definizioni dei ruoli](#permissions). A seconda dell&#39;obiettivo, è possibile contattare l&#39;amministratore di sistema e richiedere il ruolo necessario.

Cloud Manager definisce attualmente quattro ruoli per gli utenti che determinano la disponibilità di funzionalità specifiche:

* Business Owner (Proprietario)
* Deployment Manager (Responsabile implementazione)
* Program Manager (Responsabile programma)
* Developer (Sviluppatore)

>[!NOTE]
>La persona sviluppatore in Admin Console non è correlata al ruolo Sviluppatore in [!UICONTROL Cloud Manager].

## Definizioni dei ruoli {#role-definitions}

La tabella seguente riepiloga i ruoli:

| [!UICONTROL Ruoli ] di Cloud Manager | Descrizione |
|--- |--- |
| Business Owner (Proprietario) | Responsabile della definizione dei KPI, dell’approvazione delle implementazioni di produzione e dell’override di importanti errori a 3 livelli. |
| Program Manager (Responsabile programma) | Utilizza [!UICONTROL Cloud Manager] per eseguire la configurazione del team, esaminare lo stato e visualizzare i KPI. Può approvare importanti errori a 3 livelli. |
| Deployment Manager (Responsabile implementazione) | Gestisce le operazioni di distribuzione. Utilizza [!UICONTROL Cloud Manager] per eseguire distribuzioni di stage/produzione. È possibile modificare le pipeline CI/CD. Può approvare importanti errori a 3 livelli. È possibile accedere all’archivio Git. |
| Developer (Sviluppatore) | Sviluppa e verifica il codice personalizzato dell’applicazione. Utilizza principalmente [!UICONTROL Cloud Manager] per visualizzare lo stato. Può accedere all’archivio Git per il commit del codice. |
| Autore del contenuto | In genere non interagisce con [!UICONTROL Cloud Manager]. Per accedere a AEM può essere utilizzato il commutatore di programma [!UICONTROL Cloud Manager] (dopo aver navigato da [!UICONTROL Experience Cloud]). |

### Visualizzazione dei ruoli {#view-roles}

Per visualizzare il tuo ruolo in Cloud Manager, accedi all’interfaccia utente di Cloud Manager, seleziona l’icona del tuo profilo nell’angolo in alto a destra e seleziona **Ruoli utente**, come illustrato nella figura seguente.

![](/help/onboarding/what-is-required/assets/admin-console-9.png)

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