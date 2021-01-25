---
title: Utilizzo dello strumento di mappatura utente
description: Utilizzo dello strumento di mappatura utente
translation-type: tm+mt
source-git-commit: 664c278494a5ac88362b994946060ab3baa846d8
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# Utilizzo dello strumento di mappatura utente {#user-mapping-tool}

## Panoramica {#overview}

Come parte del percorso di transizione da AEM come Cloud Service, è necessario spostare utenti e gruppi dal sistema AEM esistente a AEM come Cloud Service. Questo viene fatto dallo strumento di trasferimento dei contenuti.

Un cambiamento importante nell’AEM come Cloud Service è l’uso completamente integrato di  ID Adobe per accedere al livello di authoring.  Ciò richiede l’utilizzo di Adobe Admin Console per la gestione di utenti e gruppi di utenti. Le informazioni sul profilo utente sono centralizzate nel Adobe   Identity Management System (IMS) che fornisce il single sign-on in tutte  applicazioni cloud Adobe. Per ulteriori dettagli, vedere  Identity Management. A causa di questa modifica, gli utenti e i gruppi esistenti devono essere mappati sui loro ID IMS per evitare la duplicazione di utenti e gruppi nell’istanza di creazione del Cloud Service.

## Considerazioni importanti {#important-considerations}

Vi sono alcuni casi eccezionali da prendere in considerazione. Verranno registrati i seguenti casi specifici e l&#39;utente o il gruppo in questione non verrà mappato:

1. Se un utente non dispone di un indirizzo e-mail nel campo `profile/email` del proprio nodo jcr.

1. Se un&#39;e-mail specificata non viene trovata nel sistema IMS per l&#39;ID organizzazione utilizzato (o se l&#39;ID IMS non può essere recuperato per un altro motivo).

1. Se l&#39;utente è attualmente disattivato, verrà trattato come se non fosse disabilitato.  Sarà mappato e migrato come normale e rimarrà disabilitato nell&#39;istanza cloud.

## Utilizzo dello strumento di mappatura utenti {#using-user-mapping-tool}

Lo strumento di mappatura utenti utilizza un’API che consente di effettuare ricerche per gli utenti IMS tramite e-mail e di restituire i loro ID IMS. Questa API richiede che l&#39;utente crei un ID client per la propria organizzazione, un Segreto cliente e un Token di accesso/Portatore.

Per impostare questa impostazione, effettuate le seguenti operazioni:

1. Andate a [ Adobe Developer Console](https://console.adobe.io) utilizzando l&#39;Adobe ID .
1. Creazione di un nuovo progetto o apertura di un progetto esistente
1. Aggiunta di un&#39;API
1. Scegli API di gestione utente
1. Creare una credenziale JWT
1. Generare una coppia di chiavi o caricare una chiave pubblica (rsa non è buona)
1. Generare un token di accesso (o un token JWT o un token del portatore).
1. Salvate tutte queste informazioni (ID client, Segreto cliente, ID account tecnico, E-mail account tecnico, ID organizzazione, Token di accesso) in un luogo sicuro.