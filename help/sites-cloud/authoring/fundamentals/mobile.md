---
title: Authoring di una pagina per dispositivi mobili
description: Quando si effettua l'authoring per i dispositivi mobili, è possibile alternare tra diversi emulatori per capire che cosa vede l'utente finale
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Authoring di una pagina per dispositivi mobili {#authoring-a-page-for-mobile-devices}

Le pagine di Adobe Experience Manager si basano su un layout reattivo. Il layout reattivo adatta automaticamente i contenuti al dispositivo di destinazione, eliminando la necessità di creare contenuti per dispositivi specifici.

Quando crei una pagina mobile, questa viene visualizzata in modo da emulare il dispositivo mobile. Quando crei la pagina, puoi scegliere tra diversi emulatori per verificare come la pagina verrà effettivamente vista dal visitatore.

I dispositivi sono raggruppati nelle categorie feature, smart e touch, a seconda delle funzionalità dei dispositivi di riprodurre una pagina. Quando l’utente accede a una pagina mobile, AEM rileva il dispositivo e invia la rappresentazione che corrisponde al gruppo di dispositivi a cui appartiene.

>[!NOTE]
>
>Per creare un sito mobile basato su un sito standard esistente, crea una Live Copy del sito standard. Consultate Creazione di una Live Copy per diversi canali.
>
>Gli sviluppatori AEM possono creare nuovi gruppi di dispositivi. Consultate Creazione di filtri per gruppi di dispositivi.
<!--
>To create a mobile site based on an existing standard site, create a live copy of the standard site. (See [Creating a Live Copy for Different Channels](/help/sites-administering/msm-livecopy.md).)
>
>AEM developers can create new device groups. (See [Creating Device Group Filters](/help/sites-developing/groupfilters.md).)
-->

Segui la procedura seguente per creare una pagina mobile:

1. From global navigation open the **Sites** console.
1. Modificare una pagina di contenuto.
1. Switch to the desired emulator by clicking the **Emulator** icon at the top of the page.

   ![Icona emulatore](/help/sites-cloud/authoring/assets/emulator.png)

1. Trascinate i componenti dal browser Componenti o dal browser Risorse sulla pagina.
1. [Modifica il layout](/help/sites-cloud/authoring/features/responsive-layout.md) reattivo della pagina e dei relativi componenti in base al dispositivo selezionato.

La pagina avrà un aspetto simile al seguente:

![Esempio mobile](/help/sites-cloud/authoring/assets/mobile.png)

>[!NOTE]
>
>Gli emulatori vengono disattivati quando una pagina nell’istanza di authoring viene richiesta da un dispositivo mobile.
