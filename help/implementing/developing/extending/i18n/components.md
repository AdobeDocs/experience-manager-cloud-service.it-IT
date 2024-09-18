---
title: Internazionalizzazione dei componenti
description: Internazionalizza i componenti e le finestre di dialogo in modo che le loro stringhe di interfaccia possano essere presentate in diverse lingue
topic-tags: components
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: b55f7260628f759de2718290624cdc82da7a2961
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Internazionalizzazione dei componenti{#internationalizing-components}

Internazionalizza i componenti e le finestre di dialogo in modo che le relative stringhe dell’interfaccia utente possano essere presentate in lingue diverse. I componenti progettati per l’internazionalizzazione consentono di esternalizzare, tradurre e importare le stringhe dell’interfaccia utente nell’archivio. In fase di esecuzione, le preferenze della lingua dell’utente o le impostazioni locali della pagina determinano quale lingua viene visualizzata nell’interfaccia utente.

![i18n-components-1.png](/help/implementing/developing/extending/assets/i18n-comp1.png)

Utilizza il seguente processo per internazionalizzare i componenti e fornire l’interfaccia utente in diverse lingue:

1. [Implementare i componenti utilizzando codice che internazionalizza le stringhe.](/help/implementing/developing/extending/i18n/dev.md) Il codice identifica le stringhe da tradurre e seleziona la lingua da presentare in fase di esecuzione.
1. Crea dizionari e aggiungi le stringhe in inglese da tradurre.
1. Esporta il dizionario in formato XLIFF, traduci le stringhe, quindi importa nuovamente i file XLIFF in AEM.
1. Incorpora il dizionario nel processo di gestione del rilascio dell’applicazione.

>[!NOTE]
>
>I metodi qui descritti per l’internazionalizzazione dei componenti sono destinati alla traduzione di stringhe statiche. Quando ci si aspetta che le stringhe dei componenti cambino, è necessario utilizzare i flussi di lavoro di traduzione convenzionali. Ad esempio, se gli autori possono modificare una stringa dell’interfaccia utente utilizzando le proprietà nella finestra di dialogo Modifica di un componente, non utilizzare un dizionario della lingua per internazionalizzare la stringa.

## Dizionari di lingua {#language-dictionaries}

Il framework di internazionalizzazione AEM utilizza i dizionari nel repository per memorizzare le stringhe inglesi e le loro traduzioni in altre lingue. Il framework utilizza l&#39;inglese come lingua predefinita. Le stringhe vengono identificate utilizzando la loro versione inglese. In genere, i framework di internazionalizzazione utilizzano ID alfanumerici per le stringhe dell’interfaccia utente. L’utilizzo della versione inglese della stringa come ID presenta diversi vantaggi:

* Il codice è facile da leggere.
* La lingua predefinita è sempre disponibile.

Le modifiche di traduzione devono provenire da Git tramite la pipeline [CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) in AEM as a Cloud Service.

![i18n-components-2](/help/implementing/developing/extending/assets/i18n-comp2.png)


### Sovrapposizione di stringhe nei dizionari di sistema {#overlaying-strings-in-system-dictionaries}

Se i componenti utilizzano stringhe incluse nei dizionari di sistema AEM, duplicare la stringa nel proprio dizionario. Tutti i componenti utilizzeranno le stringhe del dizionario.

Non è possibile prevedere quale traduzione viene utilizzata quando le stringhe vengono duplicate nei dizionari che si trovano tutti sotto il nodo `/apps`.
