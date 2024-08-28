---
title: Come modificare il contenuto di Page Zero in Designer?
description: Modifica il messaggio visualizzato nella pagina Zero di un PDF XFA per i visualizzatori non Adobe PDF.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
feature: Adaptive Forms
role: User
source-git-commit: 937bd4653e454beea3111cfc7ef7b4bbc1ace193
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# Modifica del contenuto di Page Zero in Designer {#changing-page-zero-content-in-designer}

Il contenuto Pagina zero viene visualizzato per impostazione predefinita quando un visualizzatore non Adobe PDF, ad esempio il visualizzatore PDF predefinito in [!DNL Chrome] o [!DNL Firefox], non è in grado di leggere il contenuto del modulo PDF/XFA. Di seguito viene visualizzato il messaggio predefinito Pagina zero.

![defaultpage0message](assets/defaultpage0message.png)

La versione [!DNL AEM Forms] di Designer consente di modificare il messaggio visualizzato a pagina zero. Per modificare il messaggio Pagina zero, effettuare le seguenti operazioni:

1. Verificare che sia installata la versione [!DNL AEM Forms] di Designer. Puoi controllare la versione dalla schermata Informazioni su di Designer.

1. Aprire il modulo di cui si desidera modificare il contenuto Pagina zero.

1. Fare clic su **[!UICONTROL File]** > **[!UICONTROL Proprietà modulo]**.

1. Nella finestra di dialogo [!UICONTROL Proprietà modulo], fai clic su ![più](assets/plus.png) (icona Più) per aggiungere una proprietà personalizzata.

1. Specificare **_pagezerocontent** come nome della proprietà.
1. Aggiungi come valore il nuovo messaggio Pagina zero, in formato Testo formattato. Ad esempio:


   `<body xmlns="https://www.w3.org/1999/xhtml" xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/reader_download.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/acrreader.</p></body>`

1. Salvare il modulo come PDF.

1. Visualizza il modulo PDF nel browser per confermare che il messaggio è stato aggiornato. Il valore di esempio riportato sopra viene visualizzato come segue:

   ![changedmessage](assets/changedmessage.png)

>[!NOTE]
>
>La proprietà personalizzata creata potrebbe non essere visualizzata correttamente nella finestra di dialogo Proprietà modulo quando si riapre il modulo. Tuttavia, funziona correttamente e nel modulo viene visualizzato il messaggio Pagina zero aggiornato.

>[!MORELIKETHIS]
>
>* [Scarica e installa Forms Designer per creare modelli per documenti di record](/help/forms/installing-configuring-designer.md)
>* [Utilizzare Forms Designer per creare modelli di documenti di record (DoR) e frammenti di moduli?](/help/forms/use-forms-designer.md)
