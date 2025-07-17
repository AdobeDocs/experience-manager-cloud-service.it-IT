---
title: Guida introduttiva ai moduli di HTML5
description: Per iniziare, distribuisci il pacchetto del componente aggiuntivo AEM Forms e importa i moduli HTML5 esistenti in AEM.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f276d150-8936-4bfb-8475-7ca36815b233
feature: HTML5 Forms,Mobile Forms
exl-id: a3245f05-6ea3-4f90-8981-bfa89d2e7335
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Guida introduttiva ai moduli di HTML5 {#getting-started-with-html-forms}

<span class="preview"> La funzionalità HTML5 Forms è disponibile come parte del programma di accesso anticipato. Per richiedere l’accesso, invia un’e-mail dal tuo ID e-mail ufficiale (di lavoro) a aem-forms-ea@adobe.com.
</span>

I moduli HTML5 offrono numerose funzionalità pronte per l&#39;uso su dispositivi mobili. Consente di espandere le soluzioni e i flussi di lavoro correnti a tablet o smartphone con browser HTML5. Alcune delle funzionalità includono:

* **Rendering basato su HTML5 dei modelli di modulo XFA:** Oltre al normale PDF forms, ora è possibile eseguire il rendering dei moduli basati su XFA esistenti in formato HTML5. Consente di espandere la piattaforma client ai dispositivi mobili (Apple iPad, tablet Android, smartphone e così via) che supportano HTML5 e non supportano Adobe Reader con XFA Forms. Per ulteriori informazioni sulla funzionalità di rendering basata su HTML5, vedere [Introduzione ai moduli HTML5](/help/forms/introductionhtml5.md).

* **Gestione di Forms:** Inoltre, AEM include nuove funzionalità per semplificare il processo di organizzazione e gestione dei moduli. È possibile attivare, disattivare, pubblicare e visualizzare in anteprima i moduli.<!--For more information, see [Introduction to managing forms](/help/forms/using/introduction-managing-forms.md).-->

## Configurazione dell’ambiente per i moduli HTML5 {#installing-html-forms}

Per abilitare l&#39;invio di moduli e il rendering corretto di HTML5 Forms, effettuare le seguenti operazioni:

* **Aggiungi filtri dispatcher:** Aggiorna il file `src/conf.dispatcher.d/filters/filters.any` per consentire le richieste necessarie per HTML5 Forms. Aggiungi le seguenti regole filtro:

  ```
  /0103 { /type "allow" /method '(HEAD|POST)' /url "/content/xfaforms/profiles/default.submit.html" }  # allow POSTs to form selectors under content
  /0104 { /type "allow" /method '(GET|HEAD|POST)' /url "/*.xdp.html" }
  ```

* **Aggiungi un pacchetto per l&#39;invio:** Nel progetto, aggiungi un pacchetto nella cartella `src/main/content/jcr_root/content` per supportare la funzionalità di invio del modulo.

* **Importa HTML5 Forms:** Importa i moduli dal file system locale in AEM Forms.
