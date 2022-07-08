---
title: Authoring di una pagina per dispositivi mobili
description: Quando si effettua l’authoring per i dispositivi mobili, è possibile alternare tra diversi emulatori per capire che cosa vedrà l’utente finale
exl-id: fabd4468-3304-402f-9522-342da3bbae94
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '267'
ht-degree: 100%

---

# Authoring di una pagina per dispositivi mobili  {#authoring-a-page-for-mobile-devices}

Le pagine di Adobe Experience Manager si basano su un layout dinamico, [che adatta automaticamente i contenuti al dispositivo di destinazione, eliminando la necessità di creare contenuti per dispositivi specifici.](/help/sites-cloud/authoring/features/responsive-layout.md)

Quando crei una pagina mobile, questa viene visualizzata in modo da emulare il dispositivo mobile. Quando crei la pagina, puoi scegliere tra diversi emulatori per verificare come la pagina verrà effettivamente vista dal visitatore.

I dispositivi sono raggruppati nelle categorie feature, smart e touch, a seconda delle funzionalità dei dispositivi di riprodurre una pagina. Quando l’utente accede a una pagina mobile, AEM rileva il dispositivo e invia la rappresentazione che corrisponde al gruppo di dispositivi a cui appartiene.

>[!NOTE]
>
>Per creare un sito mobile basato su un sito standard esistente, crea una Live Copy del sito standard. Vedi [Creazione di Live Copy.](/help/sites-cloud/administering/msm/creating-live-copies.md)
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
1. [Modifica il layout dinamico](/help/sites-cloud/authoring/features/responsive-layout.md) della pagina e dei relativi componenti in base al dispositivo selezionato.

La pagina avrà un aspetto simile al seguente:

![Esempio per dispositivo mobile](/help/sites-cloud/authoring/assets/mobile.png)

>[!NOTE]
>
>Gli emulatori vengono disattivati quando una pagina nell’istanza di authoring viene richiesta da un dispositivo mobile.
