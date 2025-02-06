---
title: Internazionalizzazione delle stringhe dell’interfaccia utente
description: L’AEM fornisce una console per gestire le varie traduzioni di testi utilizzati nell’interfaccia utente dei componenti.
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 14a6516872f842d099b902b9f633b1d6f984266d
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---


# Utilizzo di Translator per gestire i dizionari{#using-translator-to-manage-dictionaries}

L’AEM fornisce una console per gestire le varie traduzioni di testi utilizzati nell’interfaccia utente dei componenti. Questa console è disponibile all’indirizzo:

`https://<hostname>:<port-number>/libs/cq/i18n/gui/translator.html`

Utilizza lo strumento di traduzione per gestire le stringhe in inglese e le relative traduzioni. I dizionari vengono creati nel repository, ad esempio `/apps/myproject/i18n`.

Lo strumento Traduttore e i dizionari gestiti servono per presentare l’interfaccia utente dei componenti in lingue diverse. Se desideri tradurre le pagine, consulta [Traduzione di contenuti per siti multilingue](/help/sites-cloud/administering/translation/overview.md).

## Creazione di un dizionario {#creating-a-dictionary}

Gli sviluppatori possono creare dizionari i18n in AEM per gestire le stringhe dei componenti localizzati. I dizionari fanno generalmente parte del codice del componente in `/apps`. Di seguito è riportato un esempio tratto dal codice WKND dell’AEM con una coppia chiave/valore utilizzata in tutti i componenti WKND.

```
{
  "&copy; {0} WKND Site Site. All rights reserved." : "&copy; {0} WKND Site Site. Tous droits réservés."
}
```

Gli sviluppatori possono creare dizionari aggiuntivi aggiungendo un nodo radice (`sling:Folder`) per un nuovo dizionario che contenga le definizioni della lingua per le stringhe dei componenti.

```shell
/apps/myProject/i18n [sling:Folder]
    - de.json [nt:file] [mix:language]
        + jcr:language = de
    - fr.json [nt:file] [mix:language]
        + jcr:language = fr
```

>[!NOTE]
>
>Struttura del modulo [Sling i18n](https://sling.apache.org/site/internationalization-support.html).

Una volta creati in un archivio GitHub AEM, i dizionari possono essere distribuiti tramite una pipeline [CI/CD dell&#39;AEM](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

## Posizioni dizionario {#dictionary-locations}

Gli sviluppatori possono creare un dizionario della lingua di origine in `/apps` o `/content/cq:i18n`. Iniziando con il codice di esempio dell&#39;archetipo dell&#39;AEM, i dizionari iniziali si trovano in genere nel percorso `/apps`. Se l&#39;obiettivo è quello di memorizzare le copie per lingua del dizionario corrispondenti anche in `/apps`, tali copie per lingua devono essere create e gestite manualmente dagli sviluppatori nel codice del componente.

In alternativa, il nuovo processo di traduzione runtime AEM per i dizionari i18n creerà dizionari tradotti in `/content/cq:i18n/<projectName>`, indipendentemente dal fatto che il dizionario di origine sia archiviato in `/apps` o `/content`.

Le decisioni su dove collocare dizionari i18n, copie per lingua e sorgente devono essere prese in base ai seguenti criteri:

* `/apps`
   * posizione predefinita per i dizionari con traduzioni di stringhe di componenti, seguendo archetipo AEM e codice di esempio WKND
   * ordine di rendering più alto, per Sling ([Gerarchie di ricerca dei bundle di risorse](https://sling.apache.org/documentation/bundles/internationalization-support-i18n.html#resourcebundle-hierarchies))
   * ma non è possibile modificare o tradurre i dizionari durante il runtime, poiché `/apps` non è modificabile negli ambienti AEM as a Cloud Service

* `/content/cq:i18n`
   * posizione alternativa per i dizionari i18n se
      * è necessaria la traduzione runtime dei dizionari
      * è richiesta la possibilità di modificare un dizionario in fase di runtime
   * percorso predefinito in cui la traduzione del dizionario di runtime creerà copie per lingua.

Poiché `/apps` sostituisce sempre `/content` nell&#39;ordine di rendering Sling, è importante tenere presente che i dizionari con coppie chiave/valore identiche non devono esistere contemporaneamente in `/apps` e `/content/cq:i18n`, in quanto il dizionario in `/content/cq:i18n` non verrà mai utilizzato per il rendering. Se una copia della lingua del dizionario, ovvero una destinazione di traduzione, esiste già in `/apps` e l&#39;obiettivo è quello di renderla traducibile in fase di esecuzione in AEM as a Cloud Service, la copia originale della lingua del dizionario in `/apps` deve essere spostata in `/content/cq:i18n` o eliminata in `/apps` e ricreata automaticamente in `/content/cq:i18n` traducendo il dizionario di origine. Questo processo di traduzione creerà automaticamente le copie per lingua in `/content/cq:i18n`.

## Creazione automatica dizionario {#automatic-creation}

Per le pagine AEM e i frammenti di esperienza contenenti i componenti core AEM, il nuovo processo di traduzione del dizionario eseguirà anche la scansione di tali pagine o frammenti di esperienza per individuare i componenti e le stringhe dei componenti da tradurre. Il sistema creerà quindi automaticamente le corrispondenti nuove copie della lingua del dizionario in `/content/cq:i18n`. Ciò non si applica ai frammenti di contenuto, in quanto si tratta di contenuti puri e strutturati senza l’utilizzo dei componenti core dell’AEM.

## Esportazione di un dizionario {#exporting-a-dictionary}

Anche se la traduzione in fase di esecuzione dei dizionari i18n nei percorsi `/apps` o `/libs` non è possibile in AEM as a Cloud Service in quanto tali percorsi non sono modificabili, è comunque possibile esportare tali dizionari in fase di esecuzione per la traduzione asincrona al di fuori dell&#39;AEM.

Per esportare le stringhe della lingua di origine di un dizionario in un file XLIFF:

1. Apri lo strumento di traduzione `http://<host>:<port>/libs/cq/i18n/gui/translator.html`

   >[!NOTE]
   >
   >Lo strumento è disponibile solo tramite questo URL, non è accessibile dall’interfaccia utente del prodotto AEM.

1. Utilizza il menu a discesa Dizionari per selezionare il dizionario da esportare.
1. Fare clic su Esporta XLIFF Translation e quindi Esporta full `<locale>` xliff.

## Importazione di un dizionario {#importing-a-dictionary}

Per importare un file XLIFF in un dizionario per compilare il contenuto del dizionario:

1. Apri lo strumento di traduzione `http://<host>:<port>/libs/cq/i18n/gui/translator.html`
1. Fai clic su Importa e quindi su Traduzioni XLIFF.
1. Selezionare il file da importare e fare clic su OK.
