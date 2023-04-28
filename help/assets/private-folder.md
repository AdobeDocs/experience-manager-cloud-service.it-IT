---
title: Cartelle private per condividere le risorse
description: Scopri come creare una cartella privata nel [!DNL Adobe Experience Manager Assets] e condividerlo con altri utenti e assegnare loro vari privilegi.
contentOwner: Vishabh Gupta
role: User
feature: Collaboration
exl-id: d48f6daf-af81-4024-bff2-e8bf6d683b0c
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 3%

---

# Cartella privata in [!DNL Adobe Experience Manager Assets] {#private-folder}

Puoi creare una cartella privata nel [!DNL Adobe Experience Manager Assets] interfaccia utente disponibile esclusivamente dall’utente. Puoi condividere questa cartella privata con altri utenti e assegnare loro vari privilegi. In base al livello di privilegio assegnato, gli utenti possono eseguire varie attività sulla cartella, ad esempio visualizzare le risorse all’interno della cartella o modificare le risorse.

>[!NOTE]
>
>La cartella privata ha almeno un membro con ruolo Proprietario.
>
>Per creare una cartella privata, è necessario `Read` e `Modify` autorizzazioni per la cartella principale in cui si crea una cartella privata. Se non sei un amministratore, queste autorizzazioni non sono abilitate per impostazione predefinita in `/content/dam`. In questo caso, prima di cercare di creare cartelle private, ottieni queste autorizzazioni per il tuo ID utente/gruppo.

## Creare e condividere una cartella privata  {#create-share-private-folder}

Per creare e condividere una cartella privata:

1. In [!DNL Assets] console, fai clic su **[!UICONTROL Crea]** dalla barra degli strumenti, quindi seleziona **[!UICONTROL Cartella]** dal menu.

   ![Crea cartella risorse](assets/create-folder.png)

1. In **[!UICONTROL Crea cartella]** immettere una finestra di dialogo `Title` e `Name` (facoltativo) per la cartella.

   Seleziona la **[!UICONTROL Privato]** e fai clic su **[!UICONTROL Crea]**.

   ![chlimage_1-413](assets/create-private-folder.png)

   Viene creata una cartella privata. Ora puoi [aggiungere risorse](add-assets.md#upload-assets) alla cartella e condividi la cartella con altri utenti o gruppi. La cartella non è visibile a nessun altro utente finché non la condividi e non assegni loro i privilegi.

1. Per condividere la cartella, selezionarla e fare clic su **[!UICONTROL Proprietà]** dalla barra degli strumenti.

1. In **[!UICONTROL Proprietà cartella]** , seleziona un utente o un gruppo dal **[!UICONTROL Aggiungi utente]** elenco, assegna un ruolo (`Viewer`, `Editor`oppure `Owner`) nella cartella privata e fai clic su **[!UICONTROL Aggiungi]**.

   ![assegna gruppo di utenti](assets/assign-permissions-private-folder.png)

   Puoi assegnare vari ruoli, ad esempio `Editor`, `Owner`oppure `Viewer` all’utente con cui condividi la cartella. Se assegni un `Owner` ruolo dell&#39;utente, l&#39;utente ha `Editor` privilegi sulla cartella. Inoltre, l’utente può condividere la cartella con altri utenti. Se assegni un `Editor` , l’utente può modificare le risorse nella cartella privata. Se assegni un ruolo di visualizzatore, l’utente può visualizzare solo le risorse presenti nella cartella privata.

   >[!NOTE]
   >
   >La cartella privata ha almeno un membro con `Owner` ruolo. Pertanto, l&#39;amministratore non può rimuovere tutti i membri proprietari da una cartella privata. Tuttavia, per rimuovere i proprietari esistenti (e l&#39;amministratore stesso) dalla cartella privata, l&#39;amministratore deve aggiungere un altro utente come proprietario.

1. Fai clic su **[!UICONTROL Salva e chiudi]**. A seconda del ruolo assegnato, all’utente viene assegnato un set di privilegi sulla cartella privata quando accede a [!DNL Assets].
1. Fai clic su **[!UICONTROL Ok]** per chiudere il messaggio di conferma.
1. L’utente con cui condividi la cartella riceve una notifica di condivisione nella propria interfaccia utente.

1. Fai clic su [!UICONTROL Notifiche] per aprire un elenco di notifiche.

   ![notifica](assets/notification-icon.png)

1. Fai clic sulla voce della cartella privata condivisa dall’amministratore per aprire la cartella.

## Eliminazione di cartelle private {#delete-private-folder}

Per eliminare una cartella, selezionala e seleziona [!UICONTROL Elimina] dal menu principale o utilizzando il tasto Backspace sulla tastiera.

![opzione elimina nel menu principale](assets/delete-option.png)

>[!CAUTION]
>
>Se si elimina una cartella privata da CRXDE Lite, i gruppi di utenti ridondanti vengono lasciati nell’archivio.

>[!NOTE]
>
>Se elimini una cartella utilizzando il metodo precedente dall&#39;interfaccia utente, vengono eliminati anche i gruppi di utenti associati.
>
>Tuttavia, i gruppi di utenti ridondanti, inutilizzati e generati automaticamente possono essere rimossi dall’archivio utilizzando `clean` metodo in JMX nell&#39;istanza di authoring (`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`).

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cercare risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco di metadati](metadata-import-export.md)
