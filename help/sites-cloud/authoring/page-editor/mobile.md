---
title: Authoring di una pagina per dispositivi mobili
description: Quando si effettua l’authoring per i dispositivi mobili, è possibile alternare tra diversi emulatori per capire che cosa vedrà l’utente finale
exl-id: fabd4468-3304-402f-9522-342da3bbae94
source-git-commit: a868bf4d4acf4fbae7ccaf55b03319ba0617f9a4
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 100%

---

# Authoring di una pagina per dispositivi mobili  {#authoring-a-page-for-mobile-devices}

Le pagine di Adobe Experience Manager si basano su un layout dinamico, [che adatta automaticamente i contenuti al dispositivo di destinazione, eliminando la necessità di creare contenuti per dispositivi specifici.](/help/sites-cloud/authoring/page-editor/responsive-layout.md)

Quando si effettua l’authoring di una pagina mobile, questa viene visualizzata in modo da emulare il dispositivo mobile. Durante l’authoring della pagina, puoi passare da un emulatore all’altro per vedere cosa vedrà l’utente finale quando accede alla pagina.

I dispositivi sono raggruppati nelle categorie funzione, smart e touch in base alle funzionalità dei dispositivi per il rendering di una pagina. Quando l’utente finale accede a una pagina mobile, AEM rileva il dispositivo e invia la rappresentazione che corrisponde al suo gruppo di dispositivi.

>[!NOTE]
>
>Per creare un sito mobile basato su un sito standard esistente, crea una Live Copy del sito standard. Vedi [Creazione di Live Copy](/help/sites-cloud/administering/msm/creating-live-copies.md).
>
>Gli sviluppatori AEM possono creare nuovi gruppi di dispositivi. Consulta Creazione di filtri per i gruppi di dispositivi.

<!--
>AEM developers can create new device groups. (See [Creating Device Group Filters](/help/sites-developing/groupfilters.md).)
-->

Segui la procedura seguente per creare una pagina mobile:

1. Dalla navigazione globale apri la console **Sites**.
1. Modifica una pagina di contenuto.
1. Passa all’emulatore desiderato facendo clic sull’icona dell’**emulatore** in alto nella pagina.

   ![Icona dell’emulatore](/help/sites-cloud/authoring/assets/emulator.png)

1. Trascina i componenti nella pagina dal browser Componenti o dal browser Risorse.
1. [Modifica il layout dinamico](/help/sites-cloud/authoring/page-editor/responsive-layout.md) della pagina e dei relativi componenti in base al dispositivo selezionato.

La pagina avrà un aspetto simile al seguente:

![Esempio per dispositivo mobile](/help/sites-cloud/authoring/assets/mobile.png)

>[!NOTE]
>
>Gli emulatori vengono disattivati quando una pagina nell’istanza di authoring viene richiesta da un dispositivo mobile.
