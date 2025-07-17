---
title: Introduzione ai moduli HTML5
description: HTML5 forms è una nuova funzionalità del software Adobe Experience Manager 6.0 (AEM 6.0) che può eseguire il rendering dei modelli di moduli XFA in formato HTML5.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 0facca18-ffa1-420c-859a-6f1f2c449d71
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# Introduzione ai moduli HTML5{#introduction-to-html-forms}

<span class="preview"> La funzionalità HTML5 Forms è disponibile come parte del programma di accesso anticipato. Per richiedere l’accesso, invia un’e-mail dal tuo ID e-mail ufficiale (di lavoro) a aem-forms-ea@adobe.com.
</span>

HTML5 forms è una nuova funzionalità del software Adobe Experience Manager 6.0 (AEM 6.0) che può eseguire il rendering dei modelli di moduli XFA in formato HTML5. Questa funzionalità consente il rendering dei moduli su dispositivi mobili e browser desktop su cui non è supportato il PDF basato su XFA. HTML5 Forms non solo supporta le funzionalità esistenti dei modelli di modulo XFA, ma aggiunge anche nuove funzionalità, ad esempio la firma scarabocchio, per i dispositivi mobili.

HTML5 forms genera documenti basati su costrutti standard di HTML5. È possibile visualizzare i moduli HTML5 in tutti i browser moderni che supportano HTML5. Non è necessario installare altri plug-in per browser. Per ulteriori informazioni sui browser supportati, vedere [Piattaforme client supportate](https://adobe.com/go/learn_aemforms_supportedplatforms_63).

![Anteprima modulo HTML5](assets/mobile_form_on_an_ipad_date_14.png)

## Funzionalità chiave dei moduli HTML5 {#key-capabilities-of-html-forms-br}

* Esegue il rendering dei moduli XFA esistenti in HTML5 supportati su tutti i browser compatibili.
* Sfrutta le funzionalità di progettazione dei moduli XFA standard per eseguire il targeting dei moduli per dispositivi mobili.
* Utilizza funzionalità XFA dinamiche in formato HTML5.
* Utilizza un layout di testo SVG (SVG 1.1) altamente preciso per corrispondere al layout di testo PDF.
* Fornisce supporto per JavaScript e FormCalc.
* Assembla dinamicamente i frammenti in moduli interattivi basati su eventi basati su dati o input dell’utente.
* Fornisce il supporto per CSS personalizzati in modo che corrispondano all&#39;aspetto dei moduli in base agli standard aziendali.
* Consente ai widget personalizzati di offrire un&#39;esperienza di acquisizione dati avanzata.
* Fornisce supporto per l’integrazione con le app web.

### Pubblicazione multicanale {#multichannel-publishing}

Gli sviluppatori di moduli possono utilizzare un modello XFA per eseguire il rendering dei moduli nei formati PDF e HTML5. Questa funzionalità è utile negli scenari in cui si dispone di un set elevato di moduli XFA che richiedono modifiche minime per adattarsi alle procedure di progettazione dei moduli HTML5. È possibile eseguire il rendering dei moduli XFA esistenti in HTML5 per eseguire il targeting di vari dispositivi in cui PDF basato su XFA non è ancora supportato.

## Gestire i moduli HTML5 {#manage-html-forms}

AEM fornisce anche una vista unificata per elencare e gestire tutti i modelli di modulo tramite l’interfaccia utente di AEM Forms. Puoi attivare, disattivare, pubblicare e visualizzare in anteprima i moduli. <!--For more information, see [Introduction to managing forms](../../forms/using/introduction-managing-forms.md).-->

### Personalizzazione di Forms {#forms-customization}

HTML5 Forms esegue il rendering dei modelli di modulo utilizzando costrutti HTML5 standard. Questo semplifica la personalizzazione e l’estensione dei moduli in formato HTML5 utilizzando tecnologie web, principalmente CSS e JavaScript. È possibile personalizzare facilmente l&#39;aspetto dei widget esistenti, creare widget personalizzati o utilizzare stili personalizzati nei moduli. Per ulteriori informazioni sulla creazione di widget personalizzati e sulla personalizzazione di widget esistenti, vedere [Collegare widget personalizzati con HTML5 forms](/help/forms/custom-widgets.md).
