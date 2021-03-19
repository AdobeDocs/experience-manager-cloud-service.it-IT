---
title: Organizzare le risorse digitali
description: Organizza le risorse digitali utilizzando vari metodi disponibili in Risorse Adobe Experience Manager.
contentOwner: AG
feature: Gestione risorse
topic: '"Amministratore, Business Practitioner"'
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---


# Organizzare le risorse digitali {#organize-digital-assets}

Tutte le risorse digitali, i metadati e il contenuto di Microsoft Office e i documenti PDF vengono estratti e resi ricercabili. La ricerca consente un filtraggio sofisticato delle risorse e rispetta completamente le autorizzazioni appropriate. I metadati sono descritti in dettaglio in Metadata in Digital Asset Management.

AEM Assets supporta diversi modi per organizzare i contenuti. È possibile organizzarle in modo gerarchico utilizzando le cartelle oppure in modo non ordinato e ad hoc, utilizzando ad esempio i tag. Gli utenti possono modificare i tag nell’editor risorse DAM in cui vengono visualizzate risorse secondarie, rappresentazioni e metadati.

## Crea cartelle {#create-folders}

Quando organizzi una raccolta di risorse, ad esempio tutte le immagini *Natura*, puoi creare cartelle per mantenerle intatte. Puoi utilizzare le cartelle per suddividere in categorie e organizzare le risorse. AEM Assets non richiede di organizzare le risorse nelle cartelle per funzionare meglio.

>[!NOTE]
>
>La condivisione di una cartella di risorse (in Marketing Cloud) del tipo `sling:OrderedFolder` non è supportata. Per condividere una cartella, non selezionare Ordinato durante la creazione di una cartella.

1. Passa alla posizione nella cartella delle risorse digitali in cui desideri creare una nuova cartella.
1. Nel menu, fai clic su **[!UICONTROL Crea]**. Selezionare **[!UICONTROL Nuova cartella]**.
1. Nel campo **[!UICONTROL Titolo]** , specifica il nome di una cartella. Per impostazione predefinita, DAM utilizza il titolo fornito come nome della cartella. Una volta creata la cartella, è possibile sostituire l’impostazione predefinita e specificare un altro nome di cartella.
1. Fai clic su **[!UICONTROL Crea]**. La cartella viene visualizzata nella cartella delle risorse digitali.

## Aggiungi proprietà CUG alle cartelle {#add-cug-properties-to-folders}

È possibile limitare gli utenti che possono accedere a determinate cartelle in Assets rendendo la cartella parte di un gruppo di utenti chiuso (CUG). Per rendere una cartella parte di un CUG:

1. In Assets, fai clic con il pulsante destro del mouse sulla cartella per la quale desideri aggiungere proprietà di gruppo utenti chiuso e seleziona **Proprietà**.
1. Fare clic sulla scheda **CUG**.
1. Seleziona la casella di controllo **Enabled** per rendere la cartella e le relative risorse disponibili solo per un gruppo di utenti chiuso.
1. Per aggiungere tali informazioni, vai alla pagina di accesso, se disponibile. Aggiungi i gruppi ammessi facendo clic su **Aggiungi elemento**. Se necessario, aggiungere il realm. Fate clic su **OK** per salvare le modifiche.

## Utilizzare i tag per organizzare le risorse {#use-tags-to-organize-assets}

Puoi utilizzare cartelle o tag o entrambi per organizzare le risorse. L’aggiunta di tag alle risorse semplifica il recupero durante una ricerca. Per aggiungere tag a una risorsa, effettua le seguenti operazioni:

1. In Digital Asset Manager, fai doppio clic sulla risorsa per aprirla.
1. Nell’area **Tag**, apri il menu per visualizzare i tag disponibili. Seleziona i tag desiderati. Per eliminare un tag, posiziona il puntatore del mouse sul tag e fai clic su `X` per eliminarlo.
1. Fai clic su **Salva** per salvare i tag aggiunti.
