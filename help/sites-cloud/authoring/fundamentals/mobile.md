---
title: Authoring di una pagina per dispositivi mobili
description: Quando si effettua l’authoring per i dispositivi mobili, è possibile alternare tra diversi emulatori per capire che cosa vedrà l’utente finale
translation-type: tm+mt
source-git-commit: dbd7b8084445b03beff3b5a96b0fa6b5512e10b8
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 100%

---


# Authoring di una pagina per dispositivi mobili  {#authoring-a-page-for-mobile-devices}

Le pagine di Adobe Experience Manager si basano su un layout dinamico, che adatta automaticamente i contenuti al dispositivo di destinazione, eliminando la necessità di creare contenuti per dispositivi specifici.

Quando crei una pagina mobile, questa viene visualizzata in modo da emulare il dispositivo mobile. Quando crei la pagina, puoi scegliere tra diversi emulatori per verificare come la pagina verrà effettivamente vista dal visitatore.

I dispositivi sono raggruppati nelle categorie feature, smart e touch, a seconda delle funzionalità dei dispositivi di riprodurre una pagina. Quando l’utente accede a una pagina mobile, AEM rileva il dispositivo e invia la rappresentazione che corrisponde al gruppo di dispositivi a cui appartiene.

>[!NOTE]
>
>Per creare un sito mobile basato su un sito standard esistente, crea una Live Copy del sito standard. Consulta Creazione di una Live Copy per canali diversi.
>
>Gli sviluppatori AEM possono creare nuovi gruppi di dispositivi. Consulta Creazione di filtri per i gruppi di dispositivi.

<!--
>To create a mobile site based on an existing standard site, create a live copy of the standard site. (See [Creating a Live Copy for Different Channels](/help/sites-administering/msm-livecopy.md).)
>
>AEM developers can create new device groups. (See [Creating Device Group Filters](/help/sites-developing/groupfilters.md).)
-->

Segui la procedura seguente per creare una pagina mobile:

1. Dalla navigazione globale apri la console **Sites**.
1. Modifica una pagina di contenuto.
1. Passa all’emulatore desiderato facendo clic sull’icona dell’**emulatore** in alto nella pagina.

   ![Icona dell’emulatore](/help/sites-cloud/authoring/assets/emulator.png)

1. Trascina i componenti nella pagina dal browser Componenti o dal browser Risorse.
1. [Modifica il layout dinamico](/help/sites-cloud/authoring/features/responsive-layout.md) della pagina e dei relativi componenti in base al dispositivo selezionato.

La pagina avrà un aspetto simile al seguente:

![Esempio per dispositivo mobile](/help/sites-cloud/authoring/assets/mobile.png)

>[!NOTE]
>
>Gli emulatori vengono disattivati quando una pagina nell’istanza di authoring viene richiesta da un dispositivo mobile.
