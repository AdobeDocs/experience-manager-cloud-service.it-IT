---
title: Organizzare le risorse digitali
description: Organizza le risorse digitali utilizzando i vari metodi disponibili in Risorse Adobe Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9c5dd93be316417014fc665cc813a0d83c3fac6f
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---


# Organizzare risorse digitali {#organize-digital-assets}

Tutte le risorse digitali, i metadati e il contenuto di documenti Microsoft Office e PDF vengono estratti e resi ricercabili. La ricerca consente un filtraggio sofisticato delle risorse e rispetta pienamente le autorizzazioni corrette. I metadati sono descritti dettagliatamente in Metadati in Digital Asset Management.

 AEM Assets supporta diversi metodi per organizzare i contenuti. È possibile organizzarle in modo gerarchico utilizzando le cartelle oppure in modo non ordinato e ad hoc, utilizzando ad esempio i tag . Gli utenti possono modificare i tag nell’Editor risorse DAM in cui vengono visualizzate le risorse secondarie, le rappresentazioni e i metadati.

## Creare cartelle {#create-folders}

Quando organizzate una raccolta di risorse, ad esempio tutte le immagini *Natura*, potete creare delle cartelle per mantenerle unite. Potete usare le cartelle per classificare e organizzare le risorse.  AEM Assets non richiede l’organizzazione di risorse in cartelle per migliorare il funzionamento.

>[!NOTE]
>
>La condivisione di una cartella di risorse (in Marketing Cloud) del tipo `sling:OrderedFolder` non è supportata. Se desiderate condividere una cartella, non selezionate Ordinato al momento della creazione di una cartella.

1. Andate alla posizione nella cartella delle risorse digitali in cui desiderate creare una nuova cartella.
1. Scegliere **[!UICONTROL Crea]** dal menu. Selezionare **[!UICONTROL Nuova cartella]**.
1. Nel campo **[!UICONTROL Titolo]**, specificare un nome di cartella. Per impostazione predefinita, DAM utilizza il titolo fornito come nome della cartella. Una volta creata la cartella, potete ignorare l’impostazione predefinita e specificare un altro nome di cartella.
1. Fai clic su **[!UICONTROL Crea]**. La cartella viene visualizzata nella cartella delle risorse digitali.

## Aggiungere proprietà CUG alle cartelle {#add-cug-properties-to-folders}

Potete limitare gli utenti che possono accedere a determinate cartelle in Risorse rendendo la cartella parte di un gruppo di utenti chiuso (CUG). Per inserire una cartella in un gruppo di utenti chiuso:

1. In Risorse, fai clic con il pulsante destro del mouse sulla cartella per la quale vuoi aggiungere le proprietà del gruppo di utenti chiuso e seleziona **Proprietà**.
1. Fare clic sulla scheda **CUG**.
1. Selezionate la casella di controllo **Enabled** per rendere la cartella e le relative risorse disponibili solo per un gruppo di utenti chiuso.
1. Per aggiungere tali informazioni, andate alla pagina di accesso, se disponibile. Aggiungete i gruppi ammessi facendo clic su **Aggiungi elemento**. Se necessario, aggiungere l&#39;area di autenticazione. Fate clic su **OK** per salvare le modifiche.

## Utilizzare i tag per organizzare le risorse {#use-tags-to-organize-assets}

Potete usare cartelle o tag o entrambi per organizzare le risorse. L’aggiunta di tag alle risorse semplifica il recupero durante una ricerca. Per aggiungere tag a una risorsa, effettuate le seguenti operazioni:

1. In Digital Asset Manager, fate doppio clic sulla risorsa per aprirla.
1. Nell&#39;area **Tag**, aprire il menu per visualizzare i tag disponibili. Selezionate i tag desiderati. Per eliminare un tag, posizionate il puntatore sul tag e fate clic su `X` per eliminarlo.
1. Fare clic su **Salva** per salvare i tag aggiunti.
