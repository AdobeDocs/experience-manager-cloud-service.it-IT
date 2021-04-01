---
title: Ruoli utente e autorizzazioni
description: Questa pagina descrive i ruoli utente e le autorizzazioni. Segui questa pagina per scoprire come aggiungere utenti e assegnarli ai ruoli di Cloud Manager.
translation-type: tm+mt
source-git-commit: b48be794da0b91722fb45ccefbe83e2b0b22d2a9
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 8%

---


# Ruoli di Cloud Manager {#user-roles-permissions}

## Ruoli utente {#user-roles}

Molte funzioni di Cloud Manager richiedono autorizzazioni specifiche per funzionare e limitano le azioni eseguite all’interno dell’interfaccia utente in base ai ruoli e alle autorizzazioni assegnate. In alcuni casi, se non si dispone dell&#39;autorizzazione per eseguire un&#39;azione, il controllo dell&#39;interfaccia è presente ma è disabilitato.

Se desideri eseguire un&#39;azione, ma non puoi, controlla la sezione seguente, [Ruoli utente e autorizzazioni](#permissions). A seconda dell&#39;obiettivo, è possibile contattare l&#39;amministratore di sistema e richiedere il ruolo necessario.

Cloud Manager definisce attualmente quattro ruoli per gli utenti che determinano la disponibilità di funzionalità specifiche:

* Business Owner (Proprietario)
* Deployment Manager (Responsabile implementazione)
* Program Manager (Responsabile programma)
* Developer (Sviluppatore)

>[!NOTE]
>La persona sviluppatore in Admin Console non è correlata al ruolo Sviluppatore in [!UICONTROL Cloud Manager].

## Visualizzazione dei ruoli {#view-roles}

Per visualizzare il tuo ruolo in Cloud Manager, accedi all’interfaccia utente di Cloud Manager, seleziona l’icona del tuo profilo nell’angolo in alto a destra e seleziona **Ruoli utente**, come illustrato nella figura seguente.

>[!NOTE]
>Per ulteriori informazioni sull’accesso a Cloud Manager, consulta [Passa a Cloud Manager](/help/onboarding/what-is-required/navigate-to-cloud-manager.md) .

![](/help/onboarding/what-is-required/assets/admin-console-9.png)

### Profilo del prodotto di integrazione {#integration-product-profile}

Oltre a quanto sopra, Cloud Manager creerà automaticamente un profilo di prodotto denominato &quot;Integrazioni - Cloud Service&quot;. Questo profilo di prodotto viene utilizzato per le integrazioni tra Adobe Experience Manager e altri prodotti Adobe. Questo profilo di prodotto **non deve essere eliminato**. Se elimini accidentalmente questo profilo, dovrà essere ricreato manualmente. Il nome visualizzato per questo profilo **deve essere** `CM_CS_DEFAULT`.


## Ruoli utente e autorizzazioni {#permissions}

[!UICONTROL Cloud Manager dispone di ruoli preconfigurati con le autorizzazioni appropriate. ] Ad esempio, uno sviluppatore sviluppa il codice e dispone dell’autorizzazione per inviare il codice all’archivio Git. In alternativa, un proprietario aziendale dispone di autorizzazioni diverse che consentono di aggiungere e modificare programmi, aggiungere ambienti e approvare distribuzioni.

A ciascuno dei ruoli sono associate autorizzazioni specifiche. Ad esempio, se ti trovi nel ruolo di un:

* ***Proprietario business***, disponi dell’autorizzazione per aggiungere un nuovo programma o modificare un programma, aggiungere o aggiornare un ambiente, aggiungere/modificare/eliminare la pipeline ed eseguire qualsiasi pipeline e distribuire il codice per AEM ambiente o qualità del codice.

* ***Deployment Manager***, è disponibile l’autorizzazione per aggiungere o aggiornare un ambiente, eseguire una pipeline e distribuire il codice per AEM ambiente o qualità del codice.

* ***Sviluppatore***, disponi dell’autorizzazione per generare Token di accesso personale per accedere a Git.

   >[!NOTE]
   > Un utente può essere assegnato a più ruoli. Ad esempio, l&#39;assegnazione di ruoli Business Owner (Proprietario business) e Deployment Manager a un utente fornisce loro la combinazione o la somma di queste autorizzazioni.


La tabella seguente riepiloga i ruoli e le relative autorizzazioni associate in Cloud Manager.

| Autorizzazione | Descrizione | Business Owner (Proprietario) | Deployment Manager (Responsabile implementazione) | Program Manager (Responsabile programma) | Developer (Sviluppatore) |
|--- |--- |--- |--- |--- |--- |
| Aggiungi programma<br>Modifica programma | Aggiungi un nuovo programma.<br>Modificare un programma - Aggiungere o rimuovere soluzioni o componenti aggiuntivi | x |  |  |  |
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

