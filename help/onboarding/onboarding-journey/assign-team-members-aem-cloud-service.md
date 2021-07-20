---
title: 'Assegnazione di membri del team a AEM come profili di prodotto del Cloud Service '
description: Segui questa pagina per scoprire come assegnare i membri del team a AEM come profili di prodotto del Cloud Service
hide: true
hidefromtoc: true
index: false
source-git-commit: b45d5824afee9e2d540ea7cb41b199b517f26b25
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 2%

---


# Assegnazione a AEM come profili di prodotto di Cloud Service {#assign-team-members-cloud-service}

## Obiettivo {#objective}

Questo documento aiuta a comprendere i passaggi che l’amministratore di sistema deve seguire per assegnare i membri del team a AEM come profili di prodotto di Cloud Service e perché è fondamentale per consentire agli autori AEM di iniziare il proprio percorso con AEM.

Dopo aver letto questa sezione devi:

* Scopri perché e come i membri del team vengono assegnati a AEM come profili di prodotto di Cloud Service
* Come aggiungere membri del team al profilo di prodotto AEM utente
* Come aggiungere membri del team al profilo di prodotto Amministratori AEM


## Introduzione {#introduction}

Per poter accedere a AEM come Cloud Service, gli utenti devono appartenere a uno dei due profili di prodotto, &quot;Utenti AEM&quot; o &quot;Amministratori AEM&quot;. Ai membri del team devono essere concesse le autorizzazioni per l’istanza AEM, in quanto le autorizzazioni per amministrare Cloud Manager non sono sufficienti. Per saperne di più.

>[!NOTE]
>Ogni utente assegnato a AEM profilo di prodotto utente dall’amministratore di sistema avrà accesso (in sola lettura) a Cloud Manager.

## Prerequisiti {#prerequisites}

* Comprendere AEM come profili di prodotto di Cloud Service
* Admin Console
* I profili di prodotto di Cloud Manager sono stati assegnati ai membri del team a seconda delle necessità e le risorse cloud sono state configurate
* Dettagli sul membro del team: L’amministratore di sistema deve disporre dei nomi e degli indirizzi e-mail e dei ruoli e delle responsabilità dei membri del team che avranno bisogno dell’accesso a AEM come Cloud Service. Ai fini dell’onboarding, è consigliabile aggiungere inizialmente utenti che parteciperanno alle attività immediate, come amministratori, sviluppatori e autori di contenuti. Puoi continuare il resto dell’onboarding senza aggiungere tutti gli utenti. Dopo aver completato l’onboarding, puoi scalare un numero maggiore di utenti in un secondo momento.


1. Accedi all’Admin Console
(Come prima)

1. Rivedi AEM come profili di prodotto del Cloud Service
Dall’Admin Console è possibile visualizzare l’elenco dei profili di Cloud Manager. Per effettuare ciò:

1. Dopo aver effettuato l’accesso a Adobe Admin Console, seleziona Adobe Experience Manager as a Cloud Service dalla scheda Prodotti e servizi :

1. Passa all’istanza (istanza autore dell’ambiente di sviluppo) e selezionala come illustrato di seguito.



   Ora potrai visualizzare l’elenco dei AEM come profili di prodotto di Cloud Service che dovranno essere assegnati a un utente in base al loro ruolo. Per ulteriori informazioni, consulta AEM come profilo di prodotto di Cloud Service.




## Aggiungi i membri del team a AEM profilo di prodotto utente o AEM amministratore {#add-team-members}

Per poter accedere all’istanza AEMaaCS, gli utenti devono appartenere a uno dei due profili di prodotto &quot;Utenti AEM&quot; o &quot;Amministratori AEM&quot;.

>[!NOTE]
>È necessario disporre delle autorizzazioni per l’istanza. Le autorizzazioni per amministrare Cloud Manager non saranno sufficienti. Per saperne di più.

I passaggi seguenti devono essere seguiti dall&#39;amministratore di sistema che è anche nel ruolo Proprietario business.

1. Da Cloud Manager, passa a Cloud Manager e seleziona il pulsante Gestisci accesso dal contesto dell’ambiente di interesse come mostrato di seguito:

1. Dopo aver fatto clic su Gestisci accesso, una nuova SCHEDA consente di passare all&#39;Admin Console da cui si dispone dell&#39;accesso all&#39;istanza di authoring dell&#39;ambiente. Seleziona &quot;Amministratori AEM&quot; o &quot;Utenti AEM&quot; in base alle autorizzazioni che devono essere assegnate a questa persona. Ulteriori informazioni su AEM come profili di prodotto di Cloud Service.

1. Seleziona Aggiungi utente come mostrato di seguito e invia i dettagli necessari per completare l&#39;aggiunta del membro del team:


1. Se si dispone delle informazioni dei membri del team che hanno bisogno di accedere, è necessario ripetere questi passaggi per tutti gli ambienti, inclusi Sviluppo, Stage e Produzione.

   L’utente aggiunto avrà ora accesso all’AEM come servizi di authoring di Cloud Service!


## Novità {#whats-next}

Gli utenti assegnati ai profili di prodotto AEMaaCS sono ora pronti per imparare ad accedere a Author e per acquisire familiarità con le pagine di authoring in AEM come Cloud Service. Per saperne di più.

## Risorse aggiuntive {#additional-resources}

Configurazione dell’accesso a AEM (Procedura dettagliata per i video)
Guida rapida all’authoring delle pagine
